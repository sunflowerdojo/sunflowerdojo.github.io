---
id: 332
title: Using Git-LFS to upload big files to Github
date: 2018-10-02T16:42:51-04:00
author: Mehron Kugler
layout: post
guid: https://www.sunflowerdojo.com/?p=332
permalink: /2018/10/02/using-git-lfs-to-upload-big-files-to-github/
categories:
  - Coding
---
I had a side project to help update a department's website. The design agency they contracted with delivered the site in PHP and the method of updating the site was uploading new content via FTP.

The first thing I did was fetch the content off the server and commit to a local git repo to preserve its current state. But I couldn't push the content up to Github because of large PDF files over 50 MB and up to 250 MB in size. Although the 90s and Web 1.5 are back, there are 21st century tools to help: Git LFS.

<!--more-->

## About Git LFS

Git LFS is a supplemental Git utility that breaks up large files behind the scenes so that they can be uploaded to Github within file size limits (50 MB). It needs to be installed separately, after git.

Following the instructions at https://packagecloud.io/github/git-lfs/install (Linux version shown here)

  1. <pre>curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash</pre>

  2. <pre>sudo apt-get install git-lfs</pre>

  3. Head over to the repo with large files and declare the large files pattern from the instructions here: https://github.com/git-lfs/git-lfs#example-usage
  4. I ran into a problem at the step where I push the repo back up to Github after marking large files and setting up git-lfs: "<a href="https://github.com/git-lfs/git-lfs/issues/2533" target="_blank" rel="noopener">x509 signed by unknown authority</a>"
    <li style="list-style-type: none;">
      <ol>
        <li>
          To resolve this, disable ssl verification for the specific site (awful workaround): <pre>$ git config http.https://git.sample.com.sslVerify false</pre>
        </li>
      </ol>
    </li>

  5. Push the code to the repository, it should work now.
