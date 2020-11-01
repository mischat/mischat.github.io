---
id: 275
title: FOAF SSL
date: 2010-08-23T23:01:31+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=275
permalink: /?p=275
categories:
  - Uncategorized
---
[[  
Grab the next OpenJDK build, and run

keytool -keystore x.jks -storepass chageit -keypass changeit -genkeypair  
-alias me -dname CN=Me -ext san=uri:http://romeo.net/#romeo

The entry generated would have a cert like this (in your familiar  
openssl x509 -text output):

Certificate:  
¬†Data:  
¬†¬†¬†¬†¬†Version: 3 (0x2)  
¬†¬†¬†¬†¬†Serial Number: 1235619180 (0x49a60d6c)  
¬†¬†¬†¬†¬†Signature Algorithm: dsaWithSHA1  
¬†¬†¬†¬†¬†Issuer: CN=Me  
¬†¬†¬†¬†¬†Validity  
¬†¬†¬†¬†¬†¬†¬†¬†¬†Not Before: Feb 26 03:33:00 2009 GMT  
¬†¬†¬†¬†¬†¬†¬†¬†¬†Not After : May 27 03:33:00 2009 GMT  
¬†¬†¬†¬†¬†Subject: CN=Me  
¬†¬†¬†¬†¬†Subject Public Key Info:  
¬†¬†¬†¬†¬†¬†¬†¬†¬†&#8230;.  
¬†¬†¬†¬†¬†X509v3 extensions:  
¬†¬†¬†¬†¬†¬†¬†¬†¬†X509v3 Subject Key Identifier:  
¬†¬†¬†¬†¬†¬†¬†¬†¬†¬†¬†¬†¬†DD:BF:CE:42:A5:BB:E3:DA:37:6E:C7:4F:4A:A1:3C:4D:47:FA:EC:44  
¬†¬†¬†¬†¬†¬†¬†¬†¬†X509v3 Subject Alternative Name:  
¬†¬†¬†¬†¬†¬†¬†¬†¬†¬†¬†¬†¬†URI:http://romeo.net/#romeo  
¬†Signature Algorithm: dsaWithSHA1  
¬†¬†¬†¬†¬†&#8230;.  
]]

He then pointed out the following

[[  
Since JDK 6, keytool has a command -importkeystore which converts a  
keystore from one storetype to another. Using this command, you can  
convert a JKS keystore into a PKCS12 one. Then, I believe you will know  
how to play with the private key inside it. 🙂

Read the tooldoc for details:  
http://java.sun.com/javase/6/docs/technotes/tools/solaris/keytool.html  
]]

Alternatively, you can use environment variables in openssl.cnf:

subjectAltName=$ENV::ALTNAME

Then:  
OPENSSL_CONF=/path/to/openssl.cnf/if/not/default  
ALTNAME=&#8221;URI:http://example.com/joe#me&#8221; openssl req &#8230;

(See http://www.crsr.net/Notes/SSL.html for examples)

Best wishes,

Bruno.

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

Perhaps I should get my self a foaf+ssl cert : 

http://www.mementoweb.org/demo/

http://foaf.me?webid=