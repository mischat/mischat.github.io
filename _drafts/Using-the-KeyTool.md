---
id: 251
title: Using the KeyTool
date: 2010-08-20T17:03:23+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=251
permalink: /?p=251
categories:
  - Uncategorized
---
So I have had to play with some cypto technology recently, and thought I would share some  
of my finding.

I made use of the Java Keytool, to create a JKS keystore.

These are the commands I ended making us of :

Firstly I had to create a DSA key, so that I could pass the public key to a third party, so  
that they could verfiy digital signatures which I create:

keytool -genkey -alias lame -keyalg DSA -keystore lameDir/lame.keystore

At this point in time I had to fill out a bunch of credentially for the key.

Then if you want to output an ASCII armoured public key so that you can email the key to  
the third party so that they can verify signatures I generate, I used the following command:

keytool -export -alias lame -file lamecert.pem -keystore lameDir/lame.keystore -rfc

The next step involved me having to import the third party&#8217;s public key into my keystore,  
I did that in the following manner:

keytool -import -alias third_party -file lameDir/theirLameAsciiArmouredPublicKey.pem

This is the command which the ST people used:

openssl dgst -dss1 -verify DSAPublic.pem -signature signature.raw  
test_xml.txt

Converting from base64 to binary  
openssl dsa -in DSAPublic.pem -inform PEM -out DSA.der -outform DER -pubin

/usr/java/jre1.6.0_10/bin/keytool &#8211;import -trustcacerts -file keys/spublic.squaregaintest.co.uk.pem -alias selftrade -keystore cpp.trusted.jks