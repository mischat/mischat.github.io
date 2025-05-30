---
id: 540
title: Using Git
date: 2011-12-01T18:36:29+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2011/12/01/509-revision-28/
permalink: /2011/12/01/509-revision-v1/
---
I have been making use of [git](http://git-scm.com/ "Git - Fast Version Control System"), initially designed and developed by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), over the last few years in both my personal and professional lives. 

[Git](https://en.wikipedia.org/wiki/Git_%28software%29) is a fantastic piece of software, I have been using it for everything including document/paper writing, to adding version control to my /etc directory on my linux boxes. 

In this post I will summarise how I have been using git over the last few years. Firstly though, I should mention a friend/former colleague of mine [tialaramex](https://github.com/tialaramex) who helped me out get my head around using git to start with. 

**Cloning a repository**: 

`git clone git@github.com:mischat/sprotocol.git`

or, the following command which will clone the repo to a directory named &#8220;sprotocol-dev&#8221;

`<br />
git clone git@github.com:mischat/sprotocol.git sprotocol-dev`

If this is your first time using git you can set your name and email address, so that your changes are labelled correctly when you push them upstream. 

`git config user.email "you@email.com"<br />
git config user.name "Your Name"`

Note that you can use the **&#8211;global** flag to set them globally, instead of just in a given repo.

**Setting up a git repo**.

You can always use an online service such as [github](http://github.com "Github") &#8211; this will allow for pointing and clicking. 

But sometimes you may wish to setup your own git repository. You can do it like so: 

`mkdir LAMEREPO<br />
cd LAMEREPO<br />
git init --shared=group<br />
vim README "Readme file for LAMEREPO"<br />
git add README<br />
git commit -m "Initial commit for LAMEREPO"`

**Branches in git.** 

You can create branches in git, you may want to do this if you are planning on making considerable changes to your repo. Branches are most useful! 

To find out which branch you are currently in: 

`git branch`

To create a new branch, in turn checking it out: 

`git checkout -b lamebranch`

To check out the master branch:

`git checkout master` 

To merge branches, firstly you should checkout the branch which you want to merge into, and then use the merge command: 

`git checkout master<br />
git merge lamebranch`

Finally, you can delete branches in git using the **-d** flag: 

`git branch -d lamebranch`

Note that when deleting a branch you can use **-D** which will delete the branch if it was pushed upstream at any point in time. 

If you would like to **track a remote branch**, perhaps one created by someone else committing to the repo. This will allow you to track any changes made to a remote branch. 

`git checkout --track -b lame origin/lame`

If you would like to **create a remote branch**, so that other people can track it, you need to create a local branch, and then you need to push it upstream to **origin**.

`git checkout -b lamebranch<br />
git push origin lamebranch:lamebranch<br />
look in git/config (make sure it is a remote branch)`

**Cherry-picking changes in git**

If you find that you would like to select commits from a different branch, and merge into a different branch without having to merge the whole lot, you can cherry-pick git commits individually. 

`git cherry-pick 1d67bdbbdb4b98d142bdcce1b78cbe4d2d396afd`

**Tagging your git repo**

You can also create tags in a git repo. This is how I make tags in my repos: 

`git tag -a "TAG _NAME"<br />
git push --tags`

**Cloning a repo so that multiple people can update it**.

This is useful when working in a team. 

`<br />
git clone git@github.com:mischat/sprotocol.git<br />
cd sprotocol<br />
git config --add core.sharedRepository group<br />
chown -R username:sharedgroup .<br />
find -type d -print0 | xargs -0 chmod g+s {}`

I should mention that I always use rebase when pulling commits from upstream on to my version of a repo. I have added an alias to my global git configuration, which allows me to type **git up** whenever I wish to grab upstream commits. 

`git config --global --add alias.up 'pull --rebase'`

And finally, I also make constant use of git&#8217;s stashing and popping functions. Most useful if you have changes you wish not to commit.

`git stash<br />
git up    (or git pull)<br />
git stash pop`

I have a blog post coming up on how one can add a submodule to a git repo. Thanks for your attention!