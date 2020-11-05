---
id: 122
"comments: true"
title: Private Browsing with Safari
date: 2009-11-15T21:38:33+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=122
permalink: /blog/2009/11/15/private-browsing-with-safari/
itsec_enable_ssl:
  - "1"
categories:
  - OSX
  - Privacy
---
I use [Firefox](http://www.mozilla.com/firefox/) as my primary browser, both at home and at work. So I have setup my Safari browser, as my private browser &#8211; that is sans cache, history, cookies or anything of a similar nature. I noticed that the &#8220;Private Browsing&#8221; option in Safari, doesn&#8217;t do that good a job of not leaving files hanging around in one&#8217;s operating system, furthermore unless your careful, [Spotlight](http://en.wikipedia.org/wiki/Spotlight_%28software%29) will eventually end up indexing your browser history, cache, which may be less than ideal. 

In order to have a zero cache safari instance on my laptop I have taken the following steps :

  * 1: Removed spotlight&#8217;s prying eyes, by excluding the following directories : 
      * /Users/<USERDIR>/Library/Caches
      * /Users/<USERDIR>/Library/Safari
      * /Library/Caches
  * 2: Setup two cronjobs to constantly delete Safari cache-dir
`*/10 * * * * find /Users/<USERDIR>/Library/Safari -type f -exec rm {} \; 2>&1 > /dev/null<br />
*/10 * * * * find /Users/<USERDIR>/Library/Caches/Metadata/Safari/ -type f -exec rm {} \; 2>&1 > /dev/null` </ul> </ul> 

And finally, I have created a wrapper .app file which open&#8217;s Safari, and then enables &#8220;Private Browsing&#8221; mode, as I could not find a way to do this through editing the Safari.plist file. I followed the [instructions posted on the MacWorld site](http://www.macworld.com/article/139714/2009/03/enableprivatebrowsing.html), and they go a little something list so: 

  * 1. One needs to enable the Enable Access for Assistive Devices option, which can be found in the Universal Access system preference.
  * 2. Open the AppleScript editor, and type in the following commands : 
    `<br />
tell application "Safari"<br />
&nbsp;&nbsp;	activate<br />
end tell<br />
tell application "System Events"<br />
&nbsp;&nbsp;	tell process "Safari"<br />
&nbsp;&nbsp;&nbsp;	     tell menu bar 1<br />
&nbsp;&nbsp;&nbsp;&nbsp;	         tell menu bar item "Safari"<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	             tell menu "Safari"<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	               click menu item "Private Browsing"<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; end tell<br />
&nbsp;&nbsp;&nbsp;&nbsp; end tell<br />
&nbsp;&nbsp;&nbsp; end tell<br />
&nbsp;&nbsp;end tell<br />
end tell<br />
` </li> 
    
      * 3. Save this shiny new AppleScript as an application (.app file), and I called mine &#8220;PrivateSafari.app&#8221;. 
      * 4. I then grabbed the icon file from Safari, and added to the PrivateSafari, and then replace the old shortcut in my Dock, with one to &#8220;PrivateSafari.app&#8221;.</ul> 
    
    It should be noted that I am well aware that the private browsing features in most of the modern web browsers have come under a certain amount of scrutiny recently, below are some links to articles for the interested reader : 
    
      * [Private browsing modes leak data &#8211; BBC News](http://www.bbc.co.uk/news/technology-10891355)
      * [Private browsing: it&#8217;s not so private &#8211; Ars Technica](http://arstechnica.com/security/news/2010/08/private-browsing-not-so-private.ars)
      * [Private browsing ‘not so private’ &#8211; IT Pro](http://www.itpro.co.uk/625837/private-browsing-not-so-private) 
      * [Private browsing modes in four biggest browsers often fail &#8211; The Reg](http://www.theregister.co.uk/2010/08/06/private_browsing_mode_failure/)
