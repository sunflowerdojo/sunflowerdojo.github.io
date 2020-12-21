---
id: 243
title: Put folders in sys path so Python 3 can find them
date: 2018-06-05T09:14:04-04:00
author: Mehron Kugler
layout: post
guid: https://www.sunflowerdojo.com/?p=243
categories:
  - Coding
tags:
  - python
---
Problem: I want to import a file in the same folder

Problem 2: I want to import a file from a subfolder

Solution: Add folder path to Python's sys.path

<!--more-->Sample layout

<pre>my_package
|
|----__init__.py
|----myapp.py
|----client.py
|----/utils
|--------__init__.py
|--------client_tools.py</pre>

With the following pattern in myapp.py

<pre>from client import ClientClass</pre>

Yet Python will argue

<pre>ModuleError: No module named 'client'</pre>

Yet clearly client.py is right there in the same folder. What gives?

### Solution: Add info to the folder's \_\_init\_\_.py

For each folder having Python files in them, add the following to the init files:

<pre>import os, sys
sys.path.append(os.path.dirname(os.path.realpath(__file__)))</pre>

When Python sees the init files, it'll now register the directory in the system path, which is where it looks to find modules/files/packages being imported.

So now in myapp, both of these imports will work

<pre>from client import ExampleClass
from utils.client_tools import AnotherClass</pre>
