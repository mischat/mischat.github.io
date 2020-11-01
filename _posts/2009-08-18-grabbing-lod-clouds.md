---
id: 92
title: Grabbing LOD clouds
date: 2009-08-18T10:57:09+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=92
permalink: /2009/08/18/grabbing-lod-clouds/
itsec_enable_ssl:
  - "1"
categories:
  - SemanticWeb
---
I have been looking for a set of links for all of the (Linked Open Data) LOD clouds so that I could have a pictorial description of how the LOD cloud has evolved since it was first assembled. Sadly there are no links to the old LOD clouds on from the [LOD cloud&#8217;s home on the web](http://richard.cyganiak.de/2007/10/lod/).

So I hacked together a dirty perl script to see if I could guess the URLs for the old clouds, the code looks like so :  
`<br />
#!/usr/bin/perl`

$rootUrl = &#8216;http://richard.cyganiak.de/2007/10/lod/&#8217;;

#now to brute force the URL mangling to grab all of the pictures

for ($i = 2007 ; $i < 2010; $i++) {  
for ($j = 1 ; $j < 13; $j++) {  
for ($k = 1; $k < 32; $k++) {  
$stringToFetch = $rootUrl.&#8221;lod-datasets\_$i-&#8220;.make\_big($j).&#8221;-&#8220;.make_big($k).&#8221;.png&#8221;;

\`wget $stringToFetch\`;

}  
}  
}

#padding out string &#8230;  
sub make_big($) {  
my $string = shift;  
if (length($string) == 1) {  
$string = &#8220;0&#8221;.$string;  
}  
return $string;  
}

After running the script I have found the following old instances of the LOD cloud :

  * <http://richard.cyganiak.de/2007/10/lod/lod-datasets_2007-10-08.png>
  * <http://richard.cyganiak.de/2007/10/lod/lod-datasets_2007-11-07.png>
  * <http://richard.cyganiak.de/2007/10/lod/lod-datasets_2007-11-10.png>
  * <http://richard.cyganiak.de/2007/10/lod/lod-datasets_2008-02-28.png>
  * <http://richard.cyganiak.de/2007/10/lod/lod-datasets_2008-03-31.png>
  * <http://richard.cyganiak.de/2007/10/lod/lod-datasets_2009-07-14.png>

Finally, I still don&#8217;t think I have the first LOD cloud, would love to know its URL if anyone out there knows it!