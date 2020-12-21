---
id: 151
title: Android File Transfer behaves badly
date: 2016-12-14T15:14:02-05:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2016/12/14/56-revision-v1/
permalink: /2016/12/14/56-revision-v1/
---
I plug in my phone to start charging it. The Android File Transfer app auto-starts on my Mac, and moments later, a popup invades my screen and makes me stop whatever I'm doing.

"Can't access device storage," it says, along with some other noise.

It's time for a redesign.

<!--more-->

## Don't interrupt me while I'm working

The alert message is not contained in the main operating window for the app. It breaks its own boundaries, sadly, like many applications tend to do these days.

**Desktop applications and connected devices should communicate better**

Although I can tell my phone to "Just charge this device" when connected via USB, the Android File Transfer application is unaware of how the phone wants to connect. It should listen to configuration settings on my phone and see that my phone is set to charge only &mdash; and not throw a popup in that case.

**Application alerts should not be disruptive**

<figure id="attachment_64" aria-describedby="caption-attachment-64" style="width: 294px" class="wp-caption aligncenter">[<img loading="lazy" class="wp-image-64 size-medium" src="http://www.sunflowerdojo.com/wp-content/uploads/2016/11/Screenshot-2016-11-10-11.27.06-294x300.png" alt="Application popup interferes with daily activity" width="294" height="300" />](http://www.sunflowerdojo.com/wp-content/uploads/2016/11/Screenshot-2016-11-10-11.27.06.png)<figcaption id="caption-attachment-64" class="wp-caption-text">Android File Transfer interrupts desktop activities with its too-important message.</figcaption></figure>

This alert will interrupt my workflow whenever I connect my phone. It doesn't stay open, however &mdash; the application closes immediately. I believe it should stay open to allow me, the user, to reconnect my phone or tweak phone connection settings to allow the application to see the phone.

### Curb your enthusiasm</h2>

How should applications contain their alerts or error messages? A good example is the Printer preferences pane, built in to Mac OS:

<figure id="attachment_67" aria-describedby="caption-attachment-67" style="width: 501px" class="wp-caption aligncenter"><img loading="lazy" class="wp-image-67 size-full" src="http://www.sunflowerdojo.com/wp-content/uploads/2016/11/Screen-Shot-2016-11-16-at-12.03.08-PM.png" alt="The Printer Preferences pane does not create disruptive alerts" width="501" height="319" /><figcaption id="caption-attachment-67" class="wp-caption-text">The Printer Preferences pane does not create disruptive alerts.</figcaption></figure>

The application says "The printer is low on toner" and **contains its message within its own window**. This application and Android File Transfer look visually similar, but behave differently. Google should have done a better job investigating how Apple designed its native applications, and imitated the behavior:

## Let users decide when to quit

In the below mockup, I added the option to quit, or try again, since the application currently does not respect the user by presenting choices. The error message is contained within the application and is not disruptive to other workflows.

For some reason, Google decided to leave out an application window title. I've added one below, since they decided to leave all that empty space there unused.

<figure id="attachment_69" aria-describedby="caption-attachment-69" style="width: 629px" class="wp-caption aligncenter">[<img loading="lazy" class="wp-image-69 size-full" src="http://www.sunflowerdojo.com/wp-content/uploads/2016/11/android_file_transfer_betterdesign.png" alt="A new design for the Android File Transfer app should include a quit button." width="629" height="489" />](http://www.sunflowerdojo.com/wp-content/uploads/2016/11/android_file_transfer_betterdesign.png)<figcaption id="caption-attachment-69" class="wp-caption-text">Let the user decide when to quit, and give them the option to try again.</figcaption></figure>

Now the application won't interrupt me, and it won't quit if things aren't working.  I can plug in my phone and let it charge, and when I'm ready, I can go to the Android File Transfer application and deal with its complaints, on my own time, and Try Again without the application quitting on me.
