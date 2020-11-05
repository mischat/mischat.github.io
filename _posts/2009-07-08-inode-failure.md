---
id: 72
"comments: true"
title: Inode Failure
date: 2009-07-08T14:21:25+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=72
permalink: /blog/2009/07/08/inode-failure/
itsec_enable_ssl:
  - "1"
categories:
  - linux
tags:
  - :(
  - blog
  - linux
---
Hello All, 

I had one of my hard-drives fail miserably a couple of weeks ago, and have only now recovered all of my blog content from [Google&#8217;s](http://www.googleguide.com/cached_pages.html) and [Yahoo&#8217;s](http://help.yahoo.com/l/us/yahoo/search/basics/basics-09.html) caches. I have recreated all of the content, and have set up a cronjob to backup my sql tables, I had copies of most of the important stuff on my machine, and only lost my sql tables &#8230; d&#8217;oh&#8230;.

I have set the following 301 redirects from all of the old URLs, I don&#8217;t think I have missed any out. Do shout if you find any old broken URLs on my site.  
`<br />
redirect 301 /blog/2009/04/02/barcamp-09/ /blog/2009/07/07/barcamp-09/<br />
redirect 301 /blog/2009/03/24/time-machine-to-a-linux-box/ /blog/2009/07/07/timemachine-to-a-linux-box/<br />
redirect 301 /blog/2009/03/23/signing-a-public-key/ /blog/2009/07/08/signing-someone’s-public-key/<br />
redirect 301 /blog/2009/03/20/making-foaf-useful/ /blog/2009/07/08/making-foaf-useful/<br />
redirect 301 /blog/2009/03/19/yum_64bit_binaries/ /blog/2009/07/07/configuring-yum-to-only-install-64bit-binaries/<br />
redirect 301 /blog/2009/03/19/webdav_webid/ /blog/2009/07/08/enabling-a-writable-webid-with-webdav/<br />
redirect 301 /blog/2009/03/18/foafwot/ /blog/2009/07/08/enabling-trust-in-a-foaf-document/<br />
redirect 301 /blog/2009/03/17/signingverifyinggpg/ /blog/2009/07/08/signing-and-verifying-documents-using-gnupg/<br />
redirect 301 /blog/2009/02/05/ah-good-work-tobyink/ /blog/2009/07/07/ah-good-work-tobyink-…/<br />
redirect 301 /blog/2009/01/28/duplicate-dylib-libiconv2/ /blog/2009/07/07/duplicate-dylib-libiconv-2-dylib/<br />
redirect 301 /blog/2008/12/31/ld-duplicate-symbol-mac-osx/ /blog/2009/07/07/ld-duplicate-symbol-_g_bit_nth_lsf-mac-osx-leoparddarwin/<br />
`
