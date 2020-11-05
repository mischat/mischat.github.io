---
id: 148
"comments: true"
title: The Facebook Like Button, and how it is following you around the web
date: 2010-07-30T01:13:32+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=148
permalink: /blog/2010/07/30/the-facebook-like-button/
openid_comments:
  - 'a:2:{i:0;s:4:"2939";i:1;s:4:"3445";}'
itsec_enable_ssl:
  - "1"
categories:
  - Privacy
tags:
  - facebook
  - iframe
  - like
  - likebutton
  - privacy
---
There has been a lot of hype and talk around the Facebook Like button, and I do understand that the issues I raise in this blog post have been addressed before, I will cite some relevant literature at the bottom of this post. 

In short, I fear that [Facebook](http://www.facebook.com/) via the [Facebook Like button](http://developers.facebook.com/docs/reference/plugins/like) which you can find on many high volume, mainstream sites, such as [imdb](http://www.imdb.com/), [rottentomatoes](http://www.rottentomatoes.com/), [cnn](http://www.cnn.com/), etc, is tracking you even if you are not logged into Facebook from your browser.

So, I have no solid evidence to say that they are DEFINITELY doing so, but I will explain why it is technically possible for them to do so. And well, the **cynic in me thinks that if it is technically possible for facebook to log that my facebook id is on a given page, it will, regardless of whether or not I am logged in or not**.

From this point onwards, I will be referring to all of various versions of the **Like** button, i.e. Like, Recommend, Fan, etc as the Facebook Like button. 

So, the Facebook Like button can be implemented in one of two ways, using facebook&#8217;s [XFBML](http://wiki.developers.facebook.com/index.php/XFBML) or via the inclusion of a Facebook [iFrame](http://en.wikipedia.org/wiki/HTML_element#Frames). FWIW, all of the instances of the Like button I have come across have been implemented using the iFrame approach, but I will look into the XFBML method of doing things soon and will blog about it then (he says &#8230;) 

So, if you are a facebook user, and you have visited facebook  
since the last time you cleared you cookies, you will have a facebook cookie in your browser. It is this cookie which allows facebook to inform you of how many of your friends have liked the page your browser is currently pointing to. An example of functionality can be seen in the below screenshot.

[<img loading="lazy" src="https://mmt.me.uk/blog/wp-content/uploads/2010/07/max.png" alt="fblike" title="Max and Facebook Like" width="412" height="75" class="alignnone size-full wp-image-190" />](https://mmt.me.uk/blog/wp-content/uploads/2010/07/max.png)

I am aware that if you are signed out of facebook you wont see your list of friends which are have already clicked the like button, you will end up seeing something like:

[<img loading="lazy" src="https://mmt.me.uk/blog/wp-content/uploads/2010/07/max2.png" alt="not logged in" title="Facebook Like Button sans logged in" width="342" height="65" class="alignnone size-full wp-image-194" />](https://mmt.me.uk/blog/wp-content/uploads/2010/07/max2.png)

So, given that the Like button is an iFrame, i.e. it is actually hosted on www.facebook.com, it means that facebook can read your facebook.com [cookies](http://en.wikipedia.org/wiki/HTTP_cookie), and they can tell whether you are logged in (to show you which are of your friends have &#8220;liked&#8221; the page before you). And well, technically this implies that they know _who you are_ which enables them to tell whether you are logged in or not. 

[Dan Brickley](http://danbri.org/foaf.rdf#danbri) created a neat drawing of the what a iFrame is actually doing (thanks Dan, and see below). The illustration highlights the fact that a page which seems to be coming from a given web address, if it includes an iFrame, is actually coming from multiple web servers. 

This is danbri&#8217;s illustration of what an webpage which includes iFrame&#8217;s is actually doing

[![Dan Brickley's drawing of an iFrame](http://farm2.static.flickr.com/1155/4722327870_793fc37846_d.jpg)](http://www.flickr.com/photos/danbri/4722327870)  
[![Some Right Reserved](http://creativecommons.org/images/public/somerights20.gif)](http://creativecommons.org/licenses/by-nc-sa/2.0/)

This makes me class the Facebook Like button in the same category as ad tracking sites, insofar as the fact that if you turn up to a page with a Like iFrame, and you have a facebook cookie, you are **in theory** being tracked, regardless of whether or not you choose to click the Like button or not. 

So, why do I class this in with ad trackers, I do this because of the fact that you are being tracked passively, i.e. regardless of whether or not you choose to like something, facebook is **theoretically** logging the fact that you have been to that website. 

**So, now to give an example :** 

Let&#8217;s say that you turn up to [cnn.com](http://www.cnn.com/) can you visit the below article: 

<http://www.cnn.com/2010/US/07/29/wisconsin.roush.crash/>

The page them subsequently loads up the following iFrame and serves it to you, it renders the Like button on the page, the iframe revolves to a url on facebook.com

[http://www.facebook.com/plugins/like.php?action=recommend&&#8230;](http://www.facebook.com/plugins/like.php?action=recommend&api_key=64b385429f05b2492d713f343d05ba02&channel_url=http%3A%2F%2Fstatic.ak.fbcdn.net%2Fconnect%2Fxd_proxy.php%23%3F%3D%26cb%3Df352b329c1716ae%26origin%3Dhttp%253A%252F%252Fwww.cnn.com%252Ffd00b01dbaa2ca%26relation%3Dparent.parent%26transport%3Dpostmessage&href=http%3A%2F%2Fwww.cnn.com%2F2010%2FUS%2F07%2F29%2Fwisconsin.roush.crash%2Findex.html&layout=standard&locale=en_US&node_type=link&sdk=joey&show_faces=true&width=420)

By going to the first URL, you are also hitting the second one. Your user-agent, which based on <http://panopticlick.eff.org/>, is kinda uniquely identifiable, and is therefore in facebook&#8217;s logs. Given that the iFrame (second URL above) is hosted on facebook&#8217;s site, they **CAN** read your facebook cookies, am **NOT** saying that they do as I can&#8217;t prove that in anyway, but my guestimate is that if they are not, they **will be in the future**. 

So, I can see three scenarios, which are relevant to this 

  * A user is logged into facebook in their browser, and then visits a site in a different tab, not even knowing that the site has a facebook &#8220;like&#8221; button, because you will only become aware of the &#8220;like&#8221; button upon arriving at the page and having it in loaded in your browser, which is too late from my POV. This happened to me last night, and happened to me recently when I went to imdb (sighes).
  * A user is not logged into facebook, but has facebook cookies in their browser, they go to cnn.com, facebook knows (with a high probability) that a given facebook ID has visited a given site, by virtue of cookies and stuff
  * User has no facebook cookies, and then facebook will only get the user&#8217;s user-agent in their access logs, which I bet they store (even though once again I have no proof of this.

**Ok, so solutions:** 

_Solution 1 :_

You can delete all of you facebook related cookies from your main browser ([firefox](http://www.mozilla.com/en-US/firefox/personal.html) being browser of choice), and then you can download another browser which you use for facebook&#8217;ing, so that you are no longer given facebook the option to track the pages you read on the web. 

_Solution 2 :_

Which is the solution I am going for at the moment is that you can install [Adblocker Plus](http://adblockplus.org/) and you can block all of the Facebook Like endpoints, using custom filters. 

This is an export of my Facebook Like button filters, it is probably far from complete, and I will put it up a service which you can subscribe to in Adblocks Plus, and will update the list of URLs as and when I come by them (will blog post when I am done with this.) 

`<br />
[Adblock]<br />
! Checksum: 1+81iD/9dKSZiqqW6WtQxA<br />
http://www.connect.facebook.com/widgets/likebox.php?*<br />
http://static.ak.connect.facebook.com/js/api_lib/v0.4/FeatureLoader.js.php?*<br />
http://www.connect.facebook.com/widgets/like.php?*<br />
http://www.connect.facebook.com/widgets/fan.php?*<br />
http://www.facebook.com/plugins/fan.php?*<br />
http://www.facebook.com/widgets/likebox.php?*<br />
http://www.facebook.com/plugins/likebox.php?*<br />
http://www.facebook.com/plugins/like.php?*<br />
http://www.facebook.com/widgets/fan.php?*<br />
http://www.facebook.com/widgets/like.php?*<br />
` 

The following screenshot, shows what my current step looks like in Adblocker plus: 

[![Adblock](https://mmt.me.uk/blog/wp-content/uploads/2010/07/adblock.png "Adblock Facebook Like buttons")](https://mmt.me.uk/blog/wp-content/uploads/2010/07/adblock.png)

My colleague Vaidas Jablonskis (who is awesome), pointed me to [Adbocker Plus](http://adblockplus.org/) which is also totally awesome 🙂

Finally, it is worth mentioning that I am not sure whether or not all of these sites which have facebook like buttons are explicit about the fact that their users **CAN** be tracked passively by facebook. Or whether reputable brands like CNN have any form of agreement with Facebook regarding whether or not their users are being track. Are any of these big companies, breaking their terms and conditions ?

I will post an update on step by step instructions regarding how to subscribe to my Adblock filter list of facebook like buttons endpoints soon. 

So, I suggest people download and install Adblock and block facebook like buttons, and subsequently install the [Facebook Like plugin](https://addons.mozilla.org/en-US/firefox/addon/162124/) , so that they are no longer being passively tracked by Facebook, and so that they are in control of when they tell Facebook that they like a given web page. 

Finally, links to existing literature in this space: 

<http://techcrunch.com/2010/04/23/like-buttons-evil-facebook-not-open/>

<http://philosophicalzombie.net/post/540799211/has-facebook-just-become-the-evil-empire-whats-wrong>

Comment, corrections, or a simple &#8220;you are wrong because &#8230;&#8221; are very welcome 🙂

Happy Interneting People
