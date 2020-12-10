---
id: 159
title: Change console (tty) resolution on Debian Wheezy
date: 2016-12-14T15:15:03-05:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2016/12/14/12-revision-v1/
permalink: /2016/12/14/12-revision-v1/
---
I enjoy using Linux and also the terminal, I don&#8217;t have a problem typing all day in front of a wall of text, but I need smaller text so I can see more of it.

**Problem: The text is too large on the console.**

_Solution: Update your TTY config file with a video &#8220;mode&#8221;._

By console I mean the TTY console (press ctrl-alt-f1 through f6). First, make sure hwinfo is installed:

<pre>sudo apt-get install hwinfo</pre>

Then run:

<pre>hwinfo --framebuffer</pre>

This will list a bunch of video modes (resolutions and bit depth, by codes). Find the video resolution you want to use and its code. Mine listed

<pre>Mode 0x031b: 1280x1024 (+5120), 24 bits</pre>

This looked good to me. Edit the configuration file for the TTY consoles:

<pre>sudo nano /etc/default/console-setup</pre>

In the field titled &#8220;VIDEOMODE&#8221;, add the code of the video mode you&#8217;d like. I put:

<pre>VIDEOMODE=0x031b</pre>

For Nano users, hit Ctrl-x and Y to save changes. Run

<pre>sudo update-grub</pre>

Then, restart your computer. You should have a higher resolution text display the next time you switch to the TTY console.

&nbsp;