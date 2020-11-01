---
id: 297
title: ULIMIT
date: 2010-08-23T23:10:16+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=297
permalink: /?p=297
categories:
  - Uncategorized
---
Max number of files which can be open on a mac os x machine &#8230;

http://serverfault.com/questions/15564/where-are-the-default-ulimits-specified-on-os-x-10-5

unlimited  
jambi:~ mischatuffield$ history | grep ulimi  
198 ulimit -u  
199 man ulimit  
495 ulimit  
501 ulimit  
502 history | grep ulimi

THAT DIDN&#8217;T WORK, i.e. the /etc/launchd.conf thing wasn&#8217;t the right thing for this problem

moj: ulimit does sound right!  
[13:29] moj: \*tries to remember\*  
[13:29] moj: I did something similar for postgres  
[13:29] moj: AHo &#8211; in /etc/sysctl.conf you can tweak it I theenk  
[13:30] moj: Aha &#8211; and /etc/rc.common is where to put the ulimit  
[13:30] moj: http://www.macosxhints.com/article.php?story=200311151254441  
~