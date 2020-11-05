---
id: 15
"comments: true"
title: duplicate dylib libiconv.2.dylib
date: 2009-07-07T17:29:27+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=15
permalink: /blog/2009/07/07/duplicate-dylib-libiconv-2-dylib/
openid_comments:
  - 'a:1:{i:0;s:4:"1845";}'
itsec_enable_ssl:
  - "1"
categories:
  - OSX
tags:
  - duplicate
  - dylib
  - iconv
  - mac
  - OSX
---
When building from source on Mac OSX, I have regularly come across the problem whereby the compiler complains about _duplicate dylib_s.

`duplicate dylib libiconv.2.dylib`

This is due to my use of the [Fink](http://www.finkproject.org/) and [Darwin](http://darwinports.com/) packages to install various bits I need for OSX development.

I recently noticed that many configure scripts cater for the user to select which [dylib](http://www.kernelthread.com/mac/osx/programming.html) they would like to include. So I figured that my problem of duplicate iconv&#8217;s can be overcome by looking for options like :

`--with-iconv=`

So look out for similar parameters in configure scripts

 `./configure --with-iconv=/opt/local/..`

So, why do I not just remove all but one instance of iconv? Well, Leopard ships with an old version of iconv, and I require recent versions for my development work.
