---
id: 138
comments: true
title: Compiling 4store on a Fedora 12 box
date: 2009-12-14T14:40:16+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=138
permalink: /blog/2009/12/14/compiling-4store-on-a-fedora-12-box/
itsec_enable_ssl:
  - "1"
categories:
  - 4store
tags:
  - 4store
  - fedora
  - ld.so.conf
  - ldd
  - librasqal
  - linux
---
I was attempting to install [4store](http://4store.org/) on my fedora 12 box, and I found that I couldn&#8217;t run the tests which are shipped with 4store. I got the following output when attempting to run &#8220;make test&#8221; :

``<br />
[root@blanket 4store]# make test<br />
(cd tests && make -w test)<br />
make[1]: Entering directory `/usr/local/src/4store/tests'<br />
(cd query && pwd && ./setup.sh --autorun)<br />
/usr/local/src/4store/tests/query<br />
4store[9702]: backend-setup.c:176 erased files for KB query_test_mmt04r<br />
4store[9702]: backend-setup.c:301 created RDF metadata for KB query_test_mmt04r<br />
../../src/frontend/4s-import: error while loading shared libraries: librasqal.so.1: cannot open shared object file: No such file or directory<br />
Preparing for tests...<br />
../../src/frontend/4s-delete-model: error while loading shared libraries: librasqal.so.1: cannot open shared object file: No such file or directory<br />
[FAIL] add-and-delete<br />
[FAIL] distinct-predicate<br />
[FAIL] foaf-all-limit<br />
[FAIL] foaf-bnode-vs-variable<br />
[FAIL] foaf-construct<br />
[FAIL] foaf-disjunctive-filter<br />
[FAIL] foaf-distinct<br />
[FAIL] foaf-graph-all<br />
[FAIL] foaf-graph-pred<br />
[FAIL] foaf-knows-name<br />
[FAIL] foaf-knows-name-sha1<br />
[FAIL] foaf-knows-sha1<br />
[FAIL] foaf-knows-sha1-xml<br />
[FAIL] foaf-multi-disjunctive-filter<br />
[FAIL] foaf-nested-optional<br />
[FAIL] foaf-nothing<br />
[FAIL] foaf-optional-order<br />
[FAIL] foaf-optional-pair<br />
[FAIL] foaf-optional-regex<br />
[FAIL] foaf-repeat-var<br />
[FAIL] graphs<br />
[PASS] integrity<br />
[FAIL] null-optional<br />
[FAIL] null-optional-double<br />
[FAIL] optimiser-disjunction<br />
[FAIL] select-bnodes<br />
[FAIL] select-order<br />
[FAIL] select-unused<br />
[FAIL] size<br />
[FAIL] tiger-broadway<br />
[FAIL] tiger-explosion<br />
[FAIL] tiger-fail-optional<br />
[FAIL] tiger-harold-ave<br />
[FAIL] tiger-landmarks<br />
[FAIL] tiger-mixed-optional<br />
[FAIL] tiger-reverse<br />
[FAIL] tiger-sugar-hill<br />
[FAIL] tiger-sugar-hill-filter<br />
[FAIL] tiger-typical<br />
[FAIL] tiger-water-names<br />
Tests completed: passed 1/40 (39 fails)<br />
make[1]: Leaving directory `/usr/local/src/4store/tests'<br />
`` 

This struck me as odd given that when I ran the &#8220;configure&#8221; script I got the following output :  
`<br />
[root@blanket 4store]# ./configure<br />
[OK  ] pkg-config installed<br />
[OK  ] raptor installed<br />
[OK  ] rasqal installed<br />
[OK  ] glib2 installed<br />
[OK  ] libxml2 installed<br />
[OK  ] pcre installed<br />
[OK  ] ncurses installed<br />
[OK  ] readline installed<br />
[OK  ] z installed<br />
[OK  ] avahi installed<br />
` 

So these are the setup step which I had to perform in order to get 4store working and running the tests: 

**1. After compiling the code, used ldd to see which libs were missing**  
`<br />
ldd src/frontend/4s-query<br />
[root@blanket 4store]# ldd !$2<br />
ldd src/frontend/4s-query<br />
	linux-gate.so.1 =>  (0x00d9a000)<br />
	librasqal.so.1 => not found<br />
	libraptor.so.1 => /usr/lib/libraptor.so.1 (0x00678000)<br />
	libxml2.so.2 => /usr/lib/libxml2.so.2 (0x04f2f000)<br />
	libavahi-common.so.3 => /usr/lib/libavahi-common.so.3 (0x051d0000)<br />
	libavahi-client.so.3 => /usr/lib/libavahi-client.so.3 (0x051bd000)<br />
	libavahi-glib.so.1 => /usr/lib/libavahi-glib.so.1 (0x004b8000)<br />
	libglib-2.0.so.0 => /lib/libglib-2.0.so.0 (0x00da9000)<br />
	libpcre.so.0 => /lib/libpcre.so.0 (0x00110000)<br />
        ....<br />
`  
**  
2. Fix my ld.so configuration. The issue was that I had to add the following line, which points to my librasqal.so.1, to the following empty file  
/etc/ld.so.conf.d/local.conf :**  
`<br />
/usr/local/lib<br />
` 

A big yay to working 4store :  
``<br />
[root@blanket 4store]# make test<br />
(cd tests && make -w test)<br />
make[1]: Entering directory `/usr/local/src/4store/tests'<br />
(cd query && pwd && ./setup.sh --autorun)<br />
/usr/local/src/4store/tests/query<br />
4store[10887]: backend-setup.c:176 erased files for KB query_test_mmt04r<br />
4store[10887]: backend-setup.c:301 created RDF metadata for KB query_test_mmt04r<br />
removing old data<br />
Reading <file:///usr/local/src/4store/tests/query/../../data/swh.xrdf><br />
   into <http://example.com/swh.xrdf><br />
Pass 1, processed 63 triples (63)<br />
Reading <file:///usr/local/src/4store/tests/query/../../data/tiger/TGR06001.nt><br />
   into <http://example.com/TGR06001.nt><br />
Pass 1, processed 764610 triples (764547)<br />
Reading <file:///usr/local/src/4store/tests/query/../../data/nasty.ttl><br />
   into <http://example.com/nasty.ttl><br />
Pass 1, processed 764658 triples (48)<br />
Pass 2, processed 764658 triples, 26769 triples/s<br />
Updating index<br />
Index update took 17.133335 seconds<br />
Imported 764658 triples, average 19375 triples/s<br />
Preparing for tests...<br />
[PASS] add-and-delete<br />
[PASS] count<br />
[PASS] distinct-predicate<br />
[PASS] foaf-all-limit<br />
[PASS] foaf-bnode-vs-variable<br />
[PASS] foaf-construct<br />
[PASS] foaf-disjunctive-filter<br />
[PASS] foaf-distinct<br />
[PASS] foaf-graph-all<br />
[PASS] foaf-graph-pred<br />
[PASS] foaf-knows-name<br />
[PASS] foaf-knows-name-sha1<br />
[PASS] foaf-knows-sha1<br />
[PASS] foaf-knows-sha1-xml<br />
[PASS] foaf-multi-disjunctive-filter<br />
[PASS] foaf-nested-optional<br />
[PASS] foaf-nothing<br />
[PASS] foaf-optional-order<br />
[PASS] foaf-optional-pair<br />
[PASS] foaf-optional-regex<br />
[PASS] foaf-repeat-var<br />
[PASS] graphs<br />
[PASS] integrity<br />
[PASS] null-optional<br />
[PASS] null-optional-double<br />
[PASS] optimiser-disjunction<br />
[PASS] select-bnodes<br />
[PASS] select-order<br />
[PASS] select-unused<br />
[PASS] size<br />
[PASS] tiger-broadway<br />
[PASS] tiger-explosion<br />
[PASS] tiger-fail-optional<br />
[PASS] tiger-harold-ave<br />
[PASS] tiger-landmarks<br />
[PASS] tiger-mixed-optional<br />
[PASS] tiger-reverse<br />
[PASS] tiger-sugar-hill<br />
[PASS] tiger-sugar-hill-filter<br />
[PASS] tiger-typical<br />
[PASS] tiger-water-names<br />
[PASS] union-nobind<br />
Tests completed: passed 42/42 (0 fails)<br />
make[1]: Leaving directory `/usr/local/src/4store/tests'<br />
``
