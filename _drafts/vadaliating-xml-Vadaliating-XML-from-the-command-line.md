---
id: 127
title: Vadaliating XML from the command line
date: 2009-11-20T11:25:50+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=127
permalink: /?p=127
categories:
  - Uncategorized
---
Given that I am so sad that I can read RDF/XML and I can parse the triples in my head, and I am well versed in using RDF based tools, I have had to play with some actual XML. And found it a tad hard to find any information about how would one go about processing XML, from a nix command prompt.

So, after poking around for a bit, I found the xmllint program to be the most useful/helpful command line tool for processing XML

`<br />
xmllint --schema someLameSchema.xsd someEvenLamerXMLFile.xml<br />
` 

Will validate an XML fragment against it&#8217;s schema