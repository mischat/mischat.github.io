---
id: 364
title: Fedora 12
date: 2010-08-23T22:58:35+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/08/23/267-revision-2/
permalink: /2010/08/23/267-revision-2/
---
INSTALLING FEDORA 12 on my machine 

To get the C compile &#8230; yum install gcc libxml libexpact &#8230; 

librdf and librasqal : 

synergy &#8230; between machines 

I need to do this : 

export after raptor and before rasqal I should do this in /etc/profile &#8230; 

PKG\_CONFIG\_PATH=/usr/local/lib/pkgconfig  
export PKG\_CONFIG\_PATH

Useful links when i was setting up fedora box 

http://www.linuxquestions.org/questions/fedora-35/how-can-i-mount-lvm-partition-in-ubuntu-569507/

http://www.mjmwired.net/resources/mjm-fedora-f12.html#mp3

http://www.cyberciti.biz/tips/openssh-deny-or-restrict-access-to-users-and-groups.html  
http://www.netfamilynews.org/2010/04/new-media-monsters-weve-created-for-our.html

This lets you check what hardware you have installed on your machine using the smartctl:  
smartctl -a look for &#8211; d 80a -a

http://www.mjmwired.net/resources/mjm-fedora-manage-services.html

http://www.mjmwired.net/resources/mjm-services-f12.html

http://www.howtoforge.com/perfect-server-fedora-12-x86_64-ispconfig-2-p3

http://www.howtoforge.com/perfect-server-fedora-12-x86_64-ispconfig-2-p3

http://linuxreviews.org/man/avahi-set-host-name/

http://albertux.ayalasoft.com/2010/01/30/fedora-12-httpd-userdir-selinux-works/

http://www.howtoforge.com/installing-apache2-with-php5-and-mysql-support-on-fedora-12-lamp

http://www.ics.uci.edu/~lopes/dv/dv.html

http://www.nvidia.com/object/IO_18897.html  
http://gregularexpressions.wordpress.com/2010/01/15/graphics-drivers-for-nvidia-geforce-6200-on-fedora-12-kde/

gcc 

http://download.librdf.org/source/

php.ini http://www.rasyid.net/2007/08/29/datetimezone-in-phpini-for-php5/

Need to add module at boot &#8230; http://fedorasolved.org/video-solutions/nvidia-yum-kmod

talk about synergy 

http://www.mjmwired.net/resources/mjm-fedora-f12.html

http://www.howtoforge.com/fedora-8-server-lamp-email-dns-ftp-ispconfig-p5

SELINUX : http://docs.fedoraproject.org/selinux-user-guide/f10/en-US/sect-Security-Enhanced\_Linux-Working\_with\_SELinux-SELinux\_Contexts\_Labeling\_Files.html

http://fedorasolved.org/server-solutions/postfix-mail-server

disabling nouveau dracut -f /boot/initramfs-$(uname -r).img $(uname -r)

http://www.g-loaded.eu/2008/05/12/how-to-disable-ipv6-in-fedora-and-centos/

http://www.howtoforge.com/fedora-8-server-lamp-email-dns-ftp-ispconfig-p5

And plus there is all of the php.ini stuff &#8230; 

and then there is the glib compile stuff 

This is the list of stuff which I ended up doing : 

FIRST I EDTED : 

/etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0  
HWADDR=00:06:4F:4E:52:7D  
TYPE=Ethernet  
BOOTPROTO=none  
IPADDR=192.168.1.2  
PREFIX=24  
GATEWAY=192.168.1.1  
DNS1=192.168.1.1  
NAME=&#8221;System eth0&#8243;  
UUID=5fb06bd0-0bb0-7ffb-45f1-d6edd65f3e03  
ONBOOT=yes

then i turned on two services 

network 

and sshd

vim /etc/ssh/sshd_config 

yum install vim-enhanced

/usr/sbin/useradd my users, and I give them passwords

