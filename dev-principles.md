---
id: 312
title: Dev Principles
date: 2018-09-24T13:10:23-04:00
author: Mehron Kugler
layout: page
permalink: /dev-principles
---
Generally, I think of other people when I design and when I code. I&#8217;m writing software to make other people&#8217;s lives easier, and sometimes to make my own job easier, by creating software tools to fill a need.

Software stability is sacred to me. That is why I use test-driven development to build my projects. That way if I break something, I am only a step or two away from working code, and as well, if I change something, running tests will make sure the new changes are in line with my existing assumptions. I always test even the simplest of my assumptions. If my assumptions change, then first I change all the tests to break the code, and then go fix the code to pass the tests. Assumptions don&#8217;t have to be perfect at the start. There will always be revisions later on.

### Development principles

Development princples are &#8220;how I think about how software could solve a problem, and how to relate to others about this project.&#8221;

  * **Design for the user** &#8212; some people don&#8217;t like command line apps. Some people just want to drop a file in a folder that triggers a process and they can walk away. Make my product easy for them to wield
  * **Design for team members and other developers in the company** &#8212; If my project is any good, other people will want to use it, and it should be in a technology that a majority of them can use
  * **Design for portability** &#8212; My software should be usable by other software and plugging it in should be doable in two lines
  * **Keep external dependencies few** &#8212; I read somewhere that it&#8217;s better practice to quickly write up an integration than to fill up my project with external dependencies. Often, importing other solutions also brings along a lot of code that I don&#8217;t need. I have found that in practice this is true. For example, writing my own CSV-to-JSON converter taught me some neat tricks, and I did it in 20 or so lines. A classic example of over-dependency is the &#8220;left-pad&#8221; library. Fewer external dependencies means fewer issues porting to other environments and operating systems
  * **Complete documentation** &#8212; Someone without coding knowledge should be able to look at my project and figure out what it does, the same as another developer. There are too many projects with poor or no documentation. What good is software if no one else can use it?

### Implementation principles

Implementation principles are &#8220;how I code.&#8221;

  * **Keep it separate AKA &#8220;Single Responsibility&#8221;, &#8220;Separation of Concerns&#8221;** &#8212; each programmed method has one job, which makes it easier to unit test and to debug
  * **All methods take input and produce output** &#8212; this is to improve debugging and the testable quality of the code; &#8220;What gets measured gets managed.&#8221;
  * **Take care when naming things** &#8212; Naming things is an art and is developed through experience. Reduce redundancy, improve clarity. For loosely typed languages, good variable names can hint at the data structure. I like to also give some indication of what other processes does a method touch &#8212; TVSeriesReportScraper says more than PdfScraper.
  * **Avoid nested &#8220;for&#8230;&#8221; loops, use list comprehension, generators, or recursion instead** &#8212; I always want to keep the time complexity of my software low. A basic computer science principle. Languages have constructs that support this. Python, for example, supports iterating through multiple lists in a single declaration. While behind-the-scenes this might involve nested for loops masquerading as non-time-complex methods, this builds better thinking habits and challenges my problem-solving skills by looking for alternative methods to established conventions
  * **Be consistent with code style** &#8212; This generally means fewer questions from other developers, for example, why I formatted a string one way where in another case, I formatted it a different way. Style consistency contributes to my overall professional discipline.
  * **Make use of whitespace** &#8212; Again this improves readability not just for myself but for others as well. I am not shy about whitespace, as I am writing test-driven, shareable software at work.
  * **Code only what is necessary** &#8212; Completing all the &#8220;nice-to-haves&#8221; is a great emotional feeling but it could quickly end up as wasted time if the project priorities change. I take time to nail the &#8220;nice-to-haves&#8221; when the project is mature enough that the end is near and I can justify the extra time.
  * **Reduce code smell and follow my instincts to edit** &#8212; Detecting &#8220;code smell&#8221; is something that comes with experience. I have learned to follow my intuition and to improve areas of my code that look messy, ie, the code &#8220;smells.&#8221; I am always better off as I might learn a new technique, and I feel more ownership over my craft

I also follow <a href="https://blog.cleancoder.com/uncle-bob/2015/11/18/TheProgrammersOath.html" target="_blank" rel="noopener">Robert Martin&#8217;s &#8220;The Programmer&#8217;s Oath.&#8221;:</a>

> The Programmer&#8217;s Oath  
> 18 November 2015
> 
> In order to defend and preserve the honor of the profession of computer programmers,  
> I Promise that, to the best of my ability and judgement:
> 
> I will not produce harmful code.
> 
> The code that I produce will always be my best work. I will not knowingly allow code that is defective either in behavior or structure to accumulate.
> 
> I will produce, with each release, a quick, sure, and repeatable proof that every element of the code works as it should.
> 
> I will make frequent, small, releases so that I do not impede the progress of others.
> 
> I will fearlessly and relentlessly improve my creations at every opportunity. I will never degrade them.
> 
> I will do all that I can to keep the productivity of myself, and others, as high as possible. I will do nothing that decreases that productivity.
> 
> I will continuously ensure that others can cover for me, and that I can cover for them.
> 
> I will produce estimates that are honest both in magnitude and precision. I will not make promises without certainty.
> 
> I will never stop learning and improving my craft.

&nbsp;
