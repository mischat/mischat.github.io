---
id: 323
title: Setting up Diaspora on Fedora 12
date: 2010-09-19T19:11:32+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/09/19/322-revision/
permalink: /2010/09/19/322-revision/
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