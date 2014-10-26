---
layout: post
title: "Installing ChucK on Ubuntu"
date: 2013-10-24 16:12
comments: true
categories: tips 
---

Lately, I've been getting into this thing called "live coding". It's an improvisational programming technique used to orchestrate light and sound. I've watched a few demos of it and I'm already hooked on the idea of learning how to do this sort of thing. Currently, I'm taking a couple of classes to become better at programming, so I feel like it's the perfect thing to play around with for fun.

<div class="video-container">
<iframe width="420" height="315" src="//www.youtube.com/embed/GSGKEy8vHqg" frameborder="0" allowfullscreen></iframe>
</div> 

I'm using the ChucK programming language to get a feel for making music with algorithms. It's a language made specifically for manipulating sound and it's fun to play with, but what wasn't fun was figuring out how to install it on Ubuntu.

I had no problems installing with Mac, but the Ubuntu installation was a bit more involved. I tried the old ./configure, make, make install trick on the source file but I was missing too many dependencies for it to run. I then checked for an apt-get package but then chuck told me that I was missing an audio API to connect to so I was stuck with a music programming language that couldn't make a sound. 

After searching through message boards, mailing lists, and blogs, I was able to find a solution from a post about ["Using a DDR dance mat as a musical instrument"](http://t-a-w.blogspot.com/2007/05/using-ddr-dance-mat-as-musical.html). Not my intention, but cool idea. 

The author had figured out that you need to run apt-get chuck with another application call jackd. First you need to run the installation:

<pre><code>$ sudo apt-get install chuck jackd</code></pre>

ChucK still won't work since you need jackd running at the same time, so once you have jackd installed, go ahead and run this in a new terminal:

<pre><code>$ jackd -d alsa</code></pre>

Leave that terminal running in the background somewhere and then proceed to run ChucK with this line:

<pre><code>$ chuck --srate48000 *.ck</code></pre> 
   
And that should be it. After running that last line I was able to hear some audio from my speakers.

If you have a Mac, rejoice. It's only one click. FML

 
