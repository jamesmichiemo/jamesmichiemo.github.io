---

published: true
layout: post
title: "How to use Octopress: Deployment"
date: 2013-02-27 15:39
comments: true
categories: octopress github 

---

In our last ["How to Use Octopress"](http://jamesmichiemo.github.com/blog/2013/02/16/installing-octopress/) blog post, we went over how to setup our blog, but that was only the first step. The next step would be to make our Octopress available through hosting. Right now, the Octopress we installed is only setup locally. Only users with access to your computer are able to view the blog, but once we have our Octopress available through hosting, anyone with internet access will be able to find it.

For hosting my own blog, I chose to use [Github pages](http://pages.github.com/). There were several other options but I felt better having my blog linked to the same place I keep my other projects on [my Github account](https://github.com/jamesmichiemo). It made sense considering that most of what I'll be writing about on my blog will revolve around these repositories. As I update my repos, I'll be updating my blog.

![Octocat](http://venturebeat.files.wordpress.com/2012/03/octocat1.png)

## Using Github Pages

[Github Pages](http://pages.github.com/) is a free public hosting service that allows users more freedom in workflow options with [git](http://git-scm.com/) and other tools for web such as [Jekyll](http://jekyllrb.com/). It's most likely the best choice for our blog. I assume Octopress was created with Github in mind, considering the workflow format and the similarity between mascots. 

There's plenty documentation for assisting in deploying to Github Pages on the [official docs page](http://octopress.org/docs/deploying/github/). I recommend following the simple instructions offered there, but I'll still walkthrough and share my experience deploying my Octopress.


### Creating a New Github Repository

For a Github Page, we will need a Github account. [Make one](https://github.com/users) if you don't have a Github account already.

With your Github account, [create a new repository](https://github.com/new) and name the repo <code>username.github.com</code> 

<code>http://username.github.com</code> will be the url for the Octopress.

### Configuring Github Pages

The next step in our deployment is to use [rake](http://rake.rubyforge.org/) to configure github pages. Octopress has a built-in task for setting up everything so all that's needed is the following command to be entered into Terminal while inside the Octopress directory.

<pre><code>rake setup_github_pages</code></pre>

A prompt will appear to enter the repo url. Entering the url made in the previous step will link your Octopress to the new Github repo.

Once that's complete, we are now able to use rake to commit and push whatever changes that are made to the Octopress directory by entering:

<pre><code>rake generate</code>
<code>rake deploy</code></pre>

With this our Octopress is now published!

Check the url to see if it's up. If you can't find your blog at the url, carefully repeat the steps until it works. 

## Conclusion

We've only covered the beginning stages, but at least now we have a visible working blog on the web. Next, we'll take a look into posting and making configurations with Octopress.  




