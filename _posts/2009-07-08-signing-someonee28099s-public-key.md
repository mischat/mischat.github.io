---
id: 46
title: Signing someone’s public key
date: 2009-07-08T11:22:02+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=46
permalink: '/blog/2009/07/08/signing-someone%e2%80%99s-public-key/'
itsec_enable_ssl:
  - "1"
categories:
  - linux
---
In order to help make a digital signature trustworthy you can ask people you know who also own gpg identities to sign yours. This in turn allows for the web of trust to be bootstrapped by people signing and verifying each others gpg identities. 

In order to sign a gpg identity, one needs to : 

  * Import the user&#8217;s public key, ([mine can grabbed from here](https://mmt.me.uk/blog/mischa.pubkey.asc)):  
    `gpg --import somePubKey.asc`
  * Check the identities fingerprint: 
    `gpg --fingerprint PubKeyHexValue`</li> 
    
      * Given that you are convinced the key belongs to whoever you think it should, sign the key: 
        `gpg --sign-key PubKeyHexValue`</li> 
        
          * Send the signed key back to your keyserver:  
            `gpg --send-keys PubKeyHexValue`</ul> 
        
        I sign all of my emails using my [gpg public key](https://mmt.me.uk/blog/mischa.pubkey.asc), it should be noted that only emails sent from my laptop can sign be signed using this identity. I should thank my former colleagues from the [University of Southampton](http://www.soton.ac.uk/) who signed by gpg identity, they have done their little bit to help bootstrap the Web of Trust.