Then I locked down root ssh access PermitRoot no  
and i deny all but one users, which I will add my authorized_key file to so i can access via ssh key

yum update and then 

I think switch over my home dirs &#8230;

and switched over /etc/

and /var/www

.ssh keys 

reboot

nvidia 

.ssh keys 

[mirandam@charon ~]$ su -c &#8216;rpm -ivh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm&#8217;  
[mirandam@charon ~]$ su -c &#8216;rpm -ivh http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm&#8217;

yum install kmod-nvidia

reboot 

vim /boot/grub/grub.conf blacklisted noveau 

rdblacklist=nouveau

and 

[mirandam@charon ~]$ su &#8211;  
Password:  
[root@charon ~]# mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img  
[root@charon ~]# dracut /boot/initramfs-$(uname -r).img $(uname -r)

[root@charon ~]# exit

I stupidly tried to add my /etc dir to the /media/data so i could back it up

but i failed and had to 

Ubuntu Live CD  
Motor Mount  
Ubuntu Install Disk  
Engine Mount  
Creating LVM

Wednesday, November 21, 2007  
Mounting LVM Disk using Ubuntu livecd

Mounting is an easy process to do, provided the filesystem type you are using is supported. What happen when you have an LVM formatted disk, and you need to mount it because the disk cannot be booted and a hell lot of valuable data kept inside?? Do not worry, because the solution is here&#8230;&#8230;.‚Ä®‚Ä®1. Get a live cd, for example, Ubuntu. For this article, I use Ubuntu 6.06 (I cannot find any latest version of ubuntu at my place)‚Ä®‚Ä®2. Boot using the live cd. Search for these tools: lvm2. If the cd do not have it, install it.‚Ä®# apt-get install lvm2‚Ä®‚Ä®3. To make sure the harddisk is recognised, you can use fdisk‚Ä®# fdisk -lu‚Ä®‚Ä®4. Once installed, run pvscan to scan all disks for physical volume. this to make sure your LVM harddisk is detected by Ubuntu‚Ä®# pvscan‚Ä®PV /dev/sda2 VG VolGroup00 lvm2 [74.41 GB / 32.00 MB free]‚Ä®Total: 1 [74.41 GB] / in use: 1 [74.41 GB] / in no VG: 0 [0 ]‚Ä®‚Ä®‚Ä®5. After that run vgscan to scan disks for volume groups.‚Ä®# vgscan‚Ä®Reading all physical volumes. This may take a while&#8230;‚Ä®Found volume group &#8220;VolGroup00&#8221; using metadata type lvm2‚Ä®‚Ä®‚Ä®6. Activate all volume groups available.‚Ä®# vgchange -a y‚Ä®2 logical volume(s) in volume group &#8220;VolGroup00&#8243; now active‚Ä®‚Ä®7. Run lvscan to scan all disks for logical volume. You can see partitions inside the hard disk now active.‚Ä®# lvscan‚Ä®ACTIVE &#8216;/dev/VolGroup00/LogVol00&#8217; [72.44 GB] inherit‚Ä®ACTIVE &#8216;/dev/VolGroup00/LogVol01&#8217; [1.94 GB] inherit‚Ä®‚Ä®8. Mount the partition to any directory you want, usually to /mnt‚Ä®# mount /dev/VolGroup00/LogVol00 /mnt

fixed the etc dir from the LiveCD &#8230; and then fixed the symbolic links  
and the it starts name resolving and i can ssh 

/sbin/chkconfig &#8211;list sshd

[root@blanket mmt]# chkconfig &#8211;list sshd  
sshd 0:off 1:off 2:off 3:off 4:off 5:off 6:off  
[root@blanket mmt]# /sbin/chkconfig &#8211;list sshd  
sshd 0:off 1:off 2:off 3:off 4:off 5:off 6:off  
[root@blanket mmt]# /sbin/chkconfig sshd &#8211;level 35 on  
[root@blanket mmt]# /sbin/chkconfig &#8211;list sshd  
sshd 0:off 1:off 2:off 3:on 4:off 5:on 6:off

