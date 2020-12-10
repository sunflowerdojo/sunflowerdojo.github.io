---
id: 254
title: Python 3 logging setup
date: 2018-06-05T09:28:16-04:00
author: Mehron Kugler
layout: post
guid: https://www.sunflowerdojo.com/?p=254
permalink: /2018/06/05/python-3-logging-setup/
categories:
  - Coding
tags:
  - python
---
Doing a few things here:

  1. Showing log output in the console
  2. Writing log output to a file
  3. Set logger level

`import logging<br />
LOG_FILE = "your_log_file.log"<br />
logger = logging.getLogger(__name__)<br />
# Set up console handler for logging<br />
ch = logging.StreamHandler()<br />
# Set up file handler for logging<br />
fh = logging.FileHandler(LOG_FILE)<br />
# Make the log messages look nice<br />
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')<br />
# Apply the formatter to console and file loggers<br />
ch.setFormatter(formatter)<br />
fh.setFormatter(formatter)<br />
logger.addHandler(ch)<br />
logger.addHandler(fh)<br />
# Catch all log messages of INFO or higher(debug, critical, etc)<br />
logger.setLevel(logging.INFO)<br />
# Also set the level of the logger itself<br />
# https://mail.python.org/pipermail/python-list/2010-March/572131.html<br />
from logging.getLogger().setLevel(logging.INFO)`

Then log messages like so:  
`logger.info("This is working now")<br />
logger.debug("A behind-the-scenes message")<br />
logger.warn("This post is getting too long")`