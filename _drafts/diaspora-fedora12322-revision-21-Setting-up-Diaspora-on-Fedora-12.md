---
id: 347
title: Setting up Diaspora on Fedora 12
date: 2010-09-23T11:13:25+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/09/23/322-revision-21/
permalink: /2010/09/23/322-revision-21/
---
So, this has been a complete nightmare &#8230;

Install mongodb &#8230;  
I created a yum repo in 

/etc/yum.repos.d/mongodb.repo

[10gen]  
name=10gen Repository  
baseurl=http://downloads.mongodb.org/distros/fedora/12/os/i686/  
gpgcheck=0

yum install mongodb-server &#8230; 

To install disapora &#8230; 

echo &#8220;####&#8221;  
echo &#8220;Installing RVM &#8230;&#8221;  
echo &#8220;####&#8221;  
sleep 3

mkdir -p ~/.rvm/src/ && cd ~/.rvm/src && rm -rf ./rvm/ && git clone &#8211;depth 1 git://github.com/wayneeseguin/rvm.git && cd rvm && ./install

if [[ \`grep -l &#8220;rvm/scripts/rvm&#8221; $HOME/.bashrc | wc -l\` -eq 0 ]]; then  
echo &#8216;if [[ -s &#8220;$HOME/.rvm/scripts/rvm&#8221; ]] ; then source &#8220;$HOME/.rvm/scripts/rvm&#8221; ; fi&#8217; >> $HOME/.bashrc  
fi  
source $HOME/.bashrc

rvm install ruby-1.8.7-p302  
rvm &#8211;default ruby-1.8.7

pushd $DIASPORADIR && bundle install && popd

And I didn&#8217;t go with the passenger approach, instead i went with a reverse proxy &#8230;

system-config-firewall  
3000  
7001  
7002 Websockets 

I then started the diaspora, using the script/server : &#8230;  
Which started disapora on port 3000

and then i put in a reverse proxy on port 80 httpd with a virtual host :  
<VirtualHost *:80>  
ProxyRequests Off  
ServerName diaspora.mmt.me.uk  
ProxyPass / http://blanket:3000/  
ProxyPassReverse / http://blanket:3000/  
</VirtualHost>

and i also had the correct proxy related apache modules ;  
LoadModule proxy\_module modules/mod\_proxy.so  
LoadModule proxy\_balancer\_module modules/mod\_proxy\_balancer.so  
#LoadModule proxy\_ftp\_module modules/mod\_proxy\_ftp.so  
LoadModule proxy\_http\_module modules/mod\_proxy\_http.so  
#LoadModule proxy\_connect\_module modules/mod\_proxy\_connect.so

I also went by these instructiosn 

http://github.com/diaspora/diaspora/wiki/Installing-on-Ubuntu-Apache

I also had to chcron the gem&#8217;s dir  
and the public dir in the disapora dir .. 

And when I wrote the mongodb :  
mongodb 14008 0.2 0.1 73216 2816 ? Sl 19:19 0:00 /usr/bin/mongod &#8211;quiet -f /etc/mongodb.conf run

This is the selinux : setsebool -P httpd\_can\_network_connect=1

mischa@diaspora.mmt.me.uk 

I should comment on how the yum install thing they did, installs the ruby from yum, which is not the one which is needed.

I should also mention all of the symlinking which i had to do to get everything working correctly &#8230;

The mongodb stuff i used to yum install everything I got from here : 

http://www.mongodb.org/display/DOCS/CentOS+and+Fedora+Packages

mischat: http://webfinger.org/lookup/mischa@diaspora.mmt.me.uk

sofaer: Code_Bleu thin start -e production  
[23:38] sofaer: Code_Bleu thin start -e development

So i was blocked by iptables issues, but that is resovled now &#8230; 

\# Firewall configuration written by system-config-firewall  
\# Manual customization of this file is not recommended.  
*filter  
:INPUT ACCEPT [0:0]  
:FORWARD ACCEPT [0:0]  
:OUTPUT ACCEPT [0:0]  
-A INPUT -m state &#8211;state ESTABLISHED,RELATED -j ACCEPT  
-A INPUT -p icmp -j ACCEPT  
-A INPUT -i lo -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 5353 -d 224.0.0.251 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 22 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 80 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 25 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 137 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 138 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 137 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 138 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 139 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 445 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 993 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 993 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 993 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 6881 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 4662 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 4672 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 6667 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 6667 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 24800 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 24800 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 6669 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 6669 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 28017 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 28017 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 3000 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 3000 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 4080 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 4080 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 8080 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 8080 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m tcp -p tcp &#8211;dport 8008 -j ACCEPT  
-A INPUT -m state &#8211;state NEW -m udp -p udp &#8211;dport 8008 -j ACCEPT  
-A INPUT -j REJECT &#8211;reject-with icmp-host-prohibited  
-A FORWARD -j REJECT &#8211;reject-with icmp-host-prohibited  
COMMIT

I need to make sure that I get this work : 

http://seedup.sargodarya.de/

http://www.kalzumeus.com/2010/09/22/security-lessons-learned-from-the-diaspora-launch/