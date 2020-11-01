---
id: 23
title: 'ld: duplicate symbol _g_bit_nth_lsf Mac OSX Leopard/Darwin'
date: 2009-07-07T17:44:17+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2009/07/07/19-revision-4/
permalink: /2009/07/07/19-revision-v1/
---
I have had some problems installing software from source on my [Max OS X Leopard machine.](http://www.apple.com/macosx/) I should thank [Martin Szomszor](http://users.ecs.soton.ac.uk/mns2/) for his help on getting this working, but after some time faffing we finally got it sorted out.

I found that I was having problems making software on Leopard, which I could build fine on my linux ([fedora](http://fedoraproject.org/)) machines. The error I was getting was:

**ld: duplicate symbol \_g\_bit\_nth\_lsf in foo.o and bar.o**

I am running Leopard 10.5.3. I was using glib2, installed via [Fink](http://www.finkproject.org/), version number: 2.12.0-103. After spending lots of time googling I found the following article to be of the most use, [&#8220;Wireshark with Macports&#8221;](http://www.anders.com/cms/241/Wireshark/MacPorts), where Anders Brownworth pointed out that the error was due to a &#8220;[extern inline bug in glib/gutils.h which is easily fixed](http://trac.macosforge.org/projects/macports/ticket/13006)&#8220;.

So to fix this:

  * I located **gutils.h**, which I found here: 
    /sw/include/glib-2.0/glib/gutils.h</li> 
    
      * I then replaced these lines: 
        `#ifdef G_IMPLEMENT_INLINES</p>
<p>#  define G_INLINE_FUNC</p>
<p>#  undef  G_CAN_INLINE</p>
<p>#elif defined (__GNUC__)</p>
<p>#  define G_INLINE_FUNC extern inline</p>
<p>#elif defined (G_CAN_INLINE)`</li> 
        
          * With this: 
            `#ifdef G_IMPLEMENT_INLINES</p>
<p>#  define G_INLINE_FUNC</p>
<p>#  undef  G_CAN_INLINE</p>
<p><font color="red"><code>#elif defined (__APPLE__)</p>
<p>#  define G_INLINE_FUNC static inline`</font>
            
            #elif defined (\_\_GNUC\_\_) 
            
            \# define G\_INLINE\_FUNC extern inline
            
            #elif defined (G\_CAN\_INLINE)</code></li> 
            
              * By adding these two middle lines: 
                <font color="red"><b><code>#elif defined (__APPLE__)&lt;/p>
&lt;p>#  define G_INLINE_FUNC static inline</code></b></font></li> 
                
                  * The start of the fragment of code was at line number _96_ in my **gutils.h** file</ul> 
                
                Here is a link to my edited and working [gutils.h file](https://mmt.me.uk/blog/files/gutils.h).
                
                **Note 1:** I would make sure I get a copy of my original gutils.h file, as this may come in handy
                
                **Note 2:** There is a [patch](http://trac.macosforge.org/projects/macports/attachment/ticket/13006/glib2-inline.2.patch?format=raw) which one could apply to make the same changes which I have just described here. This patch follows this [ticket](http://trac.macports.org/ticket/13006). I didn&#8217;t know what to do with the patch file, so I ended up editing the file by hand:). I am guessing that is something todo with macports, mmm, nevermind, its working now.