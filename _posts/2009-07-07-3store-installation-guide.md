---
id: 3
title: 3store Installation Guide
date: 2009-07-07T17:01:14+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=3
permalink: /blog/2009/07/07/3store-installation-guide/
itsec_enable_ssl:
  - "1"
categories:
  - 3store
tags:
  - 3store
  - install
  - installation
  - linux
  - rdf
  - triplestore
---
I have put together these notes on installing [3Store](http://sourceforge.net/projects/threestore/) on linux boxes. I should thank [Dave Dupplaw](http://users.ecs.soton.ac.uk/dpd/) for his notes on installation, [this blog](http://semant.blogspot.com/2006/06/3store3.html) is also a good point of call.

## Pre-Install

Before you install [3Store](http://sourceforge.net/projects/threestore/) you must ensure that you have raptor and rasqal libraries installed. You should install these from source! This is not a necessity but what we have found  
it best after a number of installations.

[Rasqal](http://librdf.org/rasqal/) and [Raptor](http://librdf.org/raptor/) are both libraries produced by Redland, and can be downloaded from their site: [http://librdf.org](http://librdf.org/).

Unpack each tar ball, configure, make, and make install each one.

Rasqal and Raptor both install their package files into _/usr/local/lib/pkgconfig_g but 3Store does not expect the files there. To fix this set the environment variable **PKG\_CONFIG\_PATH** to point to that directory. If that directory does not exist, locate _rascal.pc_ to find its location and place that path in your **PKG\_CONFIG\_PATH** environment variable. For example, on a 64 bit architecture, these files should be found in _/usr/local/lib64/pkgconfig_.

In _[t]csh_ this is:

`setenv PKG_CONFIG_PATH /usr/local/lib/pkgconfig/`

In _bash_ this is:

`export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig/`

It should be noted that 3store also requires [glib](http://sourceforge.net/projects/unicode-glib), as well as the Berkeley DB libraries. You should be able to install these via your package manager, i.e. apt-get, yum, or through emerge.

## 3Store Installation

Installation is from source, so unpack the source and enter the 3store directory.

Use _./configure_ to configure the compilation scripts.

Make the scripts with the **make** command. Install 3Store with **make install** (you will have to be root to do this).

## Troubleshooting

### Package rascal.pc does not exist

If you get this error:

_checking for RASQAL&#8230; Package rasqal was not found in the pkg-config  
search path._

Perhaps you should add the directory containing _rasqal.pc_ to the 

**PKG\_CONFIG\_PATH** environment variable.

Other issue:

_No package &#8216;rasqal&#8217; found configure: error: Package requirements (rasqal >= 0.9.11) were not met:_

Then check that you have correctly installed rascal and set up the **PKG\_CONFIG\_PATH** environment variable.

### Library libidn.so does not exist

If you get this error:

_gcc: /usr/lib/libidn.so: No such file or directory_

Then locate _libidn_ and make a soft link to the necessary library.  
For example, if _libidn.so.11_ exists, link it to the filename _libidn.so_:

`ln -s /usr/lib/libidn.so.11 /usr/lib/libidn.so`

The make script will then be able to find the file.

### glibc 386 libraries missing RedHat

If you are working on x86 platform, you may still require the i386 libraries to do  
the compilation. This error may be typified by the following error message during compilation:

_/usr/bin/ld: crti.o: No such file: No such file or directory_

It is easiest if you are signed up to the [RedHat network](https://rhn.redhat.com/help/about.pxt) to do update your glibc libraries to the latest versions:

`up2date --showall # (optional to find latest versions)`

`up2date --get glibc-devel-2.3.4-2.19.i386`

`rpm -Uvh /var/spool/up2date/glibc-devel-2.3.4-2.19.i386.rpm`

Alternatively, you can check your original discs for the **i386 glibc-devel library** rpm. RedHat Enterprise Linux comes with the i386 versions of the libraries on disc 3. Install them using the last command given above.

### Wrong Architecture/File Format

There is a bug in the [RedHat Enterprise](http://www.redhat.com/rhel/) installer that means even if you tell if not to install [MySQL](http://www.mysql.com/) it will do. Unfortunately, in either case it will install the 32 bit version, which causes an error similar to this:

_/usr/local/lib/librasqal.so: could not read symbols: File in wrong format_

If this is the case, you need to ensure that the compilation knows where your 64-bit MySQL installation is. If you do not have one you will have to download an appropriate version (or build from source).

The installation works by calling the mysql-config script which tells the compilation how to compile-in the MySQL libraries. To make it work, ensure that the script in your path is the correct version:

In **[t]csh**:

`setenv PATH /usr/local/mysql/bin:${PATH}`

Or in **bash**:

`export PATH=/usr/local/mysql/bin:$PATH`

### Libraries not found

When you run a 3store tool (e.g. ts-query) you get a message similar to the following:

ts-query: error while loading shared libraries: lib3store.so.0: cannot open shared object file: No such file or directory

This means the 3Store tool cannot find the 3Store libraries. You can locate lib3store to find the location of the libraries (which by default are put into _/usr/local/lib_) and add this to your **LD\_LIBRARY\_PATH**:

In **[t]csh**:

`setenv LD_LIBRARY_PATH /usr/local/lib`

Or in **bash**:

`export LD_LIBRARY_PATH=/usr/local/lib`

Better still, you should add this path to your ld configuration so that it will always  
work. To do this create a new file in _/etc/ld.so.conf.d/_ called _3store.conf_. Put _/usr/local/lib_ on its own at the top of the file. Save it, and run **/sbin/ldconfig**, to update your configuration. The tools should now be able to find the libraries, and will be able to for anyone who uses the machine.

This is fixed in another manner if you are using [Gentoo Linux](http://www.gentoo.org). There is no _/etc/ld.so.conf.d/_ directory. In gentoo you should add the path to the  
**LDPATH** environment variable (not **LD\_LIBRARY\_PATH**!), this can be done like so:

Edit _/etc/env.d/00basic_

And add the LIBDIR to the line:

`LDPATH="/usr/local/lib"`

On a 64 bit architecture it may look like so:

`LDPATH="/usr/local/lib:/usr/local/lib64"`

Then make sure you run the **env-update** script in gentoo.

### Berkeley DB library not found

So if you get the following error during the configure process.

**&#8220;configure: error: Cannot find Berkeley DB library version 4&#8243;**

You either don&#8217;t have the Berkeley DB libraries installed, or there are not where 3store expects them to be.

If you don&#8217;t have it installed, grab it and cd to the directory, then:

`cd build_unix<br />
../dist/configure`

`make<br />
sudo make install`

So now, if you are in the position where you have Berkeley DB 4 installed, but you are still getting the above error then 3Store is assuming it is somewhere which it isn&#8217;t! So now we have to make a soft link from where the _db.h_ file actually resides, and where 3store thinks it should be.

`su<br />
mkdir /usr/include/db4<br />
cd /usr/include/db4<br />
ln -s /usr/local/BerkeleyDB.4.5/include/db.h<br />
./configure LDFLAGS=-L/usr/local/BerkeleyDB.4.5/lib`

If you are using a version 4.5 or above of Berkeley DB, you make have to edit the configure script as follows:

Edit line 21151, which looks like so:

`for ac_lib in db-4.4 db-4.3 db-4.2 db-4.1 db; do`

and add your version of db to it, like so:

`for ac_lib in <b>db-4.5</b> db-4.4 db-4.3 db-4.2 db-4.1 db; do`

And now you should be able to make and make install.

### Problems during compilation &#8220;make&#8221;

If you had problems with the configure script and Berkeley DB, then you may have to edit some on the source code in the _src_ directory. In order to get it to work I have had to:

Change the source code and which had `#include <db.h>` to `#include<<b>PATHTO</b>/db.h>`

This had to be done in the following files:

**Datatypes.h</p> 

Bulkimport.c</b>

## Problems with ts-util!

If you are having problems when running the command:

`ts-util optimise "KBNAME"`

You will have to edit line number 164 in ts-util.c in the src directory, and recompile.

Line 164 is missing an &#8220;AND&#8221;, and should look like so

`ts_mysql_query(c->db, "DELETE FROM "T_S" WHERE NOT EXISTS (SELECT * FROM "T_T" WHERE model=hash) AND NOT EXISTS (SELECT * FROM "T_T" WHERE subject=hash) AND NOT EXISTS (SELECT * FROM "T_T" WHERE predicate=hash) AND NOT EXISTS (SELECT * FROM "T_T" WHERE object=hash)");`
