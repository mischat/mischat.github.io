---
id: 392
comments: true
title: Disabling Referer Headers in Firefox
date: 2010-11-21T17:25:22+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=392
permalink: /blog/2010/11/21/disabling-referer-headers-in-firefox/
itsec_enable_ssl:
  - "1"
categories:
  - Firefox
  - Privacy
tags:
  - firefox
  - header
  - privacy
  - referer
---
Given the [awesome work detailed by Bala from AT&T](http://www2.research.att.com/~bala/papers/), and some recent privacy related measures I have been taking in my [Firefox browser](http://mozilla.org/firefox) (see [https-everywhere](https://mmt.me.uk/blog/2010/10/26/https/) and [adblocking fb](https://mmt.me.uk/blog/2010/07/30/the-facebook-like-button/)), I have decided to instruct my browser to stop sending the [Referrer Header](http://en.wikipedia.org/wiki/HTTP_referrer) (nb: incorrectly referred to as the &#8216;referer header&#8217;), when I am clicking around on the web. 

The following example shows the Referrer header of the HTTP request telling [facebook.com](http://www.facebook.com/), that I have just been looking at a page about [HIV on the NHS choices website](http://www.nhs.uk/conditions/HIV/Pages/Introduction.aspx). 

`GET /<br />
Host: www.facebook.com<br />
User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_4; en-gb) AppleWebKit/533.18.1 (KHTML, like Gecko) Version/5.0.2 Safari/533.18.5<br />
Accept: application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8,image/png,*/*;q=0.5`  
**Referer: http://www.nhs.uk/conditions/HIV/Pages/Introduction.aspx**  
`Accept-Language: en-gb<br />
Accept-Encoding: gzip, deflate<br />
Cookie: presence=DJ290173073BchADhA_22112.channelH1L60X...`

I followed instructions on the following blog post <http://cafe.elharo.com/privacy/privacy-tip-3-block-referer-headers-in-firefox/> to configure my Firefox instance to not send the &#8220;referer header&#8221;. 

In short, the steps needed are as follows: 

  * Type **about:config** into your firefox awesome bar, to bring up your settings
  * find the setting `network.http.sendRefererHeader`. This is probably set to 2.
  * Choose one of the following values: 
      * 0: Completely disables the referer header (mischa&#8217;s setting)
      * 1: Sends a referer header when following a link to another page, but not when loading images on the page
      * 2: Always sends the referer header (default)

I am going to experiment with setting it to 0, disabling the referer header all the time, I will post back here to say if it causes me any problems.  
</p>
