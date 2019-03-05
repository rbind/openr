---
title: "[New Features on steemr]  Diagrams in the Shiny app for the statistics of the Steem CN community!"
author: Peng Zhao
date: "2018-09-07 05:42:45"
slug: steemr-scner-diagrams
tags: 
tags: 
  - R
  - steemr
  - news
banner: img/banners/logo-steemr.png
---


I added diagrams into the Shiny app `scner()`. These diagrams include the word clouds of the Steemians of the CN community, as well as the histograms for the distributions according to the ESP, account value, online-days, etc.. 

<!--more-->


![scnerfig.png](https://cdn.steemitimages.com/DQmNweQ7fTRkbCcFgxT8Dpy3FKt9AAyCRDz47moz6Sx9k6W/scnerfig.png)

Minor bugs were fixed as well.

#### How did I implement them?

I added two internal functions, i.e. `pcner()` for plotting wordclouds chars, and `phist()` for plotting enhanced and customized histograms, in 'R/shiny.r'. New codes were added to the function `scner_ui()` and `scner_server()` to build the elements of the shiny app.  

Link to relevant lines in the code on GitHub can be found mainly in my latest commit (click to see the details):

- [Image display on `scner()`](https://github.com/pzhaonet/steemr/commit/b9be1fcacd87189b6466d7102cc3a5499b9344fe).

