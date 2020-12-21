---
id: 265
title: What to do after installing Arch Linux via Termux
date: 2018-07-12T22:48:10-04:00
author: Mehron Kugler
layout: post
guid: https://www.sunflowerdojo.com/?p=265
categories:
  - Linux
---
Always a fan of Linux, I love being in the command line. I found Termux to be the perfect entry point for installing Arch. There are a few housekeeping commands to do once it's installed.

<!--more-->

Brief recap: [How to install Arch Linux on Android via Termux](https://sdrausty.github.io/TermuxArch/docs/install)

After installing, run "tour" to get some helpful aliases set up, and then run "keys" to get all the official keyrings needed for installing packages.

Without keys, attempts to install packages will fail with errors about corrupt keyrings/no trust.
