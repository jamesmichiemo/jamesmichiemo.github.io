---
layout: post
title: "How to Make an Octopress: Setup"
date: 2013-02-16
comments: true
categories: octopress
published: true

---

The last time I tried to blog was ages ago in the early aughties when [Xanga](http://www.xanga.com) ruled. Nowadays, [Wordpress](http://www.wordpress.com) is definitely the most popular weapon of choice for blogging but I decided to go with Octopress to help expand my developer skills.

![Octopress Logo](http://drupal.org/files/project-images/octopress.png)

[Octopress](http://octopress.org/) is basically a “blogging framework for hackers”. I like that it's [open source](http://en.wikipedia.org/wiki/Open_source) and that [Ruby](http://www.ruby-lang.org/en/) runs everything in the framework. All you need is your favorite text editor and some command line chops to start posting. Octopress sites are fast, secure, and mobile-friendly. The limitless amount of customization is also a huge bonus that I hope will keep me challenged and engaged in my coding.

If you're interested in making your own Octopress, the [official documentation](http://octopress.org/docs/setup/) has a great guide to follow for setting up. It's a step by step walkthrough that shouldn't be a problem for anyone comfortable with Terminal. For the sake of those that aren't satisfied with the Octopress docs, I'll share a simpler step by step guide that covers the initial setup.

## Preparations

Before we begin installing Octopress, we must make sure that [Git](http://git-scm.com/), [RVM](https://rvm.io/), and Ruby 1.9.3 are up and running.

Open up Terminal and enter:

<pre><code>$ git --version</code></pre>
then
<pre><code>$ rvm --version</code></pre>
and
<pre><code>$ ruby --version</code></pre> 

The --version command will tell you which version of the application is currently installed. If no version is revealed, it must mean that your application is not installed.

If you need an easy guide for installing these tools, I recommend Moncef Belyamani's tutorial: [How to Install Xcode, Homebrew, Git, RVM, & Ruby 1.9.3 on Snow Leopard & Lion.](http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/)

## Installing Octopress

Go to the directory where you would like to use Octopress and clone the [original repo](https://github.com/imathis/octopress) by inputing the following:

<pre><code>$ git clone git://github.com/imathis/octopress.git octopress </code></pre>

## Setting up Octopress

Once installed, enter the Octopress folder just cloned.

<pre><code>$ cd octopress</code></pre> 

If RVM is installed, you'll be asked if you trust the .rvmrc file, type yes.

## Installing Dependencies 

Inside the Octopress folder, the following commands must be entered for the [Bundler gem](http://gembundler.com/).

<pre><code>$ gem install bundler</code></pre>

<pre><code>$ bundle install</code></pre>

## Installing the Default Octopress Theme

Finally, to add some styling, enter:

<pre><code>$ rake install</code></pre>

## Conclusion

At this point, we have everything we need to make a blog post, but we still need to deploy our octopress to a host and also make changes the blog configurations to make the site more personalized.  I'll be sure to cover those steps in a future post. I hope this post helps out anyone with an interest in making a new Octopress. 

