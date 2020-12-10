---
id: 354
title: 'When apps behave badly, who&#8217;s to blame?'
date: 2020-06-24T13:39:51-04:00
author: Mehron Kugler
layout: post
guid: https://www.sunflowerdojo.com/?p=354
permalink: /2020/06/24/when-apps-behave-badly-whos-to-blame/
categories:
  - Apps Behaving Badly
---
As an example: Notepad++ is one of my favorite Windows text editors. I can trust it to restore my previous working session. I use it to quickly open new notes and store information that I need on-demand. I never need to save the data because the application always saves the state correctly. I have been able to depend on its stable behavior for several months.

That was, until Windows forced me to update the base operating system yesterday, Notepad++ did not &#8220;close correctly&#8221;, and I lost weeks of knowledge on re-opening the application.

<!--more-->

## Picking sides

  1. The user, who did not save their files,
  2. The application developers, who built a feature that saves &#8220;unsaved&#8221; work

It would be easy to pin it on me, the user, for not saving my work: 

_&#8220;You always need to save your work. You never know what&#8217;ll happen while you&#8217;re using the computer,&#8221; the system admin says, wagging a finger._

Well, _that&#8217;s_ unfortunate. Why can&#8217;t I rely on computers to behave?

It would be easy to blame the application developers:

_&#8220;You should have tested more!&#8221; says the angry customer._

## Red Herrings

On re-opening Notepad++, Windows declared:

<blockquote class="wp-block-quote">
  <p>
    Notepad++ did not close properly. Close the application and re-open it.
  </p>
</blockquote>

Why didn&#8217;t it close properly? It&#8217;s my opinion that neither are to blame in this scenario. The fault occurred with the operating system failing to close applications in a respectful way.

The best, most stable software can be made to act in an unstable way if the environment in which it runs is unstable.

Another reason to use an operating system like Debian Linux or OpenSuSe for software development, where information integrity is crucial.