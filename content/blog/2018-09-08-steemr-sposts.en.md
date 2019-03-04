---
title: "[New Features on steemr] Display all the posts of a give Steemian with statistics, and get the utopian review and upvote plan!"
author: dapeng
date: "2018-09-08 20:41:57"
slug: steemr-sposts
tags: 
tags: 
  - utopian-io
  - post
  - R
  - steemr
banner: img/banners/logo-steemr.png
---


- A new function`sposts()` displays a Shiny app, which is a user friendly interactive UI to show all the posts of a give Steemian's ID.  Analysis diagrams are plotted as well, including the distribution of the post payout and votes, the active hour of the Steemian's posting, and the time series of the growth of the cumulative post number, payout, and votes.  

<!--more-->


  Shiny is an R package that makes it easy to build interactive web apps straight from R. It is very easy to use even for non-R users. The single command `sposts()`  displays a webpage, on which a flexible data frame shows the data of all the posts of the given Steemian's ID. The users can easily filter, order or search each column.

![posts.png](https://cdn.steemitimages.com/DQmeJTjCY9tCNFdgtD8Jq3YoVprnoBfD9BK7D8vcTE4gYvn/posts.png)

- A new function `gur()` can gets the utopian review and upvote plan from utopian.rocks. Utopian.io users can use it to see the progress of the submission and upvoting. Furthermore, users can do some further analysis on the utopian review data. Many thanks to @amosbastian, the author of utopian.rocks.

![gur.jpg](https://cdn.steemitimages.com/DQmTDMpU6AX2FSCk2npyJPzmHW95kGWcYViJztfRKmYTa8W/gur.jpg)

- Some minor bugs were fixed.

#### How did I implement them?

I added the new function `sposts()` in  'R/shiny.r', as well as the internal functions `sposts_ui()` and `sposts_server()`  which are the UI function and server function for `sposts()`, the function `repcalc()` which calculates the reputation of the given Steemian, and the function `skewness()` to calculate whether a distribution is normal. 

I added the new function `gur()` in 'R/get.r'.

Each part of the functions are well documented. Other files were updated automatically by compilation. 

Link to relevant lines in the code on GitHub can be found mainly in my latest commit (click to see the details):

- [new functions: gur() and sposts()](https://github.com/pzhaonet/steemr/commit/108da330916dfa4d2aa472a95e09911b60c9b8b9).

