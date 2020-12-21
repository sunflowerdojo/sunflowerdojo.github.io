---
id: 250
title: Remove executable flag from Pyhton
date: 2018-06-05T09:15:52-04:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2018/06/05/244-autosave-v1/
permalink: /2018/06/05/244-autosave-v1/
---
So, why doesn't nosetests run my newly created test file?

Python's nosetests out-of-the-box looks for

  * test files that are prepended with "test_"
  * test classes that are prepended with Test
  * test cases inside of a test class that are prepended with "test_"

However, the test files themselves cannot be marked as executable. Nosetests will ignore executable Python files. To get around this, do

chmod -x "your\_test\_file.py"

and run nosetests again.
