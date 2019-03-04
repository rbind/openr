---
title: "[New Features on steemr] Functions for a user friendly UI as an interactive follower report!"
author: dapeng
date: "2018-07-10 19:45:03"
slug: steemr-sfollow
tags: 
  - utopian-io
  - post
  - steemr
  - R
banner: img/banners/logo-steemr.png
---


A new function`sfollow()` displays a Shiny app, which is a user friendly 	interactive UI as a follower report. 

<!--more-->

Shiny is an R package that makes it easy to build interactive web apps straight from R. It is very easy to use even for non-R users. The single command `sfollow()`  displays a webpage, on which the users just has to type an ID, and then a follower report will appear, with (1) a list of the 'followers but not following',  (2) 'following but not followers', (3) a table of the followers' information, and (4) a table of the following information. The users can easily filter or order each column.

![2018-07-10-002.jpg](https://cdn.steemitimages.com/DQmZPfR1KSAUVEZLYxjPzm1tf2BBsEKaGdzFBUPqydsSURh/2018-07-10-002.jpg)

> Part 1 of @ned's follower report  produced by `sfollow()`.



![2018-07-10-001.gif](https://cdn.steemitimages.com/DQmZ37NAPM1oLRVBPfjzGUgSF4ckGLfTuHMo5GCF3Bwz9L5/2018-07-10-001.gif)


> Part 4 of @ned's follower report   produced by `sfollow()`.

#### How did I implement them?

I added the new function `sfollow()` in  'R/shiny.r', as well as the internal functions `sfollow_ui()` and `sfollow_server()`  which are the UI function and server function for `sfollow()`. Each part of the functions are well documented. Other files were updated automatically by compilation. 

Link to relevant lines in the code on GitHub can be found mainly in my latest commit (click to see the details):

- [new function: sfollow()](https://github.com/pzhaonet/steemr/commit/e50ff65bbd57cfb8cc8a2c69e49b2a12ea429da3).
