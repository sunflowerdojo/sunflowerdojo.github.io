---
id: 280
title: Better way to return from within try/catch
date: 2018-08-31T08:57:36-04:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2018/08/31/279-revision-v1/
permalink: /2018/08/31/279-revision-v1/
---
Instead of exiting a method with a return statement within a try/catch block, I think it is better design to preset an empty variable, set the value of that variable from within try/catch, and return the variable outside of the block, at the end of the method.

<!--more-->

Standard method which returns something, based on a condition:

<pre>def write_user_data_to_api(test_data: dict) -&gt; str:
    """ Write to the API server, and report the success """
    
    
    

</pre>

&nbsp;

&nbsp;