---
id: 301
title: What is linked Data
date: 2010-08-23T23:11:01+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=301
permalink: /?p=301
categories:
  - Uncategorized
---
The context is purely in discussion format; when I&#8217;m talking about  
&#8220;Linked Data&#8221; &#8211; if I first explain it to mean &#8220;linked data&#8221;; then talk  
about it being made public as &#8220;linked open data&#8221; (leaving the  
private/public what to publish bit out of it) then to what do I refer to  
the overall tech-stack as? everything that comes with it eg:

&#8211; Linked Data, RDF, SPARQL, REST, Quad-Stores, REST, Ontologies, OWL2,  
EAV/CR, FOAF+SSL, HTTP, URIs etc

A name for the above as a whole.

Many Regards,

\___\___

Linked data is a set of best practices for publishing and deploying instance and class data using the RDF data model. Two of the best practices are to name the data objects using uniform resource identifiers (URIs), and to expose the data for access via the HTTP protocol. Both of these practices enable the Web to become a distributed database, which also means that Web architectures can also be readily employed.

It is not an end in itself, a manifesto for &#8220;open data&#8221;, or a substitute for the semantic Web. ¬†It is a useful and recommended practice (technique), but nothing more [1]. 😉

<blockquote class="wp-embedded-content" data-secret="Mxjs1w7Yka">
  <p>
    <a href="https://www.mkbergman.com/802/moving-beyond-linked-data/">Moving Beyond Linked Data</a>
  </p>
</blockquote>



\___\_____

For a definition of Linked Data I&#8217;d suggest anything that conforms to  
timbl&#8217;s Linked Data expectations:

¬†¬†1. Use URIs as names for things  
¬†¬†2. Use HTTP URIs so that people can look up those names.  
¬†¬†3. When someone looks up a URI, provide useful information, using  
the standards (RDF, SPARQL)  
¬†¬†4. Include links to other URIs. so that they can discover more things.

While Tim only lists RDF & SPARQL as the standards, pragmatically I  
reckon there&#8217;s a bit of leeway here, e.g. a HTML document or Atom feed  
is likely to contain links and data that can be interpreted as RDF &#8211;  
in fact \*any\* hyperlink could be seen as an RDF statement (maybe  
<docA> dc:relation <docB>), so depending on the context a looser  
definition of linked data as &#8220;linky stuff&#8221; doesn&#8217;t seem unreasonable.  
http://www.w3.org/DesignIssues/LinkedData.html  
Cheers,  
Danny.

🙂 Even better!

Creating a Web of Linked Data  
&#8211; Linked Data  
&#8211; The Web of Linked Data  
&#8211; Linked Data Technologies  
&#8211; etc