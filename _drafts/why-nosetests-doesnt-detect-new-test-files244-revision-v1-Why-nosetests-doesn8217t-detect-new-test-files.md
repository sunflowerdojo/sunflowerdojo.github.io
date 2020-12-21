---
id: 245
title: 'Why nosetests doesn't detect new test files'
date: 2018-05-31T11:08:49-04:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2018/05/31/244-revision-v1/
permalink: /2018/05/31/244-revision-v1/
---
So, why doesn't nosetests run my newly created test file?

Python's nosetests out-of-the-box looks for

  * test files that are prepended with "test_"
  * test classes that are prepended with Test
  * test cases inside of a test class that are prepended with "test_"

However, the test files themselves cannot be marked as executable. Nosetests will ignore executable Python files. To get around this, do

chmod -x "your\_test\_file.py"

and run nosetests again.
