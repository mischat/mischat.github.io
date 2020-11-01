---
id: 78
title: Determine the Level of Trust of a Signed Document
date: 2009-07-08T17:36:35+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2009/07/08/77-revision/
permalink: /2009/07/08/77-revision-v1/
---
In order to determine how trustworthy a digital signature of a file is, you need to grab the file, the digital signature, and you will need to import the user&#8217;s public key. [This wikipedia fragment](http://en.wikipedia.org/wiki/Pretty_Good_Privacy#Web_of_trust) describes what is meant by a &#8220;trustworthy signature&#8221; in terms of the Web of Trust.

This is the command I run to determine the level of trust of my signed foaf file.  
`<br />
gpg --verify --no-tty --status-fd 2 --command-fd 0 foaf.rdf.asc foaf.rdf<br />
` 

Whic