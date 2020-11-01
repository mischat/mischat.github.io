---
id: 53
title: Enabling Trust in a FOAF Document
date: 2009-07-08T12:13:15+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=53
permalink: /2009/07/08/enabling-trust-in-a-foaf-document/
itsec_enable_ssl:
  - "1"
categories:
  - FOAF
  - SemanticWeb
---
This blog post follows on from my previous one <A HREF="https://mmt.me.uk/blog/2009/03/17/signingverifyinggpg/">signing and verifying files with GnuPG</a>, whereby I showed (he says), in its simplest form, how one can digitally sign and verify a document. This in turn allows anyone reading the document to verify whether or not it has been tampered with since it was signed.

In this post I will describe two methods of linking to a digital signature from a <A HREF="http://www.w3.org/RDF/">RDF</a> document. The RDF document I will be describing in this post is a <A HREF="http://www.foaf-project.org">FOAF</a> document, but is is needless to say that this approach can be used from any RDF file.

The method described below makes use of the <A HREF="http://xmlns.com/wot/0.1/">Web of Trust ontology (WOT)</a>. WOT allows for RDF documents to be signed using <A HREF="http://en.wikipedia.org/wiki/Digital_signature">Digital Signatures</a> and <A HREF="http://en.wikipedia.org/wiki/Public-key_cryptography">Public Key Cryptography</a>.

Whilst putting together the <A HREF="http://foaf.qdos.com/validator/">foaf validator</a>, which checks the semantics of a RDF document to ensure that it is a well formed <A HREF="http://xmlns.com/foaf/0.1/PersonalProfileDocument">foaf:PersonalProfileDocument</a>, I came across these two different methods of using the Web of Trust ontology.

**Linking to an armored digital signature using the WOT ontology from your FOAF file:**

_Step 0: Declare the wot namespace in the FOAF file_

`<BR><br />
@prefix wot: <http://xmlns.com/wot/0.1/> .<BR><br />
` 

_Step 1_

Add a triple from the Document pointing to the digital signature like so:

`<BR><br />
 <> wot:assurance <http://foo.com/foaf.rdf.asc> .<BR><br />
` 

_Step 2_

Add a triples associating the public key used to sign the FOAF document to the FOAF person. This can be done in one of two ways, like so:

**Style 1**

`<BR><br />
_:bnode0 a <http://xmlns.com/wot/0.1/PubKey> .<br />
_:bnode0 dc:title &#8220;Public Key Bnode&#8221; .<br />
_:bnode0 wot:fingerprint &#8220;FW89F7WF78SD8F7SD7FG21JL213192&#8221; .<br />
_:bnode0 wot:hex_id &#8220;12A75E9B&#8221; .<br />
_:bnode0 wot:identity <#me> .<br />
_:bnode0 wot:pubkeyAddress <http://foo.com/me.pubkey.asc> <br />
` 

This is how I sign [my FOAF file](https://mmt.me.uk/blog/foaf.rdf)

**Style 2**

`<BR><br />
<#me>  wot:hasKey _:bnode0 .<br />
_:bnode0 a <http://xmlns.com/wot/0.1/PubKey> .<br />
_:bnode0 wot:pubkeyAddress <http://foo.com/me.pubkey.asc> <br />
_:bnode0 dc:title &#8220;Public Key Bnode&#8221; .<br />
_:bnode0 wot:fingerprint &#8220;FW89F7WF78SD8F7SD7FG21JL213192&#8221; .<br />
_:bnode0 wot:hex_id &#8220;12A75E9B&#8221; .<br />
` 

This is how Kjetil signs [his FOAF file](http://www.kjetil.kjernsmo.net/foaf.rdf)

These two methods of associating a publicKey to a FOAF WebID, which is in turn can be used to digitally sign a FOAF file are both supported by [Garlik&#8217;s FOAF validator](http://foaf.qdos.com/validator/).