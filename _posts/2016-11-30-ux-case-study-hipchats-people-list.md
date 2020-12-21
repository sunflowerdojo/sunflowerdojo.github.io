---
id: 104
title: 'UX Case Study: Hipchat's "People" list'
date: 2016-11-30T16:55:32-05:00
author: Mehron Kugler
layout: post
guid: http://www.sunflowerdojo.com/?p=104
categories:
  - User Experience
tags:
  - case study
---
In this post I take a look at improving the usability of the popular chat client, HipChat, to make it easier to find people. Currently it is difficult to locate people in the side bar if you have a lot going on.

<!--more-->

## Current Usability: Good

I can currently drag and drop names up and down in the list to set my own preferred order, but in day-to-day communications, I am chatting with a number of people; team members start chats with me out of the blue. Before long, my list of people is quite long. I have to visually scan a very long list of names, all of them different, to find someone I want to chat with, so my workaround is to click the "New Chat" button and start typing the name of someone I need to communicate with.<figure id="attachment_107" aria-describedby="caption-attachment-107" style="width: 102px" class="wp-caption alignleft">

[<img loading="lazy" class="wp-image-107 size-medium" src="http://www.sunflowerdojo.com/wp-content/uploads/2016/11/hipchat_people_sidebar1-102x300.png" alt="Persons with whom you have chatted are listed in the People sidebar." width="102" height="300" />](http://www.sunflowerdojo.com/wp-content/uploads/2016/11/hipchat_people_sidebar1.png)<figcaption id="caption-attachment-107" class="wp-caption-text">Persons with whom you have chatted are listed in the People sidebar.</figcaption></figure>

**Problem**: It's time consuming and inefficient to use the People sidebar to find people when there are many of them. Manual sorting doesn't scale.

**Solution**: Develop a way of sorting that can scale.

Current method of locating people:

  * Sort the People pane yourself and try to stay organized

or

  * Use the "New Chat" button to continue a chat with an existing team member (But why have a People sidebar if I'm just going to use a button to search for them?)

Better workflow:

  * Use different automatic sorting options to find people and present them in a way that I know how to easily traverse

Proposed sorting methods:

  * Alphabetically: Natural sorting order that people are used to, but the word "Alphabetically" would be rather long to have in a UI, so maybe we can abbreviate it "A &#8211; Z" and do the same for reverse alphabetical sort: "Z &#8211; A"
  * Recent: I want to find people with whom I have chatted recently, to catch up on a topic
  * Frequent: I want to find people with whom I chat frequently

Perhaps organizing these options in a drop-down menu would be a good start:

### Mockup with dropdown menu<figure id="attachment_109" aria-describedby="caption-attachment-109" style="width: 445px" class="wp-caption aligncenter">

<img loading="lazy" class="size-full wp-image-109" src="http://www.sunflowerdojo.com/wp-content/uploads/2016/11/hipchat_people_sidebar_dropdown.png" alt="I propose putting a dropdown at the top of the People menu for sorting." width="445" height="516" /> <figcaption id="caption-attachment-109" class="wp-caption-text">A good place for sorting might be at the top of the feature.</figcaption></figure>

This is a good start. But maybe the word "Sort" is redundant; A &#8211; Z might be enough indication that there's a way to sort People. If I take out "Sort", I can make the dropdown slightly larger and the text won't be as compressed. Perhaps making it less bold will help it fit in better to the surroundings:<figure id="attachment_110" aria-describedby="caption-attachment-110" style="width: 445px" class="wp-caption aligncenter">

<img loading="lazy" class="size-full wp-image-110" src="http://www.sunflowerdojo.com/wp-content/uploads/2016/11/hipchat_people_sidebar_final.png" alt="Imply sorting with well known &quot;A - Z&quot; and down arrow (dropdown indicator)" width="445" height="480" /> <figcaption id="caption-attachment-110" class="wp-caption-text">Imply sorting with well known "A &#8211; Z" and down arrow (dropdown indicator)</figcaption></figure>

## Conclusion

Automated sorting scales well and this functionality will help improve the Hipchat user experience.

**Next steps:**

Move people-sorting actions to a menu in the application window menu to declutter the UI?
