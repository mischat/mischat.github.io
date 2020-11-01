---
id: 156
title: The Facebook Like Button, and how it follows you around the web
date: 2010-07-29T22:11:34+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/07/29/148-revision-8/
permalink: /2010/07/29/148-revision-v1/
---
There has been a lot of hype and talk around the Facebook Like button, and I do understand that the issues I raise in this blog post have been addressed before, I will cite some relevant literature at the bottom of this post. 

In short, I fear that [Facebook](http://www.facebook.com/) via the [Facebook Like button](http://developers.facebook.com/docs/reference/plugins/like) which you can find on many high volume, mainstream sites, such as [imdb](http://www.imdb.com/), [rottentomatoes](http://www.rottentomatoes.com/), [cnn](http://www.cnn.com/), etc, is tracking you even if you are not logged into Facebook from your browser.

This is Dan Brickley&#8217;s illustration of what an iFrame actually is : 

![Dan Brickley's drawing of an iFrame](http://farm2.static.flickr.com/1155/4722327870_793fc37846_d.jpg) 

There is also the issue around, what a total joke this is : 

<http://www.wired.com/threatlevel/2010/07/zombie-cookies-lawsuit/>

<https://addons.mozilla.org/en-US/firefox/addon/6623/>

Hi, 

I could be totally wrong, and if so I apologise to you and will probably apologise to other people I know which are involved, but yeah ah well am but a little noise on twitter anyways&#8230; 

As far as I can tell there are two methods for doing the facebook like button, the JS-SDK, and an iframe method, i think you guys are using the JS version. The API docs seem to suggest that there is a [JS call](http://developers.facebook.com/docs/reference/javascript/FB.getLoginStatus) which asks Facebook, who you are, and whether you logged in or not. 

Look I could be totally wrong here, but am going to spend the next hour or so hacking something together on my site to see if I can debug this properly. 

If I am logged into facebook, i.e. on a different tab, and I turn up at a page which has a facebook like button on it, Facebook will know I am there, and the page I am visiting will know which facebook account I am. That is, it will send me something along the lines of &#8220;3 of your friends have liked this page already&#8221; (I am about 90% sure about this, but will find out soon enough). What I am not certain about is if I am logged out of facebook, but there is still a facebook cookie on my machine which identities me, does the [getLoginStatus API call](http://developers.facebook.com/docs/reference/javascript/FB.getLoginStatus) know who I am and return a &#8220;notConnected&#8221; from the API. This is something else I am trying to test on my personal website now. 

But yeah, I am just a &#8220;guespert&#8221; why doesn&#8217;t the expert which implemented this stuff tell me that I am wrong?

I will report back on my findings, but I am not a JS whizz at all, but should be able to figure this stuff out.

Anyways, 

Mischa *sighes &#8230; Anyways, even if they don&#8217;t check your cookie if you are not logged in, they know which facebook account you are which has turned up on their site: &#8220;<http://www.theregister.co.uk/2010/05/17/browser_fingerprint/>&#8221; &#8230; from my POV this is passive data collection, I wish I had a gf so I could then ditch twitter &#8230;