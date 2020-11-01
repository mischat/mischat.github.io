---
id: 525
title: git
date: 2011-12-01T17:51:04+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2011/12/01/509-revision-13/
permalink: /2011/12/01/509-revision-v1/
---
I have been making use of [git](http://git-scm.com/ "Git - Fast Version Control System"), initially designed and developed by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), over the last few years in both my personal and professional lives. 

[Git](https://en.wikipedia.org/wiki/Git_%28software%29) is a fantastic piece of software, I have been using it for everything including document/paper writing to adding version control to my /etc directory on my linux boxes. 

Here I am going to summarise how I have been using git over the last few years. Firstly though, I should mention a friend/former colleague of mine [tialaramex](https://github.com/tialaramex) who helped me out get my head around using git to start with. 

Firstly, cloning a repository: 

`git clone git@github.com:mischat/sprotocol.git`

or, the following command which will clone the repo to a directory named &#8220;sprotocol-dev&#8221;

`<br />
git clone git@github.com:mischat/sprotocol.git sprotocol-dev`

If this is your first time using git you can set your name and email address, so that your changes are labelled correctly, when you push them upstream. 

`git config user.email "you@email.com"<br />
git config user.name "Your Name"`

Note that you can use the **&#8211;global** flag to set them globally, instead of just in your given repo.

Setting up a git repo. Firstly, you can always use an online service such as [github](http://github.com "Github") &#8211; this will allow pointing and clicking. 

But sometimes you may wish to setup your own git repository. You can do it like so: 

`mkdir LAMEREPO<br />
cd LAMEREPO<br />
git init --shared=group<br />
vim README "Readme file for LAMEREPO"<br />
git add README<br />
git commit -m "Initial commit for LAMEREPO"`

You can create branches in git, you may want to do this if you are planning on making considerable changes to your repo. Branches are most useful! 

To find out which branch you are currently in: 

`git branch`

To create a new branch, and it check it out: 

`git checkout -b lamebranch`

To check out the master branch:

`git checkout master` 

To merge branches, firstly you should checkout the branch which you want to merge another branch into, and then use the merge command: 

`git checkout master<br />
git merge lamebranch`

Finally, you can delete branches in git using the **-d** flag: 

`git branch -d lamebranch`

Note that when deleting a branch you can use **-D** which will delete the branch if it was pushed upstream at any point in time. 

If you would like to track a remote branch, perhaps one created by someone else committing to the repo, you can &#8220;track&#8221; a remote branch. 

`git checkout --track -b lame origin/lame`

If you would like to create a remote branch, so that other people can track it you can do so with the following commands: 

`git checkout -b lamebranch<br />
git push origin lamebranch:lamebranch<br />
look in git/config (make sure it is a remote branch)`

If you find that you would like to select a (number of) commits from a different branch, and merge into another branch without having to merge the whole lot, you can cherry-pick git commits. 

`git cherry-pick 1d67bdbbdb4b98d142bdcce1b78cbe4d2d396afd`

You can also create tags in a git repo. This is how I make tags: 

`git tag -a "TAG _NAME"<br />
git push --tags`

Cloning a repo which multiple people can update. This is useful when working other people. 

`<br />
git clone git@github.com:mischat/sprotocol.git<br />
cd sprotocol<br />
git config --add core.sharedRepository group<br />
chown -R username:sharedgroup .<br />
find -type d -print0 | xargs -0 chmod g+s {}`