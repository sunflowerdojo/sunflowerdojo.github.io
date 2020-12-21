---
id: 311
title: My development principles
date: 2018-09-24T13:07:44-04:00
author: Mehron Kugler
layout: revision
guid: https://www.sunflowerdojo.com/2018/09/24/290-revision-v1/
permalink: /2018/09/24/290-revision-v1/
---
Generally, I think of other people when I design and when I code. I'm writing software to make other people's lives easier, and sometimes to make my own job easier, by creating software tools to fill a need.

Software stability is sacred to me. That is why I use test-driven development to build my projects. That way if I break something, I am only a step or two away from working code, and as well, if I change something, running tests will make sure the new changes are in line with my existing assumptions. I always test even the simplest of my assumptions. If my assumptions change, then first I change all the tests to break the code, and then go fix the code to pass the tests. Assumptions don't have to be perfect at the start. There will always be revisions later on.

### Development principles

Development princples are "how I think about how software could solve a problem, and how to relate to others about this project."

  * **Design for the user** &mdash; some people don't like command line apps. Some people just want to drop a file in a folder that triggers a process and they can walk away. Make my product easy for them to wield
  * **Design for coding colleages and other developers in the company** &mdash; If my project is any good, other people will want to use it, and it should be in a technology that a majority of them can use
  * **Design for portability** &mdash; My software should be usable by other software and plugging it in should be doable in two lines
  * **Keep external dependencies few** &mdash; I read somewhere that it's better practice to quickly write up an integration than to fill up my project with external dependencies. Often, importing other solutions also brings along a lot of code that I don't need. I have found that in practice this is true. For example, writing my own CSV-to-JSON converter taught me some neat tricks, and I did it in 20 or so lines. A classic example of over-dependency is the "left-pad" library. Fewer external dependencies means fewer issues porting to other environments and operating systems
  * **Complete documentation** &mdash; Someone without coding knowledge should be able to look at my project and figure out what it does, the same as another developer. There are too many projects with poor or no documentation. What good is software if no one else can use it?

### Implementation principles

Implementation principles are "how I code."

  * **Keep it separate AKA "Single Responsibility", "Separation of Concerns"** &mdash; each programmed method has one job, which makes it easier to unit test and to debug
  * **All methods take input and produce output** &mdash; this is to improve debugging and the testable quality of the code; "What gets measured gets managed."
  * **Take care when naming things** &mdash; Naming things is an art and is developed through experience. Reduce redundancy, improve clarity. For loosely typed languages, good variable names can hint at the data structure. I like to also give some indication of what other processes does a method touch &mdash; TVSeriesReportScraper says more than PdfScraper.
  * **Avoid nested "for&#8230;" loops, use list comprehension, generators, or recursion instead** &mdash; I always want to keep the time complexity of my software low. A basic computer science principle. Languages have constructs that support this. Python, for example, supports iterating through multiple lists in a single declaration. While behind-the-scenes this might involve nested for loops masquerading as non-time-complex methods, this builds better thinking habits and challenges my problem-solving skills by looking for alternative methods to established conventions
  * **Be consistent with code style** &mdash; This generally means fewer questions from other developers, for example, why I formatted a string one way where in another case, I formatted it a different way. Style consistency contributes to my overall professional discipline.
  * **Make use of whitespace** &mdash; Again this improves readability not just for myself but for others as well. I am not shy about whitespace, as I am writing test-driven, shareable software at work.
  * **Code only what is necessary** &mdash; Completing all the "nice-to-haves" is a great emotional feeling but it could quickly end up as wasted time if the project priorities change. I take time to nail the "nice-to-haves" when the project is mature enough that the end is near and I can justify the extra time.
  * **Reduce code smell and follow my instincts to edit** &mdash; Detecting "code smell" is something that comes with experience. I have learned to follow my intuition and to improve areas of my code that look messy, ie, the code "smells." I am always better off as I might learn a new technique, and I feel more ownership over my craft

I also adhere to <a href="https://blog.cleancoder.com/uncle-bob/2015/11/18/TheProgrammersOath.html" target="_blank" rel="noopener">Robert Martin's "The Scribe's Oath."</a>

&nbsp;
