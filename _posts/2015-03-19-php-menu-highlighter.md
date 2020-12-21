---
id: 83
title: PHP Menu Highlighter
date: 2015-03-19T17:40:48-04:00
author: Mehron Kugler
layout: post
guid: http://cabriolegraphics.com/blog/?p=5
categories:
  - Coding
tags:
  - php
---
PHP Menu Highlighter &#8211; highlight current page in your navigation menu.

While developing a website recently, I realized I had already produced the navigation menu in a PHP file and used the include function to pull it into each page, so I needed a way to highlight the current page's navigation menu item:

This uses the nth-child(<span style="color: #ff0000;">x</span>) property of CSS to target menu item # <span style="color: #ff0000;">x</span>, where <span style="color: #ff0000;">x</span> is your navigation menu item in an array. Let's say you have the following menu:

<pre>&lt;ul class="navigation"&gt;
 &lt;li&gt;Home&lt;/li&gt;
 &lt;li&gt;About&lt;/li&gt;
 &lt;li&gt;News&lt;/li&gt;
&lt;/ul&gt;</pre>

In PHP you set up an array, like so:

<pre>$menuitems = [
 "home" =&gt; <span style="color: #ff0000;">1</span>,
 "about" =&gt; <span style="color: #ff0000;">2</span>,
 "news" =&gt; <span style="color: #ff0000;">3</span>,
 ];
</pre>

And now that numbers are assigned to each navigation menu item, we can specifically target each menu item using li:nth-child and override linked stylesheets with inline CSS.

Create our PHP function, we'll call it "highlight":

<pre>&lt;?php
 function highlight($index)
 {
   $menuitems = [
   "home" =&gt; 1,
   "about" =&gt; 2,
   "news" =&gt; 3,
   ]; // You can put these all on one line

echo "
 &lt;style&gt;
   ul.navigation &gt; li:nth-child(" . $menuitems[$index] . ") {
   background-color: #B8C7CF;
   }
 &lt;/style&gt;
 ";
 } // end of function
?&gt;</pre>

Save this to "highlight.php"
Then use the function on each page. For example, in the "home.php" page, we would use the highlighter like this:

<pre>&lt;?php include 'highlight.php' ?&gt;
&lt;?php highlight("home"); ?&gt;</pre>

Effectively, "home" is <span style="color: #ff0000;">1</span> in the array, so the html code written by the highlighter produces li:nth-child(<span style="color: #ff0000;">1</span>), which is a way to target the first <li> item in a series of list items.

So this will use CSS to highlight the menu item by way of PHP.

Note: If you are using separators between your navigation menu items, you'll have to adjust the numeric values of each menu item accordingly.

Note: If you have <a> links in your list menu, your function should target the links like so: li:nth-child(x) > a .
