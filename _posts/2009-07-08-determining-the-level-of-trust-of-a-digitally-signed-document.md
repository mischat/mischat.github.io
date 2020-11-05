---
id: 77
"comments: true"
title: Determining the Level of Trust of a Digitally Signed Document
date: 2009-07-08T17:38:37+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=77
permalink: /blog/2009/07/08/determining-the-level-of-trust-of-a-digitally-signed-document/
itsec_enable_ssl:
  - "1"
categories:
  - linux
  - SemanticWeb
---
In order to determine how trustworthy a digital signature of a file is, you need to grab the file, the digital signature, and you will need to import the user&#8217;s public key. [This wikipedia fragment](http://en.wikipedia.org/wiki/Pretty_Good_Privacy#Web_of_trust) describes what is meant by a &#8220;trustworthy signature&#8221; in terms of the Web of Trust.

This is the command I run to determine the level of trust of my signed foaf file.  
`<br />
gpg --verify --no-tty --status-fd 2 --command-fd 0 foaf.rdf.asc foaf.rdf<br />
` 

Which results in the folowing output :  
`<br />
gpg: Signature made Wed  3 Jun 23:19:52 2009 BST using RSA key ID 51F2F7EF<br />
[GNUPG:] SIG_ID foL1PiWCT+546VnE17UG2QvWJeE 2009-06-03 1244067592<br />
[GNUPG:] GOODSIG 9ED0B04E51F2F7EF Mischa Tuffield (Mischa@Garlik) <mischa.tuffield@garlik.com><br />
gpg: Good signature from "Mischa Tuffield (Mischa@Garlik) <mischa.tuffield@garlik.com>"<br />
gpg:                 aka "Mischa Tuffield (http://id.ecs.soton.ac.uk/person/6914) <mmt04r@ecs.soton.ac.uk>"<br />
[GNUPG:] VALIDSIG 18A2AF280CA59E77AE512BB39ED0B04E51F2F7EF 2009-06-03 1244067592 0 4 0 1 2 00 18A2AF280CA59E77AE512BB39ED0B04E51F2F7EF<br />
[GNUPG:] TRUST_ULTIMATE<br />
` 

This is an automatic way of evaluating how trust worthy statement at the end of a URI are.
