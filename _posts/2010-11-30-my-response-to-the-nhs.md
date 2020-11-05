---
id: 445
comments: true
title: My Response to the NHS
date: 2010-11-30T13:57:54+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=445
permalink: /blog/2010/11/30/my-response-to-the-nhs/
itsec_enable_ssl:
  - "1"
categories:
  - Privacy
tags:
  - instrusive
  - nhs
  - privacy
  - privacypolicy
---
**My letter to the NHS Choices Team dated 2010-11-30**

Hi Team NHS Choices, 

So, I just thought I would let you know that, as per my blog post, the NHS Choices website is sharing information with Facebook on pages which DONT have the Facebook Like button, as pointed out by this person, as well as being on my blog post for the last few days: 

<http://www.privacylives.com/v3-co-uk-ico-probes-nhs-choices-over-data-privacy-fears/2010/11/30/>

Note that, NHS Choices keeps stating that its privacy policy is correct, but if you read the last few paragraphs of my blog post, right before the &#8220;comments&#8221; section, you will see that this is not the case.

<https://mmt.me.uk/blog/2010/11/21/nhs-and-tracking/>

Do have a look at the following page on your website, there is NO like button, and the same data exchange is STILL happening with Facebook. 

<http://www.nhs.uk/livewell/depression/pages/depressionhome.aspx>

The following screenshot illustrates this. People are free to replicate, all you need is Firefox and the Firebug plugin (both free and open source). 

[<img src="https://mmt.me.uk/blog/wp-content/uploads/2010/11/Screen-shot-2010-11-24-at-17.01.38.png" alt="Firebug + Firefox + NHS Website + Facebook.com HTTP request + No Like Button" title="Screen shot 2010-11-24 at 17.01.38" width="90%" class="aligncenter size-full wp-image-441" />](https://mmt.me.uk/blog/wp-content/uploads/2010/11/Screen-shot-2010-11-24-at-17.01.38.png)

I also talked about how there is a German website which changed the manner in which it implemented the Like button functionality in a non-intrusive manner. That is, a manner which does NOT send any information to Facebook.com unless the user ACTIVELY CLICKS (i.e. OPT-IN) the Like button; quoting my blog post.

&#8220;There is a way to deploy the Facebook Like button which would resemble an OPT-IN based user interaction, instead of the intrusive standard iframe based approach. This involves the use of an “onClick” function call in Javascript which would tell Facebook only when explicitly “liked”. Obviously this method of interaction does not display the “social information” such as like counts, and whether or not you would be the first of your friends to “like” a given page. The German social networking site jetzt.de moved from the iframe to the self-hosted version after vigorous backlash from the userbase about being tracked (see for instance <http://jetzt.sueddeutsche.de/texte/anzeigen/385237>, line 350). This example was given to me by Sören Preibusch from the University of Cambridge.&#8221;

Please see the Garlik blog for more information : <http://www.garlik.com/blog/?p=419> 

Warmest Regards, 

Mischa
