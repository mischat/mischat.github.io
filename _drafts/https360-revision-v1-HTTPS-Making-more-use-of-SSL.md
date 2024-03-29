---
id: 362
title: 'HTTPS: Making more use of SSL'
date: 2010-10-26T11:31:01+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/10/26/360-revision-2/
permalink: /2010/10/26/360-revision-v1/
---
There has been a lot of talk about how more and more people are using their laptops on public wifi connections, and with the advent of the [Firesheep plugin](http://github.com/codebutler/firesheep/downloads), there has been a number of scares around session hijacking, and [unencrypted login details being sent through the ether](http://blogs.computerworld.com/17228/firesheep_firefox_extension_opens_fire_on_sheep_browsers). 

As a result, I thought I would describe the steps I have taken in securing my [Firefox](https://www.mozilla.com/en-US/) instance on my laptop. These are : 

  * Installing the [HTTPS Everywhere](https://www.eff.org/https-everywhere) plugin from the [eff](https://www.eff.org/), which attempts to select https if available when accessing a site. I have tested it with [Facebook](http://www.facebook.com/), [Google](http://www.google.com/), [Hotmail](http://www.hotmail.com/), [LinkedIn](http://linkedin.com/) and a few other sites
  * I have set my homepage to be [encrypted.google.com](https://encrypted.google.com/)
  * I have changed the search engine in top right hand of my Firefox instance to use the encrypted google service, by installing [their plugin](https://addons.mozilla.org/en-US/firefox/addon/161897/)
  * I have set a master password on my Firefox keychain, which gives my stored passwords some level of protection
  * And I run Adblocking software, (with a custom Facebook Like Button blocking extension) as per an [earlier blog post](https://mmt.me.uk/blog/2010/07/30/the-facebook-like-button/)

Furthmore, I use Firefox as my main browser, I have chrome installed, but I hardly ever use it, and I have a  [locked down, stateless Safari instance](https://mmt.me.uk/blog/2009/11/15/private-browsing-with-safari/) which I wrote about earlier.