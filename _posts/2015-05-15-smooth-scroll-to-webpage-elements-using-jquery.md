---
title: Smooth scroll to webpage elements using jQuery
date: 2015-05-15T15:58:29-04:00
author: Mehron Kugler
layout: post
categories:
  - Coding
tags:
  - jquery
---
While working on revamping my online portfolio, I wanted a scroll effect after clicking on menu items &mdash; the default "jump to" activity was abrupt, and after designing my Celebrity Name Game and becoming spoiled on effects, I thought it was a good move.

Turns out, however, that it's unwieldy to try and get jQuery to scroll to a named anchor. It seems that scrollTop is best used on "visible" elements, and even using CSS to add the "visibility: visible" property on my html anchors didn't work.

I came up with the following code:

<pre>$("[href|='#prints']").click(function() {
 $(this).unbind("click");
 event.preventDefault();
 $('html, body').animate({
 scrollTop: $("[data-scrollto|='prints']").offset().top-70
 }, 2000);</pre>

In my <h1> element, I put a "data-scrollto" attribute in there, like so:

<h1 data-scrollto="prints">Prints</h1>

In this code, jQuery selects the link in my menus which point to the html anchor "prints" which I put in my code just before the section. But instead of going to the anchor, which just happens immediately, instead I disable the default behavior:

<pre>event.preventDefault();</pre>

and also add an "unbind" command since I learned previously (the hard way) that these commands "pile up" on the selector's event and will repeat multiple times every time the page is loaded.

And now instead of directing the menu link to jump to the html anchor, I instead tell it to scroll to the <h1> element that has the data-scrollto property.

Ideally I should write a function on top of this that can take in variables, so that I don't have to re-use the code each time I want to set the scrolling destination of a menu item. Something like:

<pre>function setScrollTo(menulink, destination) {
...
}</pre>
