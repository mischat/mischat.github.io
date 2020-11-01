---
id: 435
title: NHS.uk allowing Google, Facebook, and others to track you
date: 2010-12-01T20:34:26+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/11/21/369-autosave/
permalink: /2010/12/01/369-autosave-v1/
---
The [NHS](http://www.nhs.uk/) is allowing [Google](http://www.google.com/), [Facebook](http://www.facebook.com/), and others to track your <http://www.nhs.uk/> browsing habits, regardless of the fact that people use the page to seek medical advice. It was recently pointed out to me that the [NHS Choices website&#8217;s](http://www.nhs.uk/Pages/HomePage.aspx) social features include the Facebook Like button (see e.g. the [page on Testicular Cancer](http://www.nhs.uk/Conditions/Cancer-of-the-testicle/Pages/Introduction.aspx)). Due to the [fact that the standard method of Facebook Like button deployment is intrusive to say the least](https://mmt.me.uk/blog/2010/07/30/the-facebook-like-button/), I thought I would look into identifying which third party companies have been given permission to track users on NHS Choices, and my results are rather disconcerting.

In short there are four third-party, advertising/tracking companies which are informed every time a user visits one of the &#8220;conditions pages&#8221; on the NHS Choices website. These listed below, all get to make a call from the user&#8217;s browser, in turn allowing the four companies to access their cookies, tracking the users (explained in [a previous blog post of mine,](https://mmt.me.uk/blog/2010/07/30/the-facebook-like-button/) and in [Bala&#8217;s research](http://www2.research.att.com/~bala/papers/)). This means, that if one has ever logged into a Google account, or a Facebook account and then visits one of the pages on the NHS site, the company will then know that their user X was just looking at a page about condition Y on the NHS website. 

These are the four third party companies that make requests every time a &#8220;conditions page&#8221; on <http://www.nhs.uk/> is viewed by a user:

`jambi:~ mt $ grep "Host" tcpdump.ext.20101121.log | sort -u<br />
Host: l.addthiscdn.com<br />
Host: statse.webtrendslive.com<br />
Host: www.facebook.com<br />
Host: www.google-analytics.com`

Two of the four third-party sites ([facebook.com](http://www.facebook.com) and [addthiscdn.com](http://addthiscdn.com)) are contacted in order to provider the &#8220;social functionality&#8221; shown in the following screenshot. This intrusive OPT-OUT method of adding social features to the NHS website, in my opinion is NOT acceptable. I would only deem this to be acceptable if NHS has written declarations from the two aforementioned services stating that they WOULDN&#8217;T be tracking peoples&#8217; browsing habits on <http://www.nhs.uk/>. 

[<img src="https://mmt.me.uk/blog/wp-content/uploads/2010/11/nhschoices2010-11-21T17.28.24.png" alt="" title="NHS Choices &quot;Social Features&quot;" width="90%" class="aligncenter size-full wp-image-411" />](https://mmt.me.uk/blog/wp-content/uploads/2010/11/nhschoices2010-11-21T17.28.24.png)

And the other two sites contacted ([webtrendslive.com](http://webtrendslive.com) and [google-analytics.com](http://www.google-analytics.com)) seemed to be used for analytics purposes. In my view, this task should NOT be outsourced to a third party. If this was a website about pub reviews these third-party services would be acceptable, but due to the nature of the information on the Choices website, I feel the NHS should be hosting their own analytics code. Ok, I understand that the NHS needs to gather statistics about their website usage, but **their user&#8217;s privacy should be of utmost importance**, there do exist a high number of open sourced analytics software which the NHS should run themselves.

In order to show that I am not making this up, I have captured all of the HTTP requests made by my browser when loading the HIV and AIDS information page on NHS Choices. 

<http://www.nhs.uk/conditions/HIV/Pages/Introduction.aspx>

[<img src="https://mmt.me.uk/blog/wp-content/uploads/2010/11/firebugNetNHS.uk_.2010-11-21T13.49.15.png" alt="" title="Firebug Network traffic output HIV/AIDS Information Page on the NHS" width="90%" class="aligncenter size-full wp-image-371" />](https://mmt.me.uk/blog/wp-content/uploads/2010/11/firebugNetNHS.uk_.2010-11-21T13.49.15.png)

The below two files are logs of all HTTP requests made when loading the HIV page:

<https://mmt.me.uk/blog/misc/nhscookies/tcpdump.full.20101121.log>

And this cut down log file shows all of the third-party HTTP requests made by one&#8217;s browser when loading the aforementioned page: 

<https://mmt.me.uk/blog/misc/nhscookies/tcpdump.ext.20101121.log>

The above logs where captured using the following bash command:  
`tcpdump -A -s 1024 -i en0 dst port 80`

**An example:** 

My colleague [Steve](http://steve.harris.name/) captured output from the HTTP trace via the NHS website, it can be found on <http://pastebin.com/4TfDRRZJ>

The browser (Safari) had it&#8217;s history cleared, logged into facebook, the facebook window closed, then sent to the NHS page. 

Bits of confidential data replaced with XXXs

`GET /plugins/like.php?href=http%3A%2F%2Fwww.nhs.uk%2fConditions%2fHIV%2fPages%2fIntroduction.aspx&layout=button_count&show_faces=true&width=450&action=like&colorscheme=light&height=21 HTTP/1.1<br />
Host: www.facebook.com<br />
User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_4; en-gb) AppleWebKit/533.18.1 (KHTML, like Gecko) Version/5.0.2 Safari/533.18.5<br />
Accept: application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8,image/png,*/*;q=0.5<br />
Referer: http://www.nhs.uk/conditions/HIV/Pages/Introduction.aspx<br />
Accept-Language: en-gb<br />
Accept-Encoding: gzip, deflate<br />
Cookie: presence=DJ290173073BchADhA_22112.channelH1L60XXXXXXXXXXXXXXXXX4104WMblcMsndPBXXXXXXXXXXXsbPBtA_5b_5dBfAnullBuctMsA0QBblADacP0VXXXXXXXXXXXX0K290173073QQQ; x-referer=http%3A%2F%2Fwww.facebook.com%2Fhome.php%23%2Fhome.php; xs=976XXXXXXXXXXXXXXXXXXX0e11a0e600; sid=2; sct=12XXXXXX70; made_write_conn=12XXXXXX70; lu=ghXXXXXXXXXXXXXXXXXXYgqQ; datr=12XXXXXXXX-XXXXXXXXXXXf24`

**Possible Data Protection Violation**

_It was pointed out to me that I was reference the incorrect ICO filing. The data controller for the NHS Choices website is the Department of Health and not NHS Direct. </p> 

Find below, my amended version of this and the following section of this blog post. &#8211; **Mischa 2010-11-24 11:00:00**.</em>

In order to see the NHS&#8217;s Data Protection Policy, we had a look at their [ICO](http://www.ico.gov.uk/) filing, which led me to the following page:

<del datetime="2010-11-24T10:12:42+00:00"><a href="http://www.ico.gov.uk/ESDWebPages/DoSearch.asp?reg=4693360">http://www.ico.gov.uk/ESDWebPages/DoSearch.asp?reg=4693360</a></del>  
<http://www.ico.gov.uk/ESDWebPages/DoSearch.asp?reg=4906007>

I should start this section by saying that I am not a lawyer. But it seems like <del datetime="2010-11-24T10:12:42+00:00">sections 6 and 4</del> **purpose 2** <del datetime="2010-11-24T10:12:42+00:00">are</del> **is** relevant to my question of &#8220;how come the NHS website has third-party tracking enabled, especially given that the tracking is provided by for profit advertising companies?&#8221;. Firstly, it should be noted that by contacting facebook and google, data is being sent outside of the European Economic Area. Which is in violation of their Data Protection commitment of &#8220;Transfers: None outside the European Economic Area&#8221;.

<del datetime="2010-11-24T10:12:42+00:00">And as per the ICO filing the potential recipients are: Business associates and other professional advisers, Central Government, Data subjects themselves, Employees and agents of the data controller, Healthcare, social and welfare advisers or practitioners, Local Government, Ombudsmen and regulatory authorities, Other companies in the same group as the data controller, Persons making an enquiry or complaint, Police forces, Relatives, guardians or other persons associated the data subject, Survey and research organisations.</p> 


  <p>
    I will like to point out that no where in the ICO filing can one see that the NHS will be sharing data with advertising companies.</del>
  </p>



  <p>
    It should be noted that the <a href="http://www.ico.gov.uk/ESDWebPages/DoSearch.asp?reg=4906007">ICO filing</a> does not make it explicit that the Department of Health would not:
  </p>



  <ul>
    <li>
      Sell advertising to patients
    </li>
    <li>
      Sell/Provide user data for third party advertising
    </li>
  </ul>



  <p>
    <strong>Next Steps: FOI </strong>
  </p>



  <p>
    I am about to post off a Freedom Of Information request (tomorrow morning), asking the NHS to please supply the minutes of all policy and technical meetings involved in the decision to deploy iframes referencing non-NHS sites and to use third-party analytics software on NHS choices pages.
  </p>



  <p>
    <strong>Next Steps: Official Complaint </strong>
  </p>



  <p>
    Further to the FOI request I am going to submit an official complaint via the official NHS Choices feedback form :<a href="http://www.nhs.uk/aboutNHSChoices/Pages/ContactUs.aspx">http://www.nhs.uk/aboutNHSChoices/Pages/ContactUs.aspx</a>.
  </p>



  <p>
    I have the latest copy of the <del datetime="2010-11-24T10:12:42+00:00"><a href="https://mmt.me.uk/blog/misc/nhscookies/FOIRequest.pdf">FOI Request</a></del> <a href="https://mmt.me.uk/blog/misc/nhscookies/FOIRequest.pdf">updated FOI Request</a> and the<a href="https://mmt.me.uk/blog/misc/nhscookies/LetterOfComplaint.pdf"> Letter of Complaint</a> up in .pdf format on <a href="https://mmt.me.uk/blog/">my website</a>.
  </p>



  <p>
    <strong>Note that: </strong>
  </p>



  <p>
    There is a way to deploy the Facebook Like button which would resemble an OPT-IN based user interaction, instead of the intrusive standard iframe based approach. This involves the use of an &#8220;onClick&#8221; function call in Javascript which would tell Facebook only when explicitly &#8220;liked&#8221;. Obviously this method of interaction does not display the &#8220;social information&#8221; such as like counts, and whether or not you would be the first of your friends to &#8220;like&#8221; a given page. The German social networking site <a href="http://jetzt.de/">jetzt.de</a> moved from the iframe to the self-hosted version after vigorous backlash from the userbase about being tracked (see for instance <a href="http://jetzt.sueddeutsche.de/texte/anzeigen/385237">http://jetzt.sueddeutsche.de/texte/anzeigen/385237</a>, line 350). This example was given to me by Sören Preibusch from the University of Cambridge.
  </p>



  <p>
    <strong>And Finally&#8230;</strong>
  </p>



  <p>
    I would like to thank <a href="http://steve.harris.name/">Steve Harris</a> and <a href="http://danbri.org/">Dan Brickley</a> for helping me decide how to take this forward. And I would like to thank <a href="http://twitter.com/rich13">Richard Northover</a> for the link.
  </p>



  <p>
    <strong>Amendment 2010-11-24 16:57 Conflict in terms of NHS privacy policy</strong><br /> It has been pointed out to me that in relation to the NHS stating that how only on pages with the Like button&#8230;. communications with Facebook.com occurs, this is also not true :
  </p>



  <p>
    See the following page :
  </p>



  <p>
    <a href="http://www.nhs.uk/livewell/depression/pages/depressionhome.aspx">http://www.nhs.uk/livewell/depression/pages/depressionhome.aspx</a>
  </p>



  <p>
    I see no &#8220;Like&#8221; button on this page. But according to firebug, There is still an HTTP request made to facebook.com from my browser.
  </p>



  <p>
    The following quote from the <a href="http://www.nhs.uk/aboutNHSChoices/aboutnhschoices/termsandconditions/Pages/Privacypolicy.aspx">NHS Choices privacy policy</a> states :
  </p>



  <p>
    <em>&#8220;While we only share your information with the Data Processors, when you visit pages on our site that display a Facebook Like button, Facebook will collect information about your visit. For more information, read the relevant section of the Facebook privacy policy.&#8221;</em>
  </p>



  <p>
    Which is NOT true.
  </p>



  <p>
    The following screenshot illustrates this. People are free to replicate, all you need is Firefox and the Firebug plugin (both free and open source).
  </p>



  <p>
    <a href="https://mmt.me.uk/blog/wp-content/uploads/2010/11/Screen-shot-2010-11-24-at-17.01.38.png"><img src="https://mmt.me.uk/blog/wp-content/uploads/2010/11/Screen-shot-2010-11-24-at-17.01.38.png" alt="Firebug + Firefox + NHS Website + Facebook.com HTTP request + No Like Button" title="Screen shot 2010-11-24 at 17.01.38" width="90%" class="aligncenter size-full wp-image-441" /></a>
  </p>



  <p>
    <strong>NHS privacy policy</strong>
  </p>



  <p>
    I thought I would cut and paste the NHS&#8217;s privacy policy, in case it changes dated 2010-11-25 15:58:00 GMT
  </p>



  <p>
    <em>&#8220;As a government department, we do not share data with other organisations unless the law permits us to do so. We do not sell individual information. We will share it only with our authorised Data Processors, who must act at all times on our instructions as the Data Controller under the Data Protection Act 1998. Before you submit any information, we will notify you as to why we are asking for specific information and it is up to you whether you provide it.</p> 
    
    <p>
      While we only share your information with the Data Processors, when you visit pages on our site that display a Facebook Like button, Facebook will collect information about your visit. For more information, read the relevant section of the Facebook privacy policy.&#8221;</em>
    </p>
    
    <p>
      <strong>Furthermore</strong>
    </p>
    
    <p>
      It should be noted that it has been pointed out to me that AddThis&#8217; privacy policy reveals they monetise their product through behavourial targeting. Would you be somewhat surprised if you started to received adverts about their ailments on third-party websites.?
    </p>