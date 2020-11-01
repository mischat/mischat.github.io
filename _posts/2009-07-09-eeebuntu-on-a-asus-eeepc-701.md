---
id: 82
title: EEEbuntu on a ASUS EEEpc 701
date: 2009-07-09T12:18:15+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=82
permalink: /2009/07/09/eeebuntu-on-a-asus-eeepc-701/
itsec_enable_ssl:
  - "1"
categories:
  - linux
---
I have recently been given a [ASUS EEEpc 701](http://en.wikipedia.org/wiki/ASUS_Eee_PC), thanks [swh](http://plugin.org.uk/swh.xrdf#me), and have till now found it way too slow and jerky. The 701 I have has got 1G of RAM and 4G of disk space built in, which I added a 16G flash disk too.

Thanks to [Seb](http://oneshare.ecs.soton.ac.uk/people/) (old housemate), I have now downgraded the graphics driver, and as a result it is now totally usable, yay to small computers!! I followed this [howto guide](http://digitalpatch.blogspot.com/2009/06/story.html) when attempting to fix the EeeeeePc.

These are the steps I took : 

1. Edited and added the below lines to : /etc/apt/sources.list:  
`<br />
 deb http://ppa.launchpad.net/siretart/ppa/ubuntu jaunty main<br />
 deb-src http://ppa.launchpad.net/siretart/ppa/ubuntu jaunty main<br />
` 

2. Imported the needed key:  
`<br />
 sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 0xce90d8983e731f79<br />
` 

3. Installed the older driver:  
`<br />
 $ sudo apt-get update<br />
 $ sudo apt-get install xserver-xorg-video-intel-2.4<br />
` 

4. Restarted X.  
`<br />
sudo /etc/init.d/gdm restart<br />
` 

And then, like magic a usable working [EEEbuntu](http://eeebuntu.org/) on the 701. Notes that I tend to install [Fedora OSs](http://fedoraproject.org/) on my machines, this is the first time I have decided to stick with an Ubuntu flavoured OS.