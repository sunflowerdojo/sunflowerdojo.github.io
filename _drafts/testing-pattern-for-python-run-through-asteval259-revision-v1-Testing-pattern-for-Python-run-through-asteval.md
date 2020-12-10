---
id: 262
title: Testing pattern for Python run through asteval
date: 2018-07-03T16:50:26-04:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2018/07/03/259-revision-v1/
permalink: /2018/07/03/259-revision-v1/
---
An enterprise application I am developing for is processing my Python scripts using asteval. Without classes, imports, and other built-ins, this presents some interesting challenges for automated testing.

<!--more-->

  
In my current job I can upload Python scripts to an enterprise application where the scripts are executed server-side. I didn&#8217;t realize it until after a while that the server is interpreting the Python scripts through asteval, a library developed to be a safer version of &#8220;eval.&#8221; I can guess that the developers want to reduce the risk of malicious behavior on their servers by blocking imports, classes, and other built-in methods. They did document this but I didn&#8217;t understand the full extent.

I am developing an API integration to be used server-side to communicate with a third-party API. My usual pattern is to develop a client class with standard CRUD methods, and then in my automated tests, set up mocking instances for calls to the API so that I can test my code.

The revised testing workflow runs something like this:

  1. Write a method
  2. In the automated test, get its source code using inspect.getsource()
  3. Load the source code into the asteval interpreter, and watch for errors

**Workaround for a client class**

I like to have the API host, base path, and request headers set up in a tidy class. The classless workaround I developed is to take a step back and write a method that returns a dictionary, like so:

<pre>def client_requests_settings():

""" Hard-coded client settings
Have to hard code settings because classes aren't allowed in asteval
Otherwise this would be a client class that could take parameters
"""

    return {
        "endpoint": "http://some-api-server.tld/api",
        "headers": {
            "Accept": "application/json",
            "Content-Type": "application/json; charset=utf-8"
        }
    }
</pre>

Now the pattern for an HTTP request:

<pre>def client_get(api_path):

""" Base method for gets. Always return a debug object for inspection
:param api_path: String. Something like /media , etc
"""

    url = "{base_url}{api_path}".format(
        base_url=client_requests_settings()["endpoint"],
        api_path=api_path
    )
    r = requests.get(url, headers=client_requests_settings()["headers"])
    return r.json(), {"status_code": r.status_code}
</pre>

I always like to return a debug object so I can inspect what I put in to the method. It would not work to build arguments into client\_requests\_settings because then every encapsulating method would have to take those arguments as well and trickle them in to client\_requests\_settings. Unfortunately in this case, hard-coding seems like the most viable and concise method for ensuring parameters are the same across request types.

### Automatically test the method with asteval

<pre>from inspect import getsource
from asteval import Interpreter, make_symbol_table

class TestMethodsThroughAsteval(TestCase):

""" Run these methods through asteval """

    # Put in a reference to the libraries that the upstream server allows
    # So I can reference 'requests' within interpret()

    syms = make_symbol_table(requests=requests, re=re, json=json)
    interpret = Interpreter(symtable=syms)

    def load_and_eval(self, source_method):
        """ Save some LOC """
        logger.debug("Putting %s through asteval" % source_method)
        try:
            self.interpret(getsource(source_method))
        except:
            self.fail("%s didn't pass asteval" % source_method)
            # Print traceback info for better error clarity

    def test_asteval_mediaflex_requests_settings(self):

        """ Run client_requests_settings through asteval """

        self.load_and_eval(client_requests_settings)
</pre>

For each method written, create a test method and test its source with load\_and\_eval.

&nbsp;