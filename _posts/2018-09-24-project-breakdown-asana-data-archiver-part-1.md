---
id: 298
title: Project breakdown: Asana data archiver, Part 1
date: 2018-09-24T13:28:33-04:00
author: Mehron Kugler
layout: post
guid: https://www.sunflowerdojo.com/?p=298
permalink: /2018/09/24/project-breakdown-asana-data-archiver-part-1/
categories:
  - Coding
  - Design Projects
tags:
  - APIs
  - python
---
My assignment was to get the team's Asana data off of the Asana platform, as the company set a hard date for closing their enterprise account. Since I had done a similar project like this before in Python, and some developers in teams that I interact with also use Python, I chose to use Python for this project.

I am still working on getting permission from my employer to release the project to the public, so the code examples below are my own work not copied from that project.

My approach was as follows:

  1. Read the API documentation for the target server
  2. Model outgoing and incoming data by recording calls to and from the API server
  3. Use a mocking tool to capture network requests during tests
  4. Build iterators that together can assemble the entire structure of a user's Asana account

Mirroring the API models is very important for creating a test system that is free of making actual API calls (no API rate limiting there, no test/real data modified on remote servers, no risk of a test failing because of connectivity/firewall issues).

## Data models

Asana's data is structured like so:

  * Organization
      * Teams
          * Projects
              * Tasks
                  * File attachments
                  * Stories (comments and things like task description updates)

### Caveats

There were some **caveats** that I discovered while making my way through the API and tesing functionality, which I'll list first:

Asana has split each resource (organizations, teams, projects, tasks, attachments, stories) into separate API paths, but in doing so, neglected to leave indicators or references to the presense of sub-resources in the top-level resource.

It is not possible to know, for example, if an organization has any teams by polling the organization resource itself. I need to poll the teams endpoint using the organization ID as an identifier.

Likewise it is not possible to know if a task has any file attachments by polling only the /tasks endpoint; I have to call the file attachments endpoint with the task ID to see if there are any attachments. Even after learning whether a task has endpoint, by querying the attachments endpoint with the task ID, I then had to make a third API call to download the file using the link provided in the second API call.

The demands of creating a complete picture of an organization's total teams, projects, tasks, etc, via API, increase exponentially, and results in excessive API calls. Asana have rate-limited client API calls, which they could probably relax if they hadn't designed an API that required so many API calls just to discover and retrieve related resources.

I think it would make things easier if each resource contained information about what resources are related to it. For example, a response to querying an organization should, in addition to organization metadata, also include the IDs of associated teams; querying teams should also return metadata that includes the associated projects; and so forth. Querying a task should also include URIs for related file attachments, to cut down the number of API calls required.

### User Model

I started with the user's own "user" model. It also contains the user's organization ID, which makes for a good starting point for making queries. Organizations are simply enterprise-level workspaces. I got the user model <a href="https://asana.com/developers/api-reference/users" target="_blank" rel="noopener">from Asana's official documentation</a>:

<pre># Request
curl -H "Authorization: Bearer " \
https://app.asana.com/api/1.0/users/5678

# Response
HTTP/1.1 200
{
  "data": {
    "workspaces": [
      {
        "id": 1337,
        "name": "My Favorite Workspace"
      },
      "~..."
    ],
    "id": 5678,
    "name": "Greg Sanchez",
    "email": "gsanchez@example.com"
  }
}
</pre>

From this I built a small test class method (part of the test class that describes tests) that creates a fake API response from querying that path:

<pre>def gen_fake_user_response(self):
    # Based on data model described here:
    # https://asana.com/developers/api-reference/users
    return {
        "data": {
            "workspaces": [
                {
                    "id": 1337,
                    "name": "My Favorite Workspace"
                },
            ],
            "id": 5678,
            "name": "Greg Sanchez",
            "email": "gsanchez@example.com"
        }
    }
</pre>

However, returning dynamic data will be more interesting, and will better reflect iterating through any number of records. My other methods which consume this test data will then be forced to support dynamic data. For this <a href="https://faker.readthedocs.io/en/master/" target="_blank" rel="noopener">I like to use the Faker library</a>, which has a nice selection of methods for generating fake data:

_Randint is a built-in python library for generating random numbers._

<pre>def gen_fake_user_response(self):
    # Based on data model described here:
    # https://asana.com/developers/api-reference/users
    return {
        "data": {
            "workspaces": [
                {
                    "id": randint(9, 9999),  # int between 10 and 10000
                    "name": fake.company()   # Acme, Inc
                },
            ],
            "id": randint(99, 9999),
            "name": fake.name(),             # Jane Smith
            "email": fake.email()            # brenner@compsci.org
        }
    }
