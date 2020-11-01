---
id: 26
title: Configuring Yum to only install 64bit binaries
date: 2009-07-07T18:12:27+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2009/07/07/24-revision-2/
permalink: /2009/07/07/24-revision-v1/
---
This post follows the fact that I noticed that some of my [64bit](http://en.wikipedia.org/w
iki/X86-64) development machines had 32bit binaries installed on them. It should be noted that this is not fatal in any sense of the word, but it is simply not ideal. 

Here I will present how you can first identify what your machine&#8217;s architecture is, and then I will show how you can b  
oth remove existing 32bit binaries, and how you can configure [YUM](http://yum.baseurl.org/) so that it will only ev  
er install 64bit software.

This blog post is only relevant if your linux box uses YUM as a package manager. 

**Identifying your machine&#8217;s architecture**

In order to find out what your machine&#8217;s architecture is you need to execute the following command from your command line: 

`uname -a` 

If the result looks something like below, it means you have a 64bit machine, where the x86_64 implies the machine is 64bit.  
If it had any of i386, i586, or i686, it would imply that the machine was a 32bit one.

`Linux foo.bar.com 2.6.18-92.el5 #1 SMP Tue Jun 10 18:51:06 EDT 2008 x86_64 x86_64 x86_64 GNU/Linux`

**Remove all 32bit binaries :** 

`yum erase *.i386<br />
yum erase *.i586<br />
yum erase *.i686<br />
` 

**Tell YUM to never install 32bit binaries again:** 

You need to add the below line to your `yum.conf` file (usually found in /etc/) :

`exclude=*.i386 *.i586 *.i686`

At this point, all future software install via the YUM package manager will be optimised for your machine&#8217;s architecture.