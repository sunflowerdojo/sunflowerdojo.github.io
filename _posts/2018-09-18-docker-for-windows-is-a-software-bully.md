---
id: 278
title: Docker for Windows is a software bully
date: 2018-09-18T20:12:52-04:00
author: Mehron Kugler
layout: post
guid: https://www.sunflowerdojo.com/?p=278
categories:
  - Apps Behaving Badly
---
I went to install Docker for Windows today. It told me that in order for Docker to work, I had to enable Hyper-V, which would make VirtualBox unusable. So in order for it to "work", it needs to disable the competition. Convenient.

<img loading="lazy" class="aligncenter wp-image-284 size-full" src="/wp-content/uploads/2018/09/docker_bully1.png" alt="System error message from Docker" width="693" height="255" srcset="/wp-content/uploads/2018/09/docker_bully1.png 693w, /wp-content/uploads/2018/09/docker_bully1-300x110.png 300w" sizes="(max-width: 693px) 100vw, 693px" />

_"Hyper-V and Containers features are not enabled. Do you want to enable them for Docker to be able to work properly? Your computer will restart automatically. Note: VirtualBox will no longer work."_

Also, to get Docker to install correctly, I had to run the installer with administrative privileges, which could pose a security threat if the downloader was compromised.

It's unfortunate that <a href="https://github.com/docker/for-win/issues/2153" target="_blank" rel="noopener">the developers of Docker decided it was too much work</a> to engineer their software to play nicely with other virtualization platforms. <a href="https://github.com/docker/for-win/issues" target="_blank" rel="noopener">There are 495 active issues just for the Windows version of Docker</a>, keeping the team quite busy.
