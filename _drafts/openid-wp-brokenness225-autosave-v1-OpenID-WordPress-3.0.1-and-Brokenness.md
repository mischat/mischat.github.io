---
id: 229
title: OpenID, WordPress 3.0.1 and Brokenness
date: 2010-08-20T12:24:36+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/08/20/225-autosave/
permalink: /2010/08/20/225-autosave-v1/
---
So, I am officially super annoyed with both [OpenID](http://openid.net/) and with [WordPress](http://wordpress.org/) right now. There is a bug in the OpenID plugin developed by the [Diso project](http://code.google.com/p/diso/) (thanks guys), I have been using this plugin for a while now, but it seems very broken at the moment. 

I have managed to get my OpenID server working, my OpenID URI being <https://mmt.me.uk/blog/>, but I have yet (after hours of trying), managed to get OpenID commenting fixed on my blog. 

So my apologies if you try and comment on my blog using your OpenID, as it doesn&#8217;t work.

The most annoying thing about this whole issue is the fact that I get perhaps the least helpful error message ever. The following error message pops up when I attempt to use my colleagues OpenID to post a comment to one of my articles, this following error message gets sent to my STERR :

`[Fri Aug 20 12:01:14 2010] [error] [client XXX.XXX.XXX.XXX] Successfully fetched 'http://steve.harris.name/': GET response code 200, referer: https://mmt.me.uk/blog/2010/07/30/the-facebook-like-button/`

&#8220;200, and Successfully fetched!&#8221; my ass!

In order to get the OpenID server working I had to apply a [patch](http://code.google.com/p/diso/issues/detail?id=161), which has been raised as a ticket on the diso project issue tracker. In short, there are two required changes, due to PHP 5.3 funkiness, required to make the OpenID server work.

These couple of changes to the OpenID libraries which came with my version of WordPress is due to the fact that PHP 5.3 has clamped down on the returning of values when expecting a reference to be returned by a function, this phenomena was illustrated in the following errors : 

`<br />
[Sun Apr 18 23:40:05 2010] [error] [client 140.203.155.13] PHP Warning:  Parameter 1 to Auth_OpenID_Server::openid_associate() expected to be a reference, value given in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1702<br />
[Sun Apr 18 23:40:05 2010] [error] [client 140.203.155.13] PHP Fatal error:  Call to a member function needsSigning() on a non-object in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1495<br />
[Sun Apr 18 23:40:06 2010] [error] [client 78.86.167.133] PHP Warning:  Parameter 1 to Auth_OpenID_CheckIDRequest::fromMessage() expected to be a reference, value given in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1576, referer: http://apassant.net/blog/2010/04/18/sparql-pubsubhubbub-sparqlpush?destination=node%2F374<br />
[Sun Apr 18 23:49:36 2010] [error] [client 193.203.240.209] PHP Warning:  Parameter 1 to Auth_OpenID_Server::openid_associate() expected to be a reference, value given in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1702<br />
[Sun Apr 18 23:49:36 2010] [error] [client 193.203.240.209] PHP Fatal error:  Call to a member function needsSigning() on a non-object in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1495<br />
[Sun Apr 18 23:49:52 2010] [error] [client 193.203.240.209] PHP Warning:  Parameter 1 to Auth_OpenID_Server::openid_associate() expected to be a reference, value given in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1702<br />
[Sun Apr 18 23:49:52 2010] [error] [client 193.203.240.209] PHP Fatal error:  Call to a member function needsSigning() on a non-object in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1495<br />
[Sun Apr 18 23:50:27 2010] [error] [client 216.97.225.85] PHP Warning:  Parameter 1 to Auth_OpenID_Server::openid_associate() expected to be a reference, value given in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1702<br />
[Sun Apr 18 23:50:27 2010] [error] [client 216.97.225.85] PHP Fatal error:  Call to a member function needsSigning() on a non-object in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1495<br />
[Sun Apr 18 23:50:28 2010] [error] [client 78.86.167.133] PHP Warning:  Parameter 1 to Auth_OpenID_CheckIDRequest::fromMessage() expected to be a reference, value given in /media/data/www/mmtmeuk/public_html/blog/wp-content/plugins/openid/Auth/OpenID/Server.php on line 1576, referer: http://www.pillwatch.com/proc_openid-login.php<br />
` 

There is a page which describes the patch one needs to run to overcome this: 

<http://patchlog.com/wp-content/uploads/2009/11/openid-server-php.5.3.diff>

I need to get on with other stuff now, will revisit this in the future &#8230;