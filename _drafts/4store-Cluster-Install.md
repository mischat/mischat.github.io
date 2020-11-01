---
id: 501
title: 4store Cluster Install
date: 2011-11-07T13:48:33+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=501
permalink: /?p=501
categories:
  - Uncategorized
---
So, 

Step one install the 4store dependencies excluding libraptor and librasqal via yum

from HIVE: 

cat vms.txt | pdsh -R ssh -w &#8211; &#8220;yum install gcc glib2-devel libxml2-devel  
pcre-devel avahi avahi-devel avahi-glib-devel readline-devel ncurses-devel  
termcap libtermcap-devel libtool expat-devel zlib-develi avahi-tools&#8221;

checked if avahi was on: 

[root@hive ~]# cat vms.txt | pdsh -R ssh -w &#8211; &#8220;/sbin/chkconfig &#8211;list | grep  
avahi&#8221;  
black: avahi-daemon 0:off 1:off 2:on 3:on 4:on 5:on 6:off  
red: avahi-daemon 0:off 1:off 2:on 3:on 4:on 5:on 6:off  
blue: avahi-daemon 0:off 1:off 2:on 3:on 4:on 5:on 6:off  
gold: avahi-daemon 0:off 1:off 2:on 3:on 4:on 5:on 6:off  
green: avahi-daemon 0:off 1:off 2:on 3:on 4:on 5:on 6:off

All on all machines : 

wget http://download.librdf.org/source/rasqal-0.9.27.tar.gz  
wget http://download.librdf.org/source/raptor2-2.0.4.tar.gz  
./configure make make install  
make sure you set: PKG\_CONFIG\_PATH=/usr/local/lib/pkgconfig when compiling

This is what you need to see post compiling 4store to ensure cluster support :  
Configuration status:  
Found mDNS libraries, cluster suport enabled  
Using Raptor version 2.0.4  
Using Rasqal version 0.9.27

At this point I would suggest that your sys admin setups up an nfs share on  
blue&#8217;s (your master server&#8217;s) /usr/local and mount it as read/only via nfs  
for all the other &#8220;slave nodes&#8217;s&#8221; /usr/local. This way all you need to do  
it update 4store on one machine. This should be an easy task for someone  
to do. 

I have created a 4store user, and have used the ssh keys i pinched from the  
root user. You guys probably want to remove the .ssh key infrastructure of the  
root users, these are not necessary. I was using these to debug early on. 

All of the 4s-cluster-* commands use ssh to execute commands, please use to  
4store user, not root when creating and starting up KBs. 

You can install a new kb like so : 

4s-cluster-create foo  
I would go for &#8211;segments 16 like so  
4s-cluster-create &#8211;segments 16 foo (given the number of cores in your setup)  
The above command creates the relevant directories in /var/lib/4store/

And then to start the backends please run: 

4s-cluster-start foo

and 

4s-cluster-stop foo 

respectively. 

I have set up a couple of KBs, one which has my foaf file in it &#8220;test&#8221;  
and one called sampledata &#8220;as per email instruction&#8221;. test has a SPARQL  
endpoint on http://blue:8080/ and the sampledata is running on port 8081/.

Details of interacting with the SPARQL Server can be found here:  
http://4store.org/trac/wiki/SparqlServer

When importing big files I suggest stopping the 4s-httpd and using the  
4s-import command line client.

[4store@blue ~]$ cd /sampledata  
[4store@blue sampledata]$ 4s-cluster-create sampledata  
0: red:  
4store[15897]: backend-setup.c:185 erased files for KB sampledata  
4store[15897]: backend-setup.c:310 created RDF metadata for KB sampledata  
1: green:  
4store[16390]: backend-setup.c:185 erased files for KB sampledata  
4store[16390]: backend-setup.c:310 created RDF metadata for KB sampledata  
2: black:  
4store[3776]: backend-setup.c:185 erased files for KB sampledata  
4store[3776]: backend-setup.c:310 created RDF metadata for KB sampledata  
3: gold:  
4store[21429]: backend-setup.c:185 erased files for KB sampledata  
4store[21429]: backend-setup.c:310 created RDF metadata for KB sampledata  
[4store@blue sampledata]$ 4s-cluster-start sampledata  
0: red:  
1: green:  
2: black:  
3: gold:  
[4store@blue sampledata]$ 4s-import -vv -M http://data.linkedct.org/ -f  
ntriples sampledata /sampledata/linkedct-dump-latest.nt  
removing old data  
Reading <file:///sampledata/linkedct-dump-latest.nt>  
into <http://data.linkedct.org/>  
Pass 1, processed 5000000 triples (5000000)  
Pass 2, processed 5000000 triples, 147170 triples/s  
Pass 1, processed 4809330 triples (9809330)  
Pass 2, processed 4809330 triples, 169100 triples/s  
Updating index  
Index update took 1.917708 seconds  
Imported 9809330 triples, average 154460 triples/s  
….  
Reading <file:///sampledata/diseasome_dump.nt>  
into <http://www4.wiwiss.fu-berlin.de/diseasome/>  
Pass 1, processed 91182 triples (91182)  
Pass 2, processed 91182 triples, 142086 triples/s  
Index update took 0.090085 seconds  
Imported 91182 triples, average 126918 triples/s

In order to check whether avahi is working properly when setting up your  
cluster please run: 

avahi-browse -tv \_4store.\_tcp 

the output should look like so : 

Server version: avahi 0.6.25; Host name: hive.local  
E Ifce Prot Name Type Domain  
+ virbr0 IPv4 gold-sampledata \_4store.\_tcp local  
+ virbr0 IPv4 black-sampledata \_4store.\_tcp local  
+ virbr0 IPv4 green-sampledata \_4store.\_tcp local  
+ virbr0 IPv4 red-sampledata \_4store.\_tcp local  
+ virbr0 IPv4 gold-test \_4store.\_tcp local  
+ virbr0 IPv4 black-test \_4store.\_tcp local  
+ virbr0 IPv4 green-test \_4store.\_tcp local  
+ virbr0 IPv4 red-test \_4store.\_tcp local  
+ eth2 IPv4 macallan-triplestorebenchmark \_4store.\_tcp local  
+ eth2 IPv4 lagavulin.entagensystems.com-olamasterindex \_4store.\_tcp local  
+ eth2 IPv4 macallan-hugotriplestore \_4store.\_tcp local  
: Cache exhausted  
: All for now