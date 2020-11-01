---
id: 455
title: Knocking up my own RSS reader
date: 2010-12-13T00:05:14+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=455
permalink: /2010/12/13/rss-reader/
itsec_enable_ssl:
  - "1"
categories:
  - Privacy
tags:
  - data
  - privacy
  - rss
---
Since [Newsgators RSS Reader](http://www.newsgator.com/rss-readers.aspx) asked me to supply them with a Google Account, becoming [Google Reader](http://www.google.com/reader), I gave up on the service. I using an RSS reader which would sync my laptop with my phone and when my phone became capable of reading interwebs when traveling about. In short RSS is awesome, and Google Search is awesome, but I try and spread my personal data thin across many companies instead of giving it all away to one. I used the [iGoogle](http://www.google.com/ig) page for a while, but I thought I could just emulate that on my website, so I did &#8230;

In short: 

[Google](http://www.google.com/) offer a great search experience, they can have my search history, [Facebook](http://www.facebook.com/) offer a good way to stay in touch with your friends, [Yahoo/Flickr](http://www.flickr.com/) provide a good photo sharing experience, and well [Last.fm](http://www.last.fm/) do an awesome job of recommending me music &#8211; get what I am hinting at. I could just used Google to do all of the above, but somehow I feel better about myself spreading my data around a bit (sorry crazy doesn&#8217;t it!).

So, I made a start at knocking together my own RSS reader which I can use to catch up on stuff : <https://mmt.me.uk/blog/rss/>. I used this [PHP RSS Reader library](http://www.scriptol.com/rss/rss-reader.php). Sadly, it doesn&#8217;t understand RSS 1.0 which is RDF, it only seems to parse RSS 2.0. 

It was really easy to do not more than an hours work. I am going to start parsing in the descriptions of the items in the RSS feeds, but sadly this isn&#8217;t trivial, people are starting to flood their streams with linked to google-analytics, to facebook share (including links to icons hosted on facebook.com [naughty]), and other nastiness. So I will have to write some code to pull out all the evil in the descriptions before adding them to <https://mmt.me.uk/blog/rss/>, I will update my blog when I get round it to it. I can also release code if people want, just shout&#8230;

[<img src="https://mmt.me.uk/blog/wp-content/uploads/2010/12/Screen-shot-2010-12-12-at-23.03.04.png" alt="" title="Simple HTML based RSS Reader" width="95%" class="aligncenter size-full wp-image-458" />](https://mmt.me.uk/blog/wp-content/uploads/2010/12/Screen-shot-2010-12-12-at-23.03.04.png)

On a similar topic, the below blog post, states: 

_&#8220;One privacy protection model is to scatter your data about to make it more difficult to parse, akin to keeping valuables in different hiding spots in your house to thwart intruders getting everything in one go.&#8221;_

When referring to the use of Facebook, as your one stop shop for IM messages, photos, emails and your social graph. 

<http://blogs.forbes.com/kashmirhill/2010/11/29/how-facebook-applications-can-download-all-the-messages-in-your-inbox/>