---
id: 236
title: The joys of upgrading to PHP 5.3
date: 2010-08-20T12:32:47+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/08/20/144-revision-9/
permalink: /2010/08/20/144-revision-v1/
---
I have been bitten by a number of things when I updated my PHP to PHP 5.3. These are the changes which I had to make to my php.ini file : 

`<br />
short_open_tag = 1<br />
` 

This option allows for the use of the short hand  `"<?"` and  `"?>"` used as abbreviations for `"<?php"` and  `"php?>"`. And yes, shorts hand are good, I am super lazy, insofar as I am not good at setting &#8220;use strict;&#8221; when writing perl code. 

Secondly, I was stung due to the fact that PHP 5.3 has clamped down on the returning of values when expecting a reference to be returned by a function, this phenomena and the necessary fix is illustrated in my [previous blog post](https://mmt.me.uk/blog/2010/08/20/openid-wp-brokenness/).