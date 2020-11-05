---
id: 50
comments: true
title: Enabling a Writable WebID with WebDAV
date: 2009-07-08T11:45:49+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=50
permalink: /blog/2009/07/08/enabling-a-writable-webid-with-webdav/
itsec_enable_ssl:
  - "1"
categories:
  - FOAF
  - SemanticWeb
---
In this post I will describe how you can enable write access to a file, specially a <A HREF="http://www.w3.org/RDF/">RDF</a> one, via <A HREF="http://httpd.apache.org/">Apache’s HTTP server</a> and the <A HREF="http://en.wikipedia.org/wiki/WebDAV">Web Distributed Authoring and Versioning protocol (WebDAV)</a> extension to the <A HREF="http://www.w3.org/Protocols/">HTTP protocol</a>. 

_So, why would you want to do this?_ 

I use WebDAV on <A HREF="https://mmt.me.uk/blog/foaf.rdf#mischa">my</a> <A HREF="http://www.foaf-project.org/">FOAF</a> file to enable write access via <A HREF="http://www.w3.org/People/Berners-Lee/card#i">Tim Berners-Lee’s</a> <A HREF="http://www.w3.org/2005/ajar/tab.html">Tabulator</a> and <A HREF="http://foafbuilder.qdos.com/">Garlik’s foafbuilder</a>. This technology allows me to write updates straight through the HTTP protocol, so that I don’t have to save the file to my local machine, and <A HREF="http://en.wikipedia.org/wiki/Scp">scp</a> it over. 

These are the configuration settings needed in your `httpd.conf` file:

**Setting up WebDAV on a whole directory:**

`<BR><br />
<VirtualHost *:80><BR><br />
 ServerName   www.foo.com<BR><br />
 ServerAlias   foo.com<BR><br />
 Alias / /var/www/foo/public_html/<BR><br />
 <Location /><BR><br />
  DAV On<BR><br />
  AuthType Basic<BR><br />
  AuthName &#8220;webdav&#8221;<BR><br />
  Header set MS-Author-Via DAV<BR><br />
  AuthUserFile /var/www/foo/passwd.dav<BR><br />
  <LimitExcept GET HEAD OPTIONS POST><BR><br />
   Require user bar<BR><br />
  </LimitExcept><BR><br />
 </Location><BR><br />
</VirtualHost><BR><br />
` 

**Enabling WebDAV for all files ending in .rdf:**  
  
`<BR><br />
<VirtualHost *:80><BR><br />
 ServerName   www.foo.com<BR><br />
 ServerAlias   foo.com<BR><br />
 Alias / /var/www/foo/public_html/<BR><br />
 <Files ~ &#8220;.*\.rdf&#8221;><BR><br />
  DAV On<BR><br />
  AuthType Basic<BR><br />
  AuthName &#8220;webdav&#8221;<BR><br />
  AuthUserFile /var/www/foo/passwd.dav<BR><br />
  Header set MS-Author-Via DAV<BR><br />
  ForceType application/rdf+xml<BR><br />
  <LimitExcept GET HEAD OPTIONS POST><BR><br />
   Require user bar<BR><br />
  </LimitExcept><BR><br />
 </Files><BR><br />
</VirtualHost><BR><br />
` 

_It should be noted that the methods presented above allow for the files to be read normally via HTTP, as well as catering for writing via WebDAV.  
  
_ 

**WebDAV related HTTP Headers:** 

The correct HTTP header used to tell a client that a file is WebDAV enabled is: 

`MS-Author-via: DAV`

Some of this information was taken from the <A HREF="http://esw.w3.org/topic/EditingData">ESW wiki’s article “EditingData”</a>, and I should thank everyone who helped put it together.
