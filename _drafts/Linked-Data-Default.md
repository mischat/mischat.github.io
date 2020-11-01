---
id: 284
title: Linked Data Default
date: 2010-08-23T23:04:53+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=284
permalink: /?p=284
categories:
  - Uncategorized
---
I need to mention how I failed to find a movie which I wanted to watch. This was an issue, for the data didn&#8217;t have any of rating based information in it 🙁 Which kinda sucked: 

Need to fix the pastebin

curl -i &#8216;http://data.linkedmdb.org/sparql?query=select+*+where+%7B%3Chttp%3A%2F%2Fdata.linkedmdb.org%2Fdata%2Ffilm%2F122%3E+%3Fp+%3Fo%7D&#8217;

http://pastebin.com/pHgUupsv

jambi:~ mischatuffield$ curl -i &#8216;http://data.linkedmdb.org/sparql?query=select+*+where+%7B%3Chttp%3A%2F%2Fdata.linkedmdb.org%2Fdata%2Ffilm%2F122%3E+%3Fp+%3Fo%7D&#8217;  
HTTP/1.1 200 OK  
Date: Fri, 02 Apr 2010 19:25:56 GMT  
Server: Jetty(6.1.4)  
Cache-Control: no-cache  
Pragma: no-cache  
X-Joseki-Server: Joseki-3.0-dev  
Content-Type: application/sparql-results+xml  
Via: 1.1 data.linkedmdb.org  
Transfer-Encoding: chunked  
X-Pad: avoid browser bug

<?xml version="1.0"?>

  
<sparql xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#" xmlns:xs="http://www.w3.org/2001/XMLSchema#" xmlns="http://www.w3.org/2005/sparql-results#" >  
  
<results>  
</results>  
</sparql>  
jambi:~ mischatuffield$ curl -i &#8216;http://data.linkedmdb.org/sparql?query=select+*+where+%7B%3Chttp%3A%2F%2Fdata.linkedmdb.org%2Fdata%2Ffilm%2F122%3E+%3Fp+%3Fo%7D&#8217;

This would have been linked data working in action for me if it actually worked !?!?!?

Should blog about how this failed, adn how it sucked : 

http://pastebin.com/pHgUupsv