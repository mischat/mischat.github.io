---
id: 27
title: Timemachine to a Linux Box
date: 2009-07-07T18:22:11+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=27
permalink: /blog/2009/07/07/timemachine-to-a-linux-box/
itsec_enable_ssl:
  - "1"
categories:
  - OSX
---
By default [TimeMachine](http://www.apple.com/macosx/features/timemachine.html) on [Mac OSX](http://www.apple.com/macosx/) is configured to run through the [Apple Filing Protocol](http://en.wikipedia.org/wiki/Apple_Filing_Protocol) only. 

At home I run a backup server for Time Machine on one of my Linux boxes, I did this by enabling the following feature on the machine which I have configured to be backed up. 

`defaults write com.apple.systempreferences TMShowUnsupportedNetworkVolumes 1` 

This in turn allows for unsupported network volumes to be used as backup volumes. 

Below are some other Apple related preferences I have configured on my macbook:

`defaults write com.apple.dock persistent-others -array-add '{ "tile-data" = { "list-type" = 1; }; "tile-type" = "recents-tile"; }'`

`defaults write com.apple.terminal FocusFollowsMouse -string YES`

`defaults write com.apple.Safari IncludeDebugMenu 1`

`defaults write com.apple.finder AppleShowAllFiles Yes (ALL FILES IN FINDER)`
