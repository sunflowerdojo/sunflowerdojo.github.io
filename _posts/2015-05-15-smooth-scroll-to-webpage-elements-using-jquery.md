---
id: 18
title: Smooth scroll to webpage elements using jQuery
date: 2015-05-15T15:58:29-04:00
author: Mehron Kugler
layout: post
guid: http://cabriolegraphics.com/blog/?p=18
permalink: /2015/05/15/smooth-scroll-to-webpage-elements-using-jquery/
categories:
  - Coding
tags:
  - jquery
---
While working on revamping my online portfolio, I wanted a scroll effect after clicking on menu items &#8212; the default &#8220;jump to&#8221; activity was abrupt, and after designing my Celebrity Name Game and becoming spoiled on effects, I thought it was a good move.

Turns out, however, that it&#8217;s unwieldy to try and get jQuery to scroll to a named anchor. It seems that scrollTop is best used on &#8220;visible&#8221; elements, and even using CSS to add the &#8220;visibility: visible&#8221; property on my html anchors didn&#8217;t work.

I came up with the following code:

<pre>$("[href|='#prints']").click(function() {
 $(this).unbind("click");
 event.preventDefault();
 $('html, body').animate({
 scrollTop: $("[data-scrollto|='prints']").offset().top-70
 }, 2000);</pre>

In my <h1> element, I put a &#8220;data-scrollto&#8221; attribute in there, like so:

<h1 data-scrollto=&#8221;prints&#8221;>Prints</h1>

In this code, jQuery selects the link in my menus which point to the html anchor &#8220;prints&#8221; which I put in my code just before the section. But instead of going to the anchor, which just happens immediately, instead I disable the default behavior:

<pre>event.preventDefault();</pre>

and also add an &#8220;unbind&#8221; command since I learned previously (the hard way) that these commands &#8220;pile up&#8221; on the selector&#8217;s event and will repeat multiple times every time the page is loaded.

And now instead of directing the menu link to jump to the html anchor, I instead tell it to scroll to the <h1> element that has the data-scrollto property.

Ideally I should write a function on top of this that can take in variables, so that I don&#8217;t have to re-use the code each time I want to set the scrolling destination of a menu item. Something like:

<pre>function setScrollTo(menulink, destination) {
...
}</pre>