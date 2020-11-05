---
id: 32
comments: true
title: Ah, good work tobyink …
date: 2009-07-07T18:24:25+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=32
permalink: '/blog/2009/07/07/ah-good-work-tobyink-%e2%80%a6/'
itsec_enable_ssl:
  - "1"
categories:
  - SemanticWeb
---
I have just read [tobyink&#8217;s](mail@tobyinkster.co.uk) article on [how one could cater for 3rd parties wanting to contribute triples to an RDF file you own](http://buzzword.org.uk/2009/posted-data/spec). Firstly, great stuff, this follows on from some things I have been thinking about recently, which include, that of how best to inform RDF documents of when they have been mentioned elsewhere.

[tobyink](http://tobyinkster.co.uk/) and various other people have been talking about such things recently you can find them of the <irc://irc.freenode.net/swig> [chatlogs here](http://chatlogs.planetrdf.com/swig/2009-02-04#T16-16-11) (thanks phenny&#8230;). I first started thinking about this when I read [this email](http://lists.foaf-project.org/pipermail/foaf-protocols/2008-December/000117.html) and when I was thinking about how technologies like [linkback, inc. trackback and pingback](http://en.wikipedia.org/wiki/Linkback) changed blogging for the better. 

I like tobyink&#8217;s approach, but I think I would prefer to use a [SPARQL endpoint](http://esw.w3.org/topic/SparqlEndpointDescription) for updating any [RDF](http://www.w3.org/RDF/) I own. And I would definitely protected this behind some sort of security mechanism, from .htaccess rules to techniques such as [OAuth](http://oauth.net/) or [FOAF+SSL](http://blogs.sun.com/bblfish/entry/foaf_ssl_creating_a_global) or similar, I would stress that I would be very careful who I allowed access to any data I owned.

I guess I come from a world of triple-stores, and do enjoy being able to SPARQL quads efficiently as apposed to coming to this from a linked data standpoint. In [JXT](http://esw.w3.org/topic/LargeTripleStores) the SPARQL Endpoint implements a HTTP DELETE and HTTP PUT to allow for graph&#8217;s to be updated in the quad store. Give the following SPARQL endpoint :

`http://example.com/sparql`

We would delete a graph like so :

`'curl -X DELETE http://example.com/sparql/https://mmt.me.uk/blog/foaf.rdf'`

and similarly for adding triples we use PUT to add triples into the quad store, in the form of a string of RDF and its graph URI. There is work underway to get a [SPARUL](http://jena.hpl.hp.com/~afs/SPARQL-Update.html) implementation working so that we can update individual triples in future quad stores.

I was more envisaging the mechanism that would pingback to my FOAF file (or any RDF document I own) as soon as it has been used elsewhere. So for example if Alice befriends Bob, in the form of I know this chap with some URI, then the Alice should somehow ping Bob, like bloggers do, with a simple request, something like what tobyink describes in the [section 2.2 POST](http://buzzword.org.uk/2009/posted-data/spec#ssec-behaviour-POST) of the aforementioned post. I would definately not let other people add triples to my [FOAF file](http://xmlns.com/foaf/spec/), and would rather have the triple which mentioned my FOAF URI and have the graph URI where the statement was made, so that I can decide on any future action I may take. If Alice doesn&#8217;t know Bob&#8217;s FOAF URI, but knows another identifier for him, they could always use a service like the [QDOS FOAF search](http://foaf.qdos.com/) to find a URI for Bob before befriending him.

So something like [2.2](http://buzzword.org.uk/2009/posted-data/spec#ssec-behaviour-POST) sounds good, but I would prefer if they simply sent me the triple(s) authored that mentioned me, along with the graph URI, than triples they would like to insert into one of my graphs.

I understand how the approach tobyink mentions could be beneficial in a linked data world, and do kind of like the idea of have some sort of &#8220;RDF scrap book&#8221; which my FOAF friends could write to, but I still think I prefer to not let anyone but me author triples on my domain. If I where to implement an &#8220;RDF scrap book&#8221; which my foaf:friends could add triples to, whatever they may be ? [dbtune scrobbles](http://dbtune.org/last-fm/MischaTuffield), their [dbpedia](http://dbpedia.org/resource/Drum) interests, I would much rather that information be hosted on one of their sites, which in turn I would store in my quad store for future SPARQL goodness.

Finally, tobyink, why did you decide to use `charset="us-ascii"` ?
