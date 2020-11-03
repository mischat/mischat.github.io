---
id: 40
title: Making FOAF useful ?
date: 2009-07-08T11:16:31+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=40
permalink: /blog/2009/07/08/making-foaf-useful/
itsec_enable_ssl:
  - "1"
categories:
  - FOAF
  - SemanticWeb
---
[FOAF files](http://www.foaf-project.org/) in isolation only give you information about a person, and who they know &#8211; i.e. who they claim to know in their FOAF file. 

At [Garlik](http://www.garlik.com/) we have implemented a [reverse search facility](http://foaf.qdos.com/reverse/) for FOAF, whereby given an API request one can get back triples containing a list of people who claim to know the FOAF URI/IFP used to generate the API request. This list of people is taken from our [knowledge base of harvested FOAF files,](http://foaf.qdos.com/) which currently holds around 10 millions individual FOAF files.

By including an API request to our reverse search in your FOAF file, you can have a FOAF file with both links out and links in<img src='https://mmt.me.uk/blog/wp-includes/images/smilies/icon_smile.gif' alt=':)' class='wp-smiley' /> Wow (he says)&#8230;

This API call &#8211; <http://foaf.qdos.com/reverse/?path=https://mmt.me.uk/blog/foaf.rdf%23mischa> &#8211; returns an RDF fragment listing foaf:People that claim to know me.

All you need to do is add one triple that requests RDF from our reverse search API to your FOAF file. The triple will look something like this: 

`<#me> rdfs:seeAlso <http://foaf.qdos.com/reverse/?path=http://foo.com/foaf.rdf%23me> .`

You can find examples of this API call in [Danbri&#8217;s](http://danbri.org/foaf.rdf), [Steve Harris&#8217;s,](http://plugin.org.uk/swh.xrdf) and [my](https://mmt.me.uk/blog/foaf.rdf) FOAF files.

There is some information regarding how to use the API on the [reverse search HTML page](http://foaf.qdos.com/reverse/).