</pre>

What would make the generator more flexible is to take a "workspace" object argument, which it would insert automatically into the "workspaces" key, and make the generated user name match the email address in some fashion, so that while looking through tests logs, the data will appear sensible and I will not be distracted from real issues by seeing data that doesn't match (when in fact mismatched user/email would be &mdash; from a test perspective &mdash; perfectly fine.)

### Tests that define the attributes of the client

Since I am using test-driven development, I describe how the API client will pass tests by **first** writing test assumptions and assertions and **then** the actual client itself. For example:

<pre>class TestAsanaAccessWithClient(TestCase):

    """  Tests for using my own client to call Asana """

    ASANA_BASE_URL = "https://app.asana.com/api/1.0"
    # Set to 123456abcdefg if no token defined in environment
    ASANA_ACCESS_TOKEN = os.environ.get(
        "ASANA_ACCESS_TOKEN", "123456abcdefg"
    )
    HEADER = "Authorization: Bearer %s" % ASANA_ACCESS_TOKEN
    CURRENT_PATH = os.path.dirname(os.path.realpath(__file__))
    TMP_PATH = "%s/tmp" % CURRENT_PATH

    def test_api_wrapper_class(self):

        """ Test setup options for api wrapper class """

        wrapper = api_wrapper.AsanaClient(
            API_KEY=self.ASANA_ACCESS_TOKEN
        )
        self.assertEqual(wrapper.API_KEY, self.ASANA_ACCESS_TOKEN)
        self.assertEqual(wrapper.ASANA_BASE_URL, self.ASANA_BASE_URL)
        self.assertEqual(wrapper.DEFAULT_HEADER, self.HEADER)
        self.assertEqual(
            wrapper.REQUESTS_HEADER,
            {"Authorization": "Bearer %s" % self.ASANA_ACCESS_TOKEN}
        )
</pre>

I specify that the custom client will take an API key as an argument. This is a nice workaround instead of storing an API key in my test code &mdash; a mistake no developer should make. As well this ensures the responsibility of storing the API key is with the client, not a "settings" file.

### First test for getting user data

This may look trivial but this test is meaningful. Although the httpretty library, and any network connection mocking library, will return predetermined data, this is useful for making sure that my retrieval methods in the client do not mangle the data along the way (constant data format) and that the data I want is exposed in a known manner. Asana responds to all API requests (which do not result in errors) with JSON like **{ "data": { &#8230; } }**

Writing tests like this ensures that I test all of my assumptions &mdash; how my retrieval method will respond, what headers it uses, and that the path to the host is created correctly.

**An indirect benefit is that this code tests whether Asana's API documentation is accurate.**

_api_wrapper is the package that I've developed for this project, and AsanaClient should be a good description for the client._

<pre>@httpretty.activate
    def test_get_self_user_data(self):

        """ Test reading data from /users/me """

        httpretty.allow_net_connect = False

        urlpath = "{base}{path}".format(
            base=self.ASANA_BASE_URL,
            path="/users/me"
        )

        expected = self.gen_fake_user_response()

        httpretty.register_uri(
            httpretty.GET,
            urlpath,
            body=json.dumps({"data": expected}),
            status=200
        )

        wrapper = api_wrapper.AsanaClient(
            API_KEY=self.ASANA_ACCESS_TOKEN
        )
        actual = wrapper.read_api_user()
        self.assertDictEqual(expected, actual)
</pre>

This tests that my helper method for making API calls hasn't mangled anything along the way. Additional tests will check that the helper method reacts to API errors. I could add type checking at some point but **it is not useful to type check what comes from the server &mdash; only what goes into my methods to make calls to the server, or other methods.**

## Design tests and functionality through requirements

I created a "to-do" list and create empty tests for each requirement. Every test includes mocking (simulating) the API response. Every software method that I create takes input and produces output, according to my TDD principles.

"The API client shall&#8230;"

  1. Get the organization ID from the user account associated with the supplied API key
  2. Get a list of teams associated with the org ID
  3. For each team in the organization, retrieve detailed attributes
  4. Get a list of projects associated with each team
  5. For each project, retrieve detailed attributes
  6. Get a list of tasks associated with each project
  7. For each task, retrieve detailed attributes
  8. For each task, check if attachments exist
  9. For each task, retrieve stories (comments and task metadata changes)
 10. For each story, download detailed attributes and associate it with the task
 11. For each attachment, download it and associated it with the task
 12. For each downloaded attachment, name it in such a way that it can be identified to a task
 13. For each task, associate it with a project
 14. For each project, associate it with the team
 15. For each team, associate it with the organization
 16. Store the assembled data as a single structure and write it to a file

### Next:

Part two is in the works.
