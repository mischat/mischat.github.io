---
id: 474
title: Deleting History
date: 2011-05-24T23:47:45+01:00
author: Mischa
layout: post
guid: http://mmt.me.uk/blog/?p=474
permalink: /?p=474
categories:
  - Uncategorized
---
http://t.co/MCAMHh6 <-- #git removing stuff from history http://dound.com/2009/04/git-forever-remove-files-or-folders-from-history/ and then git push --force --verbose to push it upstream ...  `</p>
<p>#!/bin/bash<br />
set -o errexit</p>
<p># Author: David Underhill<br />
# Script to permanently delete files/folders from your git repository.  To use<br />
# it, cd to your repository&#8217;s root and then run the script with a list of paths<br />
# you want to delete, e.g., git-delete-history path1 path2</p>
<p>if [ $# -eq 0 ]; then<br />
    exit 0are still<br />
fi</p>
<p># make sure we&#8217;re at the root of git repo<br />
if [ ! -d .git ]; then<br />
    echo &#8220;Error: must run this script from the root of a git repository&#8221;<br />
    exit 1<br />
fi</p>
<p># remove all paths passed as arguments from the history of the repo<br />
files=$@<br />
git filter-branch &#8211;index-filter &#8220;git rm -rf &#8211;cached &#8211;ignore-unmatch $files&#8221; HEAD</p>
<p># remove the temporary history git-filter-branch otherwise leaves behind for a long time<br />
rm -rf .git/refs/original/ &#038;&#038; git reflog expire &#8211;all &#038;&#038;  git gc &#8211;aggressive &#8211;prune</p>
<p>`