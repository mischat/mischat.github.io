---
id: 366
title: 'Catch all email address &#8230;.'
date: 2010-11-02T17:03:04+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=366
permalink: /?p=366
categories:
  - Uncategorized
---
In Jaguar server, the GUI admin tool had a section to add an account for all email to be sent if the user did not exist. This feature is not part of Panther Server. After much trial and error, and many readings of many forums, I figured out a simple, if annoying way to do this.

1. As root, vi /etc/postfix/main.cf and include the following line (I put mine at the bottom of the file):

virtual\_alias\_maps = hash:/etc/postfix/virtual

2. As root, vi /etc/postfix/virtual and add the following:

###########  
\# local users  
###########  
localUser1@domain.com localUser1  
localUser2@domain.com localUser2  
localUser3@domain.com localUser3  
localUser4@domain.com localUser4

##########  
\# catch-all  
##########  
@domain.com catch-all

I put this at the top above the comments. You must include all local users or the catch-all account will get all mail. localUser# is used in place of the actual user account name for local users. catch-all is used in place of the account you designate as the catch-all. domain.com is used in place of your domain name. There are tabs between the entries on each line. There is a caveat &#8212; if you create an alias, that email will go to the catch-all account as well as to the aliased accounts.

3. As root, run postmap /etc/postfix/virtual

4. As root, run postfix reload