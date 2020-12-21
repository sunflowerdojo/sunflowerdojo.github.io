---
id: 12
title: Change console (tty) resolution on Debian Wheezy
date: 2015-03-19T21:36:58-04:00
author: Mehron Kugler
layout: post
guid: http://cabriolegraphics.com/blog/?p=12
permalink: /2015/03/19/change-console-tty-resolution-on-debian-wheezy/
categories:
  - Linux
tags:
  - debian
  - tty
---
I enjoy using Linux and also the terminal, I don't have a problem typing all day in front of a wall of text, but I need smaller text so I can see more of it.

**Problem: The text is too large on the console.**

_Solution: Update your TTY config file with a video "mode"._

By console I mean the TTY console (press ctrl-alt-f1 through f6). First, make sure hwinfo is installed:

<pre>sudo apt-get install hwinfo</pre>

Then run:

<pre>hwinfo --framebuffer</pre>

This will list a bunch of video modes (resolutions and bit depth, by codes). Find the video resolution you want to use and its code. Mine listed

<pre>Mode 0x031b: 1280x1024 (+5120), 24 bits</pre>

This looked good to me. Edit the configuration file for the TTY consoles:

<pre>sudo nano /etc/default/console-setup</pre>

In the field titled "VIDEOMODE", add the code of the video mode you'd like. I put:

<pre>VIDEOMODE=0x031b</pre>

For Nano users, hit Ctrl-x and Y to save changes. Run

<pre>sudo update-grub</pre>

Then, restart your computer. You should have a higher resolution text display the next time you switch to the TTY console.

&nbsp;
