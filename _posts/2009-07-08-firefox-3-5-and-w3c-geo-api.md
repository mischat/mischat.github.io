---
id: 60
title: Firefox 3.5 and W3C Geo API
date: 2009-07-08T13:09:29+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=60
permalink: /2009/07/08/firefox-3-5-and-w3c-geo-api/
itsec_enable_ssl:
  - "1"
categories:
  - FOAF
  - Lifelogging
  - SemanticWeb
tags:
  - firefox
  - FOAF
  - foafevent
  - geo
  - personscrobble
  - rdf
  - w3c
---
I have made a simple webpage which makes use of the [W3C Geo API](http://dev.w3.org/geo/api/spec-source.html). The page will prompt you for your location, given you are using FF3.5, and will subsequently ask you for a WebID and some text to describe what you are up to.

The service then generates a call to another [endpoint](https://mmt.me.uk/blog/services/FOAFEvent) I bashed together, that takes the following cgi arguements.  
`<br />
webid -  lat - long with an OPTIONAL alt - datetime - doing(what I am doing now field)<br />
`  
e.g.,  
`<br />
https://mmt.me.uk/blog/services/FOAFEvent?lat=51.4583494&long=-0.1186444&webid=http://foo.com/foaf.rdf%23bar&datetime=2009-07-08T13:02:46+01:00&doing=writing+a+blog+article<br />
`  
That in turn generates a _FOAF person scrobble_, or a FOAF Event. I have made us of the [Event](http://purl.org/NET/c4dm/event.owl#), [Timeline](http://purl.org/NET/c4dm/timeline.owl#), [FOAF](http://xmlns.com/foaf/0.1/), [dc](http://purl.org/dc/elements/1.1/), and the [Geo](http://www.w3.org/2003/01/geo/wgs84_pos#) ontologies. 

So this service can be found on my site, <https://mmt.me.uk/blog/geo>. It should be noted that I **DO NOT** store any of the information which I output on this site. I will make it HTTPS at some point, and then I will replace using [Plazes.com](http://plazes.com/) with my own service. I would rather a world where I was running all of my own social networking from my own machine.

The code to do this is so simple. In order to do the W3C geo stuff all you need to do is write some html and javascript, like so (sorry about the indentation)  
`<br />
<script src="http://maps.google.com/maps?file=api&v=2&key=YOUR_API_KEY_HERE" type="text/javascript"></script><br />
<script type="text/javascript"><br />
        function load() {<br />
                navigator.geolocation.getCurrentPosition(showMap);<br />
        }<br />
      function showMap(position.coords) {<br />
                // (position.coords.latitude, position.coords.longitude).<br />
                if (GBrowserIsCompatible()) {<br />
                        var map = new GMap2(document.getElementById("map"));<br />
                        map.setCenter(new GLatLng(position.coords.latitude, position.coords.longitude), 13);<br />
                        var point = new GLatLng(position.coords.latitude, position.coords.longitude);<br />
                        map.addOverlay(new GMarker(point));<br />
                }<br />
        }<br />
</script><br />
<div id="map" style="width: 620px; height: 310px"></div><br />
`  
and this :  
`<br />
<body onload="load()" onunload="GUnload()"><br />
` 

Here are a bunch of links which I used to find out how to do this : 

  * <http://www.skyhookwireless.com/whoweare/privacypolicy.php> 
  * <http://dev.w3.org/geo/api/spec-source.html> 
  * <http://ajaxian.com/archives/navigatorgeolocation-using-the-w3c-geolocation-api-today> 
  * <http://www.tralfamadore.com/2008/08/w3c-geolocation-api-on-iphone-with.html> 
  * <http://almaer.com/blog/using-the-w3c-geolocation-api-specification-today-extending-whereareyou> 
  * <https://developer.mozilla.org/En/Using_geolocation>