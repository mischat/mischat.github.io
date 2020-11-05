---
id: 94
"comments: true"
title: meh to owl:equivalentClass
date: 2009-08-10T18:26:53+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=94
permalink: /blog/2009/08/10/meh-to-owlequivalentclass/
itsec_enable_ssl:
  - "1"
categories:
  - SemanticWeb
---
Meh, 

So we now have more links from dbpedia to other RDF resources on the web. Dbpedia now links from dbpedia classes to freebase ones, [this example SPARQL query gives some examples of the described linkage](http://dbpedia.org/sparql?default-graph-uri=&query=select+distinct+*+from+%3Chttp%3A%2F%2Fdbpedia.org%2Ffreebase_type_links%23%3E+where+%7B%3Fs+%3Fp+%3Fo%7D+limit+10&format=text%2Fhtml&debug=on&timeout=). None of these make any sense to me. Why have people decided to use owl:equivalentClass and not owl:sameAs (ducks behind computer screen). Neither of the two seem correct to me, am guessing there is a [skos:broader](http://www.w3.org/TR/2008/WD-skos-reference-20080609/#broader) relationship (or something similar) which would be more appropriate, but at least we have come to accept that owl:sameAs tends to get abused, do we really need to loose faith in the semantics of the other OWL classes. Does anyone know why dbpedia decided to go this way?

The [OWL spec](http://www.w3.org/TR/owl-ref/) defines owl:equivalentClass to be : 

"A class axiom may contain (multiple) owl:equivalentClass statements. owl:equivalentClass is a built-in property that links a class description to another class description. The meaning of such a class axiom is that the two class descriptions involved have the same class extension (i.e., both class extensions contain exactly the same set of individuals)."

I really don't think these links are suitable for the knowledge at hand. Perhaps even rdfs:subClassOf would be more fitting.
