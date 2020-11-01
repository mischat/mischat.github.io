---
id: 516
title: git submoduling
date: 2011-12-01T16:42:25+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2011/12/01/496-revision-5/
permalink: /2011/12/01/496-revision-5/
---
Adding Submodules to a Git Repository

In order to add a git submodule the following steps need to be taken:

Go to the root of the repo which you want to add the submodule to  
git submodule add git@example.com:foozle misc/bar (which added the git repo to the dir misc/bar)  
cat .gitmodules (to check that the submodule is correctly configured)  
git submodule init (initiate the submodule in the existing repo)  
git submodule update (to fetch the commits) 

It should be noted that :

You will do a git fetch in the submodule and checkout origin/master or whatever.  
Then you need to commit the change in the parent project.  
git submodule update will then sync the submodules with the commit referenced in the parent module.  
If it can do that without fetching it will. If not it will fetch and see if it can find the commit.  
Remember also that submodules work with a &#8216;detached head&#8217;  
Please don&#8217;t make changes to the submodule in your dpx repo, please check out the submodule in its own right,make changes there and then fetch and commit them the main repo. This will make everyones life easier. 

These are what I had put up on the wiki at some point in the past: 

Adding Submodules to a Git Repository  
In order to add a git submodule the following steps need to be taken:  
Go to the root of the repo which you want to add the submodule to  
git submodule add git@example.com:foozle misc/bar (which added the git repo to the dir misc/bar)  
cat .gitmodules (to check that the submodule is correctly configured)  
git submodule init (initiate the submodule in the existing repo)  
git submodule update (to fetch the commits)  
It should be noted that :  
You will do a git fetch in the submodule and checkout origin/master or whatever.  
Then you need to commit the change in the parent project.  
git submodule update will then sync the submodules with the commit referenced in the parent module.  
If it can do that without fetching it will. If not it will fetch and see if it can find the commit.  
Remember also that submodules work with a &#8216;detached head&#8217;  
Please don&#8217;t make changes to the submodule in your dpx repo, please check out the submodule in its own right,make changes there and then fetch and commit them the main repo. This will make everyones life easier.