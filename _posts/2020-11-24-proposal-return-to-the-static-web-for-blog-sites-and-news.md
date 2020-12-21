---
title: Proposal: Return to the static web for blog sites and news
date: 2020-11-24T14:58:16-05:00
author: Mehron Kugler
layout: post
categories:
  - Technology
  - Writing
tags:
  - proposal
---
Let the blog system look for new content from its authors each night, build the new pages as static content, and let the web server only deal with serving pages when visitors come, instead of spending time reading from a database each time a visitor arrives.

This will decrease site load times drastically, and with the content hosted outside of the database, visitors can still access content if the database should crash or get hijacked.

Advantages of a database-driven blog system:

  * Can modify a large number of entries at once, such as bulk tagging

Disadvantages of a database-driven blog system:

  * The database is a target for hackers
  * A database server must be running in addition to the web server, and it must receive security patches and upgrades over time
  * Packing up and leaving a database-driven site is proprietary &mdash; the data can't just be exported as text files or documents, and if a writer is using someone else's service, obtaining database backups isn't guaranteed

**A "build" system workflow for nightly website updates:**

The experience is like adding a document to a specific folder, and writing in that new document. That's it.

  1. An author adds a new journal entry (a text file, or Markdown file) to the website folder titled "Journal entries". The author adds a specially formatted line at the top of the document with publish date, entry category, author, and other info
  2. (Advanced) Optionally, the author adds a new file, and a second file for the entry, with information like entry category, author, publish time, etc; this tells the build system where to place the entry during the nightly run
  3. At midnight each day, a system of scripts check for new blog entry files, and generates HTML pages and cached images for each new entry

In this "build" system, the database exists just to let the writer authenticate with the website and drop in new files to the file management area.

Alternately, the writer can use a version control system, like Git, to interact with a repository like Github, and push new versions of files, and new files, to the file server, where the build system will be watching.
