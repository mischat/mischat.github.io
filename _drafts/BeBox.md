---
id: 289
title: BeBox
date: 2010-08-23T23:07:44+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=289
permalink: /?p=289
categories:
  - Uncategorized
---
HOME TECH NOTES:  
\___\___\___\___\___\_____  
Router Config

ip config natloopback=enabled

assign name=&#8221;Secure Web Server (HTTPS)&#8221; host=192.168.1.2 log=disabled

service system ifdelete name=TELNET group=wan  
{Administrator}=>saveall  
~