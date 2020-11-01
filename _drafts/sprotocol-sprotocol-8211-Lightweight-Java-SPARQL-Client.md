---
id: 566
title: 'sprotocol &#8211; Lightweight Java SPARQL Client'
date: 2011-12-30T14:50:55+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=566
permalink: /?p=566
categories:
  - SemanticWeb
---
This is a blog post about sprotocol, a lightweight Java SPARQL client library. 

You can find it on [github](https://github.com/mischat/sprotocol), it is open-sourced, and it comes with NO Dependencies. I have come to love Java as a language, but one thing which is most annoying about it as a language is how it handles dependencies. 

I designed and built (with help from Luke Wilson-Mawer and Cezary Biernacki) sprotocol with a goal of creating an easy to use SPARQL client, which comes with NO dependencies outside the standard Java libraries. 

Sprotocol can be downloaded from github, it is a tiny package. And example code looks like so: 

[sprotocol](https://github.com/mischat/sprotocol) is a standalone, lightweight Java SPARQL client library. sprotocol is open-source, it is released under the [Apache License v2](), and it was written by myself, with help from Luke Wilson-Mawer, and Cezary Biernacki.

At this point in time you may be asking yourself &#8220;Why do we need yet another SPARQL implementation?&#8221;, which is a totally fair question, that is for sure. sprotocol is lightweight, it has no dependencies outside of Java&#8217;s core libraries, and it is a standalone SPARQL protocol library. If you are thinking of building an application in Java, where you system will end up talking to a SPARQL store, you can use sprotocol to both query and to update the contents of your store.

You can download the [latest version of sprotocol]() from github. If you require a full blown RDF parser, generator, or a SPARQL implementation, sprotocol is not the thing for you &#8211; check out other tools such as Jena, Sesame, Fuseki, or 4store.

When interacting with sprotocol