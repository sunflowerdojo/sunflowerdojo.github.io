---
id: 296
title: 'Project analysis: TDD approach to building an API client'
date: 2018-09-18T21:32:18-04:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2018/09/18/290-revision-v1/
permalink: /2018/09/18/290-revision-v1/
---
My most recent work project to date, where I am the solo dev and designer, is a PDF scraper. I'm building it in Python, which has great libraries for making HTTP requests and scraping text out of PDFs. The goal is to be able to drop PDFs into a folder, which the scraper will watch, extract content, and publish it to a piece of enterprise software.

I follow the same tried-and-true strategy that I've developed when creating API clients:

  1. Read the API documentation for the target server
  2. Model outgoing and incoming data by recording calls to and from the API server
  3. Use a mocking tool to capture network requests during tests

My development philosophy is that of test-driven development: I first start with tests, and then write code which makes the tests pass. That way if I break something, I am only a step or two away from working code, and as well, if I change something, running tests will make sure the new changes are in line with my existing assumptions. If my assumptions change, then first I change all the tests to break the code, and then go fix the code to pass the tests. Assumptions don't have to be perfect at the start. There will always be revisions later on.

<!--more-->

### What makes code testable?

In my opinion, testable methods all take input and produce output. "What gets measured, gets managed."

This might seem like a no-brainer, and far too elementary, but there are plenty of libraries out there with methods that take no input whatsoever; some methods write directly to disk instead of producing output for another method to consume.

I have also started a pattern where I return two objects from my testable methods: one, the payload object, which has the data that I'm interested in, the data to be consumed by the next method in line, and a second object which I call a "debug" object which has copies of the data that went in as well as other "debug" information that I might want to use to analyze the state of some process (the data object that I posted to the API server). I can use the debug object for more thorough test introspection.

For example, here are two settings objects. The first is not testable because it has no input; the second is testable:

<pre>class ServerSettings():
    # A settings object for use with an http library

    def __init__(self):
        self.hostname = "https://www.example.com"
        self.headers = {
            "Accept": "application/json;"
        }

class TestableServerSettings():
    # A testable settings object

    def __init__(self, **opts):
        self.hostname = opts.get("hostname")
        self.headers = {
            "Accept": "application/json;"
        }
</pre>

The first one is, arguably, testable because I can measure its output, but there is no point to measuring its output because the output will always be static, and for an API client that is not really useful when I have a development server to fill with test data, and a production server to fill with real data.

### Making models and generators

I always create some generator methods to produce data structures that match what the API server returns for various paths, but with different values each time so I know my consumers can handle random values. Likewise I have little factories that create data structures in the expected shape for transmission to the API server. At first, I do not make these methods malleable; they return a fixed structure, taking no input, but with fresh values each instance. Later, I tweak them to take arguments if needed.

Things I create generators for:

  1. API responses to GET, POST methods (and other supported methods) to the various paths I will be interacting with at the API server
  2. Data structures for transmission to the API server's various paths using the various HTTP methods
  3. Server responses with various HTTP codes (200, 201, 404, 409, 500) using the various methods. This includes error messages

I create the generators as I go along. The first helper method I usually work on supports GET requests, so I build up all the associated generators at that time. Because of all this test infrastructure, I can already use a mocking tool like "requests-mock" at this stage to capture GET requests and return whatever data I want, and I can test an array of server responses before spending any real attempts to contact the API server with my self-made client.

My ideal is to build all of my tests, and run each helper method "live" to the api server as few times as possible to correct my assumptions.

An eager developer might already have helper methods for making GET and POST requests made to the server at this point, including POST or PATCH for several endpoints.

The first folly with this approach, that I've experienced, occurs during error handling, because the error handling can be poor when the server returns an unexpected error. Or maybe the server returns 500s in XML format and not JSON, and these errors are lost because:

  1. HTTP call methods have no automated way to prove they work
  2. Error handling is typically absent
  3. Values can be passed between client methods with a None or null value and there are no built-in assertions around type checking

I witnessed a team at work create 500+ new records on the production server titled "Undefined" with a mess of values, a few weeks after I started my new job. I took a look at their code repo and they had absolutely no software tests. This disaster created several days of extra work which my colleagues had to resolve by hand-editing the database.

### Tests are tedious but worth it

Usually when I run an integration test or test chaining a few methods together, the setup becomes pretty large, and when it's time to create a similar test with a similar setup, copying and pasting one test to another is not efficient because:

  1. Test setup can be better replicated using a setUp() method (fewer lines of code)
  2. Copying and pasting copies the good and the bad (typos, wrong variable names, etc)

Copying and pasting contributes to "test fatigue." I've noticed it in myself when I feel myself leaning towards cutting corners because of the work load. Cutting corners means writing code without tests, and that always, 100% of the time, backfires, because sooner or later, I run into an issue, and I have no visibility into it because I don't have a tested method that's being managed.

Also, it is more efficient to create separate test classes for each server endpoint, than copying and pasting test setups, because I will use different fake data generators for each.

### Assertions are for working code and for tests

I have found that adding assertions into my methods works wonders. Especially for servers with numerous endpoints that can receive fairly large data strutures, it can be easy for me to forget which search terms are supported for a particular endpoint, for example. Take the following "consumer" method:

<pre>def assemble_book_information_from_scraped_pdf(
    scraped_pdf_keys: dict = {}
):
    """ Helper method to take scraped text from book overview PDF and assemble data
    structure for creating a server-side record """

    required_pdf_keys = [
        "title", "author", "isbn", "year"
    ]
    keys_missing_message = "The PDF scrape did not complete as expected. Required keys:"\
        {keys}. This scrape only has {scrape_keys}".format(
            keys=required_pdf_keys,
            scrape_keys=scrape_pdf_keys.keys()
        )
    assert(
        all(
            [key in required_pdf_keys for key in scraped_pdf_keys]
        ), keys_missing_message
    )
    return {
        "book": {
            "Book Title": scraped_pdf_keys["title"],
            "Author Name": scraped_pdf_keys["author"],
            "ISBN Code": scraped_pdf_keys["isbn"],
            "Publication Year": scraped_pdf_keys["year"]
        }
    }
</pre>

If the scraping fails (assuming the source method only returns keys for found values), this method, which prepares the data for the server, will break immediately, and serves to exactly pinpoint the error. Likewise it will ensure that my test data going in to it also adheres to these rules.

I could add extra assertions to check that not only does the incoming data have the expected keys, but they have values.
