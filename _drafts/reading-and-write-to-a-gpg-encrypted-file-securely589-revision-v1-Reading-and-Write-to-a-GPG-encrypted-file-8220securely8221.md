---
id: 593
title: 'Reading and Write to a GPG encrypted file &#8220;securely&#8221;'
date: 2014-07-09T00:26:47+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2014/07/09/589-revision-v1/
permalink: /2014/07/09/589-revision-v1/
---
have been using two commands blogged about by a friend [Steve Harris](https://twitter.com/theno23) to store my passwords on my mac osx laptop. He illustrated two commands “useful” and “viuseful” which open an gpg encrypted file using less and vi respectively. Opening the file in less, allows for safe read-only access to the contents of the encrypted file. The vi mode of operation as described by Steve leaves a temporary copy of the file that exists in plaintext briefly while it’s being encrypted.

With a little help from one of my current colleagues Sid I have altered Steve’s example by writing the temp file to a ramdisk, which is subsequently srm’d.

The fact that this implementation never writes the contents of the unencrypted file to disk, I recon I can go as far as saying that it was a little \*more\* secure than Steve’s original post 🙂  
`<br />
#Password config<br />
USEFUL_FILE="$HOME/.passwords/your_password_file.txt.gpg"<br />
USEFUL_KEYID="XXXXXXXX"<br />
RDLABEL="ramdisk"<br />
RAMDISK="/Volumes/$RDLABEL" # Please no spaces<br />
FILE="passtmp" # Please no spaces`  
</code>  
`<br />
function useful {<br />
&nbsp;&nbsp;gpg --trust-model always -d $USEFUL_FILE | less<br />
}<br />
`  
`<br />
function ramdisk {<br />
&nbsp;&nbsp;let SIZE=$1*2<br />
&nbsp;&nbsp;# Check if the ramdisk is already mounted<br />
&nbsp;&nbsp;if [[ $(mount | grep "$RAMDISK " | wc -l) -eq 0 ]]; then<br />
&nbsp;&nbsp;&nbsp;&nbsp;diskutil erasevolume HFS+ "$RDLABEL" $(hdiutil attach -nomount ram://$SIZE) &> /dev/null<br />
&nbsp;&nbsp;fi<br />
}<br />
`  
<br />
function cleanup {<br />
&nbsp;&nbsp;if [[ -e "$RAMDISK/$FILE" ]]; then<br />
&nbsp;&nbsp;&nbsp;&nbsp;srm -f "$RAMDISK/$FILE"<br />
&nbsp;&nbsp;&nbsp;&nbsp;umount "$RAMDISK"<br />
&nbsp;&nbsp;fi<br />
}</p>
<p>function viuseful {<br />
&nbsp;&nbsp;ramdisk 4096 # 4MB<br />
&nbsp;&nbsp;cp "$USEFUL_FILE" "$USEFUL_FILE~"<br />
&nbsp;&nbsp;vi '+set viminfo=' '+set noswapfile' '+r !gpg --trust-model always --quiet -d '"$USEFUL_FILE"' 2>/dev/null' '+1d' '+redraw!' "$RAMDISK/$FILE"<br />
&nbsp;&nbsp;if [ -s "$RAMDISK/$FILE" ]; then<br />
&nbsp;&nbsp;&nbsp;&nbsp;gpg --trust-model always --yes -r "$USEFUL_KEYID" -o "$USEFUL_FILE" -e "$RAMDISK/$FILE"<br />
&nbsp;&nbsp;else<br />
&nbsp;&nbsp;&nbsp;&nbsp;echo "File not changed"<br />
&nbsp;&nbsp;fi<br />
&nbsp;&nbsp;cleanup<br />
}</p>
<p>So yeah, a big shout out to both Steve and Sid, for now I have a secure(-ish) way of storing a bunch of passwords and stuff.</p>
<p>If someone would like to tell me how to create the RAMDISK on a linux machine I would love to know!</p>