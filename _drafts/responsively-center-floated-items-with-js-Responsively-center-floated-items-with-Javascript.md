---
id: 38
title: Responsively center floated items with Javascript
date: 2015-06-02T22:46:10-04:00
author: Mehron Kugler
layout: post
guid: http://cabriolegraphics.com/blog/?p=38
permalink: /?p=38
categories:
  - Coding
tags:
  - javascript
  - jquery
---
Recently I tackled the problem of centering the floated grid of card items in my portfolio. Since they were all floated to the left, when the window grew too small and kicked off an item to the next row, there was leftover space.

My portfolio (div class=&#8221;portfolio&#8221;) contains any number of portfolio items, shown in cards (div class=&#8221;card&#8221;).

There is still a bit of leftover space which makes the display of grid items uneven (more empty space on the right than the left.)

I used basic pseudo-math to sort things out:

  1. Portfolio width divided by card width, dropping the remainder = number of cards in a row at any given time
  2. Number of cards in a row times card width = used space
  3. Portfolio width minus used space = extra space which needs to be distributed evenly at the margins
  4. Adjusted margin = extra space divided by 2

I drew up the following Javascript, based on http://stackoverflow.com/a/3150139 :

<pre>$( function() {

function go(){
 port_width = $('div.portfolio').outerWidth( true );
 // console.log("portfolio width is " + port_width);
 card_width = $('div.card').outerWidth( true ); // should be 228 px
 // console.log("card width is " + card_width);
 num_of_cards_in_row = Math.floor(port_width / card_width);
 // console.log("There are " + num_of_cards_in_row + " in a row.");
 used_space = (card_width * num_of_cards_in_row);
 remainder = (port_width - used_space);
 // console.log("The extra space remaining is " + remainder);
 newmargin = (remainder / 2);
 // console.log("Therefore the margins should be " + newmargin + " each.");

$('div.portfolio').css("margin-left", newmargin);
$('div.portfolio').css("margin-right", newmargin);
 // document.querySelector('.width').innerText = document.documentElement.clientWidth;
 // document.querySelector('.height').innerText = document.documentElement.clientHeight;
}

go();
window.addEventListener('resize', go);

});</pre>

In order for .width() to pay attention to the container&#8217;s margins, it needs to specify .width( true ).

This should be applicable to any container which has items of equal sizes within, floated to the left (or right).

CSS animators should be interested to know that transition: margin does not work in this situation; the margins animate as expected but it causes a bug which interferes with the calculations and the margin calculations never recover.