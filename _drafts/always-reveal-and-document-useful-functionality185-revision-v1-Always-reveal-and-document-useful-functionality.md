---
id: 198
title: Always reveal and document useful functionality
date: 2018-03-27T12:09:56-04:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2018/03/27/185-revision-v1/
permalink: /2018/03/27/185-revision-v1/
---
I can operate my Macbook in &#8220;closed-shell&#8221; mode but I never knew about it until I accidentally shut my laptop with my external monitor plugged in &#8230; and my monitor stayed on, to my surprise.

<!--more-->

In &#8220;closed-shell&#8221; mode with an external monitor connected, the laptop can be closed and the external monitor will stay on. I&#8217;ve been using that setup at work.

The other day, I tried using &#8220;closed-shell&#8221; mode, having no idea it was actually called that, without the charger plugged in. It didn&#8217;t work as expected. I thought it was a hardware issue which a reboot would solve &#8212; it didn&#8217;t &#8212; or a PRAM reset might &#8212; it didn&#8217;t &#8212; so off to scour the internet I went.

It took some searching outside of Apple official support channels to discover that <span style="text-decoration: underline;">this feature doesn&#8217;t work unless the Macbook is plugged in</span>. Well, why not? (Cue high-level genius-&#8216;splaining of Apple&#8217;s &#8220;core performance values&#8221;.)

### Create contextual feature alerts

Notifications or guides are appropriate when the situation arises where user behavior could lead to feature discovery.

In this case there could be some notification on the external monitor: &#8220;For performance reasons, please plug in your laptop to use the external monitor in closed-shell mode. This display will turn off in 60 seconds&#8230;&#8221;

or

&#8220;Plug in your laptop to continue to use closed-shell mode (use only this monitor). This display will automatically turn off in 60 .. 59 &#8230; 58.&#8221;

My not-so-modern monitor informs me it will shut off in a few moments after no data from the input source was detected. That is good feedback.