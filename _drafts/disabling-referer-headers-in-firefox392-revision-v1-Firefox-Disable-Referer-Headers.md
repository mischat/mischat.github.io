---
id: 395
title: Firefox Disable Referer Headers
date: 2010-11-21T16:54:40+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/11/21/392-revision-3/
permalink: /2010/11/21/392-revision-v1/
---
Given the awesome work detailed by Bala from AT&T, and some recent privacy related measures I have been taking in my Firefox browser, I have decided to instruct my browser to stop sending the Referer Header, when I am clicking around on the web. 

GET /plugins/like.php?href=http%3A%2F%2Fwww.nhs.uk%2fConditions%2fHIV%2fPages%2fIntroduction.aspx&layout=button\_count&show\_faces=true&width=450&action=like&colorscheme=light&height=21 HTTP/1.1  
Host: www.facebook.com  
User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10\_6\_4; en-gb) AppleWebKit/533.18.1 (KHTML, like Gecko) Version/5.0.2 Safari/533.18.5  
Accept: application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8,image/png,\*/\*;q=0.5  
Referer: http://www.nhs.uk/conditions/HIV/Pages/Introduction.aspx  
Accept-Language: en-gb  
Accept-Encoding: gzip, deflate  
Cookie: presence=DJ290173073BchADhA\_22112.channelH1L60XXXXXXXXXXXXXXXXX4104WMblcMsndPBXXXXXXXXXXXsbPBtA\_5b\_5dBfAnullBuctMsA0QBblADacP0VXXXXXXXXXXXX0K290173073QQQ; x-referer=http%3A%2F%2Fwww.facebook.com%2Fhome.php%23%2Fhome.php; xs=976XXXXXXXXXXXXXXXXXXX0e11a0e600; sid=2; sct=12XXXXXX70; made\_write_conn=12XXXXXX70; lu=ghXXXXXXXXXXXXXXXXXXYgqQ; datr=12XXXXXXXX-XXXXXXXXXXXf24

<blockquote class="wp-embedded-content" data-secret="iHW7R4rvbd">
  <p>
    <a href="http://cafe.elharo.com/privacy/privacy-tip-3-block-referer-headers-in-firefox/">Privacy Tip #3: Block Referer Headers in Firefox</a>
  </p>
</blockquote>