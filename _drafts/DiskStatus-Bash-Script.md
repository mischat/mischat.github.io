---
id: 256
title: DiskStatus Bash Script
date: 2010-08-23T22:15:30+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=256
permalink: /?p=256
categories:
  - Uncategorized
---
I use this bash script to monitor how much disk space I have available on my home server.

`#!/bin/sh<br />
# set -x<br />
# Shell script to monitor or watch the disk space<br />
# It will send an email to $ADMIN, if the (free available) percentage of space is >= 90%.<br />
# -------------------------------------------------------------------------<br />
# Set admin email so that you can get email.<br />
ADMIN="mischa.tuffield@garlik.com steve.harris@garlik.com nick.lamb@garlik.com"<br />
# set alert level 90% is default<br />
ALERT=95<br />
# Exclude list of unwanted monitoring, if several partions then use "|" to separate the partitions.<br />
# An example: EXCLUDE_LIST="/dev/hdd1|/dev/hdc5"<br />
EXCLUDE_LIST="tempfs";<br />
#<br />
#::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::<br />
#<br />
function main_prog() {<br />
while read output;<br />
do<br />
#echo $output<br />
  usep=$(echo $output | awk '{ print $1}' | cut -d'%' -f1)<br />
  partition=$(echo $output | awk '{print $2}')</p>
<p>  if [ $usep -gt $ALERT ] ; then<br />
    for email in $ADMIN ; do<br />
       echo "Running out of space \"$partition ($usep%)\" on server $(hostname), $(date)" | \<br />
       mail -s "Alert: Almost out of disk space $usep%" $email<br />
    done<br />
  fi<br />
done<br />
}</p>
<p>if [ "$EXCLUDE_LIST" != "" ] ; then<br />
  df -HP | grep -vE "^Filesystem|tmpfs|cdrom|${EXCLUDE_LIST}" | awk '{print $5 " " $6}' | main_prog<br />
else<br />
  df -HP | grep -vE "^Filesystem|tmpfs|cdrom" | awk '{print $5 " " $6}' | main_prog<br />
fi`