TURN OFF ipv6 : 

chkconfig ip6tables off

put on tv &#8230; do up case &#8230; then services : 

Installed Flash

for iplayer 

XMMS + audio scrobbler  
yum install xmms xmms-mp3 xmms-faad2 xmms-pulse xmms-skins xmms-scrobbler

yum install mplayer mplayer-gui gecko-mediaplayer mencoder

yum install vlc

Big icon&#8217;s for the tv user 

yum install samba  
[c_drive]  
path = /media/c_drive  
public = yes  
writable = no  
[netshare]  
path = /data/  
public = yes  
writable = yes

[mirandam@charon ~]$ sudo smbpasswd -a username  
New SMB password:  
Retype new SMB password:  
account\_policy\_get: (warnings ignored)  
Added user username.

chkconfig ip6tables off

And make sure it doesn&#8217;t 

start : 

\# Realtek Semiconductor Co., Ltd. RTL-8169 Gigabit Ethernet  
DEVICE=eth0  
HWADDR=00:06:4F:4E:52:7D  
TYPE=Ethernet  
BOOTPROTO=none  
IPADDR=192.168.1.2  
PREFIX=24  
GATEWAY=192.168.1.1  
DNS1=192.168.1.1  
NAME=&#8221;System eth0&#8221;  
UUID=5fb06bd0-0bb0-7ffb-45f1-d6edd65f3e03  
ONBOOT=yes  
IPV6INIT=no  
IPV6_AUTOCONF=no

started samba, smb, httpd mysqld 

mysql-server

mysqladmin -u root password &#8220;softpedia&#8221;

mysql -u root -p < /media/data/disk/mysql.20100324.sql http ... I set my vhosts : and configured my httpd.conf And then I needed to update my php.ini file : I had to set my date.timezone to Europe/London date.timezone = Europe/London Then I had to set php to allow for <? and ?> short hand : 

I then had to install : yum install php-mysql for my wordpress blog to work &#8230;

EMAIL AND STUFF : 

yum install cyrus-sasl cyrus-sasl-devel cyrus-sasl-gssapi cyrus-sasl-md5 cyrus-sasl-plain postfix dovecot

Configuring SMTP-AUTH and TLS : 

postconf -e &#8216;smtpd\_sasl\_local_domain =&#8217;  
postconf -e &#8216;smtpd\_sasl\_auth_enable = yes&#8217;  
postconf -e &#8216;smtpd\_sasl\_security_options = noanonymous&#8217;  
postconf -e &#8216;broken\_sasl\_auth_clients = yes&#8217;  
postconf -e &#8216;smtpd\_recipient\_restrictions = permit\_sasl\_authenticated,permit\_mynetworks,reject\_unauth_destination&#8217;  
postconf -e &#8216;inet_interfaces = all&#8217;  
postconf -e &#8216;mynetworks = 127.0.0.0/8&#8217;

vi /usr/lib/sasl2/smtpd.conf neeeds: 

pwcheck_method: saslauthd  
mech_list: plain login

Then i had to make my ssl cert : 

mkdir /etc/postfix/ssl  
cd /etc/postfix/ssl/  
openssl genrsa -des3 -rand /etc/hosts -out smtpd.key 1024

chmod 600 smtpd.key  
openssl req -new -key smtpd.key -out smtpd.csr

openssl x509 -req -days 3650 -in smtpd.csr -signkey smtpd.key -out smtpd.crt  
mv -f smtpd.key.unencrypted smtpd.key  
openssl req -new -x509 -extensions v3_ca -keyout cakey.pem -out cacert.pem -days 3650

