---
id: 348
"comments: true"
title: 'NQUADS -> TRIG &#8230; A Noddy Perl Script'
date: 2010-10-22T16:18:50+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=348
permalink: /blog/2010/10/22/nquads-to-trig/
itsec_enable_ssl:
  - "1"
categories:
  - SemanticWeb
tags:
  - nquads
  - parser
  - perl
  - rdf
  - trig
---
I keep coming across [nquads](http://sw.deri.org/2008/07/n-quads/) files, and [libraptor](http://librdf.org/raptor/) doesn&#8217;t support this serialisation, it only supports quad-based [TriG format](http://www4.wiwiss.fu-berlin.de/bizer/TriG/). I knocked together a dirty perl file which will parse a [nquads](http://sw.deri.org/2008/07/n-quads/) file to TriG if ever need be.

You can find the perl file on my site : 

[https://mmt.me.uk/blog/examples/perl/nquads\_to\_trig.pl](https://mmt.me.uk/blog/examples/perl/nquads_to_trig.pl)

`<br />
#!/usr/bin/perl<br />
use strict;</p>
<p>my $files = scalar(@ARGV);<br />
if ($files != 1) {<br />
    &nbsp;&nbsp;print "NQuads importer. ./nquads_importer nquads_file\n";<br />
    &nbsp;&nbsp;exit();<br />
}</p>
<p>my $input_filename = @ARGV[0];</p>
<p>open (INPUT,$input_filename) || die { print "Input file does not exist\n"};<br />
open (OUTPUT,">$input_filename.trig") || die { print "Failed to open output file\n"};</p>
<p>my $line = "";<br />
my $model_uri = "";<br />
my $triple = "";<br />
my $count = 0;<br />
my %quads = ();</p>
<p>while (<INPUT>) {<br />
    &nbsp;&nbsp;$line = $_;<br />
    &nbsp;&nbsp;if ($line =~ m/^(.*?)(<[^>]+>?)\s*\.$/) {<br />
        &nbsp;&nbsp;&nbsp;$model_uri = $2;<br />
        &nbsp;&nbsp;&nbsp;$triple = $1.".\n";</p>
<p>        &nbsp;&nbsp;&nbsp;$quads{$model_uri} .= $triple;</p>
<p>    &nbsp;&nbsp;} else {<br />
       &nbsp;&nbsp;&nbsp;print ERROR "boo this nquad doesn't pass regex\n$line\n*************\n";<br />
   &nbsp;&nbsp; }<br />
   &nbsp;&nbsp;$count++;<br />
}</p>
<p>foreach my $forth (keys %quads) {<br />
    &nbsp;&nbsp;print OUTPUT "$forth { ".$quads{$forth}." }\n";<br />
}</p>
<p>print "Finished\n";<br />
close(INPUT);<br />
close(OUTPUT);</p>
<p># vi:set ts=8 sts=4 sw=4 et:<br />
`
