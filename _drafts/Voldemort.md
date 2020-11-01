---
id: 503
title: Voldemort
date: 2011-11-07T13:50:03+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=503
permalink: /?p=503
categories:
  - Uncategorized
---
We need to put each of the segments on each disk

Need to make sure that the perl libraries I am using attempts keep-alive 

The java code supplied does 30-40k requests/sec

Check the replication factoro

In voldemort teminology &#8220;vector clocks&#8221; are used to sync replication, especially over a clustered network &#8230;

RE: Test 1 of voldemort: 

There was no increase in file IO when running up to a 1M iterations of PUT to voldemort.

AHH: 

In http://search.cpan.org/~exussum/Voldemort-0.11/lib/Voldemort.pm#\___top

^^ They talk about the &#8220;version&#8221; numbers of the values of a give key. This is used so that the client can decide what the correct value is. This should be used when you attach multiple clients to the server.