Next we configure Postfix for TLS:  
\# The mydomain parameter specifies the local internet domain name.  
\# The default is to use $myhostname minus the first component.  
\# $mydomain is used as a default value for many other configuration  
\# parameters.  
#  
mydomain = mmt.me.uk  
myorigin = $mydomain  
inet_interfaces = all  
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain  
mynetworks_style = host  
#mydomain = domain.tld

#TLS &#8211; SMTP AUTH  
disable\_vrfy\_command = yes  
smtpd\_use\_tls = yes  
smtpd\_tls\_auth_only = yes  
tls\_random\_source = dev:/dev/urandom  
smtpd\_tls\_key_file = /etc/postfix/ssl/smtpd.key  
smtpd\_tls\_cert_file = /etc/postfix/ssl/smtpd.crt  
#smtpd\_tls\_CAfile = /etc/postfix/ssl/cacert.pem  
smtpd\_sasl\_auth_enable = yes  
smtpd\_sasl\_security_options = noanonymous  
broken\_sasl\_auth_clients = yes  
\# Add some security  
#smtpd\_recipient\_restrictions = permit\_sasl\_authenticated, permit_mynetworks  
smtpd\_recipient\_restrictions = permit\_sasl\_authenticated,permit\_mynetworks,reject\_unauth_destination

Start the needed services : 

chkconfig &#8211;levels 235 sendmail off  
chkconfig &#8211;levels 235 postfix on  
chkconfig &#8211;levels 235 saslauthd on  
chkconfig &#8211;levels 235 dovecot on  
/etc/init.d/sendmail stop  
/etc/init.d/postfix start  
/etc/init.d/saslauthd start  
/etc/init.d/dovecot start

To see if SMTP-AUTH and TLS work properly now run the following command:  
telnet localhost 25  
After you have established the connection to your Postfix mail server type  
ehlo localhost  
If you see the lines  
250-STARTTLS  
and  
250-AUTH LOGIN PLAIN  
everything is fine.  
[root@server1 ssl]# telnet localhost 25‚Ä®Trying 127.0.0.1&#8230;‚Ä®Connected to localhost.‚Ä®Escape character is &#8216;^]&#8217;.‚Ä®220 server1.example.com ESMTP Postfix‚Ä®ehlo localhost‚Ä®250-server1.example.com‚Ä®250-PIPELINING‚Ä®250-SIZE 10240000‚Ä®250-VRFY‚Ä®250-ETRN‚Ä®250-STARTTLS‚Ä®250-AUTH LOGIN PLAIN‚Ä®250-AUTH=LOGIN PLAIN‚Ä®250-ENHANCEDSTATUSCODES‚Ä®250-8BITMIME‚Ä®250 DSN‚Ä®quit‚Ä®221 2.0.0 Bye‚Ä®Connection closed by foreign host.‚Ä®[root@server1 ssl]#  
Type  
To make the dovecot cert:  
You need to edit this file :  
vim /etc/pki/dovecot/dovecot-openssl.cnf  
and then run :  
[root@blanket mischa]# history | grep mkcer  
465 /mkcert.sh  
466 locate mkcert.sh  
468 locate mkcert.sh  
469 /usr/libexec/dovecot/mkcert.sh  
476 /usr/libexec/dovecot/mkcert.sh  
478 /usr/libexec/dovecot/mkcert  
And then I ircd &#8230; which I installed as per usual &#8230;  
Then i installed libraptor and librasqal  
Which i needed to install gcc  
expat-devel  
libxml2-devel  
libcurl-devel  
avahi-devel  
yum install pcre-devel  
yum install ncurses-devel  
readline-devel

I just need to install the synergy now 

and i have put one alias for the lounge user :  
alias connect_server=&#8221;synergyc -f &#8211;name blanket.config jambi.config&#8221;

updatedb cron  
I have done my mv_safe script  
and I have added /etc/cron.daily/diskstatus &#8230; 

I NEED TO SETUP my GIT REPOS now &#8230; and put loads of stuff in git &#8230; should put etc in git for example &#8230;  
I need to