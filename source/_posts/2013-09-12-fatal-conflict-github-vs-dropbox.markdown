---
layout: post
title: "Fatal Conflict: Git vs Dropbox"
date: 2013-09-12 11:38
comments: true
categories: vcs versioncontrol  
---


So this morning, I ran into a very small problem that had to do with version control. I decided to update a repo that I had been working on for the past few days on another laptop. When I attempted to perform a git pull, I was given an error message that said, "fatal: Reference has invalid format: 'refs/heads/master'".

After doing a bit of research I discovered that the problem may have been caused by using both Git and Dropbox at the same time for the same project. Now I've actually been warned NOT to do this, but I'm stubborn about my tools and I figured that if it's been working for me for months, there really shouldn't be any reason why I should do away with my own methods for my own projects.

I could do away with using Dropbox for coding, but Dropbox is super convenient for accessing projects on mobile phones. Github recently made a super slick mobile web version of their website for accessing repos on smartphones, but it's not really made for editing. You can look but you can't touch.

Now it's not like I'm refactoring code on my phone on the regular, but it's still a nice feature to have, just in case. Until I figure out how to use bash on the phone, I'll stick to Dropbox.            
 
Anyways, the conflict wasn't too hard to fix. The problem was that Dropbox made an extra copy of a file that I already have. To fix the error I had to run a command that would look for the conflicted copy and destroy it. For this I used this command in the repo:

```
$ find . -type f -name "* conflicted copy*" -exec rm -f {} \; 
``` 

With that command, I was able to get rid of the error and resume using git as usual. Simple right?

This was probably the proof that I needed that Git and Dropbox don't mix well together, but I'll probably still use Dropbox and Git anyway. What else could go wrong?   
