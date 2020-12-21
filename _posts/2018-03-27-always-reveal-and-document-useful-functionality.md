---
title: Always reveal and document useful functionality
date: 2018-03-27T12:09:56-04:00
author: Mehron Kugler
layout: post
categories:
  - Apps Behaving Badly
  - User Experience
---
I can operate my Macbook in "closed-shell" mode but I never knew about it until I accidentally shut my laptop with my external monitor plugged in &#8230; and my monitor stayed on, to my surprise.

<!--more-->

In "closed-shell" mode with an external monitor connected, the laptop can be closed and the external monitor will stay on. I've been using that setup at work.

The other day, I tried using "closed-shell" mode, having no idea it was actually called that, without the charger plugged in. It didn't work as expected. I thought it was a hardware issue which a reboot would solve &mdash; it didn't &mdash; or a PRAM reset might &mdash; it didn't &mdash; so off to scour the internet I went.

It took some searching outside of Apple official support channels to discover that <span style="text-decoration: underline;">this feature doesn't work unless the Macbook is plugged in</span>. Well, why not? (Cue high-level genius-&#8216;splaining of Apple's "core performance values".)

### Create contextual feature alerts

Notifications or guides are appropriate when the situation arises where user behavior could lead to feature discovery.

In this case there could be some notification on the external monitor: "For performance reasons, please plug in your laptop to use the external monitor in closed-shell mode. This display will turn off in 60 seconds&#8230;"

or

"Plug in your laptop to continue to use closed-shell mode (use only this monitor). This display will automatically turn off in 60 .. 59 &#8230; 58."

My not-so-modern monitor informs me it will shut off in a few moments after no data from the input source was detected. That is good feedback.
