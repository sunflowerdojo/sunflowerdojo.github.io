---
title: Build Windows executable from Python 3.6 package
date: 2018-09-24T22:26:03-04:00
author: Mehron Kugler
layout: post
categories:
  - Coding
tags:
  - python
---
I have been working on a project in which I need to deploy to multiple Windows systems. I've written the software in Python; normally, I would clone the package repo via git to the target systems, and set up package dependencies by installing via internet, but I have some restrictions:

  * Firewalled systems can't pull in OS-specific package dependencies
  * Firewalled systems can't access the code repository

Which means:

  * Making changes to deployed code means hand-editing, which does not scale
  * I can copy over the entire local code repo which has cached packages for installation, but that does not scale either

So my goal is to create a single executable file which I can distribute to the target systems. I think that is the simplest, most scaleable solution.

<a href="https://cygwin.com/" target="_blank" rel="noopener">I'm developing in a Cygwin environment</a>, which is neither Linux nor Windows but somewhere inbetween. It is a system of POSIX-like packages that are installed on Windows and are run in a separate environment. I use it because of its similarity in feel to Linux.

My method will be to <a href="https://www.pyinstaller.org/index.html" target="_blank" rel="noopener">use pyinstaller to create distributable executables</a>. I can't build for Windows from Cygwin, so I do the following:

  * Install Python 3.6 for Windows (assuming I hadn't before)
  * From a Windows command shell, make "virtualenv" available to the system with
      * python -m pip install virtualenv
  * Create a Windows-compatible virtual Python environment (3.6) in my Python package folder. Virtual environments create portable, self-contained instances of the Python interpreter and dependent packages are installed in that scope
      * virtualenv package\_base\_folder
      * Specify a version if multiple are installed: virtualenv &#8211;python=python3.6 package\_base\_folder
  * Change directory into the package folder, and activate the virtual environment with
      * .\Scripts\activate

At this point, the system should look to the package\_base\_folder\Scripts path for the Python interpreter executable file. Dependencies installed via pip are accessible to the virtual environment's version of Python. If for some reason the "activate" script failed, I can still use Python in the virtual environment by referring to its path:

  * .\Scripts\python.exe -m pip list

I continue:

  * Install my Python software's requirements like so
      * .\Scripts\python.exe -m pip install -r requirements.txt
      * <a href="https://pip.readthedocs.io/en/1.1/requirements.html" target="_blank" rel="noopener">Assuming I have a requirements file set up</a>
  * Install "pyinstaller" which will analyze the Python file that I want to convert to Windows executable
      * .\Scripts\python.exe -m pip install pyinstaller
  * Run the installer on my main Python script
      * .\Scripts\pyinstaller.exe module\_folder\my\_python_file.py

At this point pyinstaller produces a LOT of console output, most of it is informational and for debugging purposes. It creates a distributable executable in module_folder\dist. Then I can pass around this executable to the other systems that I want to run it on.

Of course, a good developer tests to make sure everything works as expected, and that there are no OS-specific errors present in Windows that aren't present in other systems!
