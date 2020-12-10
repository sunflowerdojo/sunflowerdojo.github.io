---
id: 250
title: Remove executable flag from Pyhton
date: 2018-06-05T09:15:52-04:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2018/06/05/244-autosave-v1/
permalink: /2018/06/05/244-autosave-v1/
---
So, why doesn&#8217;t nosetests run my newly created test file?

Python&#8217;s nosetests out-of-the-box looks for

  * test files that are prepended with &#8220;test_&#8221;
  * test classes that are prepended with Test
  * test cases inside of a test class that are prepended with &#8220;test_&#8221;

However, the test files themselves cannot be marked as executable. Nosetests will ignore executable Python files. To get around this, do

chmod -x &#8220;your\_test\_file.py&#8221;

and run nosetests again.