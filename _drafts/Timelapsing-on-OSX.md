---
id: 563
title: Timelapsing on OSX
date: 2011-12-30T15:00:09+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=563
permalink: /?p=563
categories:
  - Uncategorized
---
ffmpeg -threads 4 -i &#8216;DSC_%16d.jpg&#8217; -r 25 -s vga -vcodec libx264 ../lame.mp4

ffmpeg -threads 4 -i &#8216;%016d.jpg&#8217; -r 25 -s vga -vcodec libx264 ../lame.mp4

you need to have your images numbered  
like %016d  
which is 16 digit number starting 1  
i.e. 000&#8230;.01

I am using exiftool instead of imagemagick, it seems to compile and work on my mac

exiftool -b -JpgFromRaw foo.NEF > foo.NEF.jpg

ffmpeg -threads 4 -i &#8216;%016d.jpg&#8217; -r 7 -s vga -vcodec libx264 ../lame2.mp4

#!/usr/bin/perl -w

$files = \`ls -s\`;  
$count = 1;

while ($files =~ m/\s(DSC.*jpg)\s/g) {  
$filename = sprintf(&#8220;%016d&#8221;, $count);  
\`mv &#8216;$1&#8217; $filename.jpg\`;

$count++;  
}

\# vi:set expandtab sts=4 sw=4:  
~  
~  
~  
~  
~