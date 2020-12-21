---
id: 325
title: Python-related Windows file permission error (WinError 32)
date: 2020-03-11T00:08:30-04:00
author: Mehron Kugler
layout: post
guid: https://www.sunflowerdojo.com/?p=325
permalink: /?p=325
categories:
  - Coding
tags:
  - python
---
In this case, I have a Windows-specific bug in my Python software, which is not present in Linux systems. My software moves files around if they don't meet certain criteria. When I run my distributable file as a test, I got

PermissionError: [WinError 32] The process cannot access the file because it is being used by another process

This occurs because somewhere I have opened a file and have not closed it. There is a Python-ic way to close and open files, using a context, like so, which automatically closes a file after some operation:

<pre>with open("file", "w+") as f:
    f.write("Some text")</pre>

In this case "w+" means "create a new file by writing to it". After the write message is sent to the file in this context, Python automatically closes the file.

I'm using built-in OS libraries to move files around, and I always use context when creating new files, so what gives?

### Time for some code analysis

If I manage to solve this bug, I hope it helps others. Most importantly, it will help improve my sanity.
