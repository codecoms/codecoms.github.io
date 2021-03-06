---
layout: post
title:  "Creating a private remote repository with Git"
subtitle: "How to create a private remote repository with Git"
date: 2012-02-23 20:20:40
author: "Kevin"
tags:
  - Git
  - Blog
  - programming
categories: Git
blurb: >
  How to create a private remote repository with Git.

---


Normally you can simply sign up at [http://github.com](http://github.com) to setup a free (but public) remote repository for your git project.
But if you want to create a private version on a remote server that already has git installed here is an example script:

{% highlight bash %}

source_dir=~/src
project=myproject
remote=myremoteserver.com

mkdir -p $source_dir/$project
cd $source_dir/$project

{% endhighlight %}

Now add some files:

{% highlight bash %}

git init .
git add .
git commit -m 'initial commit'

ssh $remote "mkdir -p repos/$project"
ssh $remote "cd repos/$project && git --bare init"

git remote add origin $remote:repos/$project
git push origin master

git config branch.master.remote origin
git config branch.master.merge refs/heads/master

{% endhighlight %}

<p>&nbsp;</p>

{% include twitter_plug.html %}
