---
id: 45
title: Signing and Verifying documents using GnuPG
date: 2009-07-08T11:19:06+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2009/07/08/43-revision-2/
permalink: /2009/07/08/43-revision-v1/
---
In this post I will describe how to both sign and in turn verify the validity of a document. Below describes how one could use the open-source [GnuPG](http://www.gnupg.org/) implementation of the OpenPGP standard as defined by [RFC4880](http://www.ietf.org/rfc/rfc4880.txt) as a mechanism of trust. You can find out more information here at [the PGP faq at pgp.net](http://www.pgp.net/pgpnet/pgp-faq/).

_So, why would you ever want to sign a document using the OpenPGP standard?_

One can sign a file using the OpenPGP standard before putting it in the public domain so that if and when another person/agent views the file they can check whether or not the file has been tampered with on route. This method of signing files provides the creator of a document with an ability to sign their work, which in turn allows the reader to know whether or not the file has been altered since being signed.

In essence every user has a public and a private key, and when a GnuPG user wants to sign a file they end-up creating a checksum of whole file using their keys. This checksum can then be used to verify that a document has not been tampered with, this is done by the GnuPG software comparing the checksum, the file in question, and the user&#8217;s public key. 

**Step 0**

After creating your gpg keys you have to ensure that you have pushed your public key to one of the public keyservers, you can do this like so: 

`gpg --keyserver pgp.mit.edu --send-keys YOUR-EMAIL-ADDRESS`

Make sure that your private key is private, and that it is not accessible by any of the other users setup on your machine. You can do this by : 

`chmod 600 ~/.gnupg/YOURPRIVATEKEY.asc`

Make sure this is safe, for this is the only file someone needs to pretend to be you. 

**Signing a file using GnuPG**

In this example the file which we are signing is called foaf.rdf. After setting up your gpg keys you can sign the file like so : 

`gpg -a --detach-sign foaf.rdf`

This creates a file called foaf.rdf.asc (ASCII-armored digital signature) in the directory where the command was executed. 

**Checking a file against it&#8217;s ASCII-armored digital signature**

If you have both the original file and the ASCII-armored digital signature of the file in the current working directory you can verify the files integrity by execting the following command : 

`gpg --verify`

The output this last command will notify the user to whether or not the file has been altered since the last time it was signed.