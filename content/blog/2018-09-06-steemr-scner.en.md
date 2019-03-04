---
title: "[New Features on steemr] A Shiny app for the statistics of the Steem CN community!"
author: dapeng
date: "2018-09-06 09:36:42"
slug: steemr-scner
tags: 
  - utopian-io
  - post
  - steemr
  - R
banner: img/banners/logo-steemr.png
---



A new function`scner()` displays a Shiny app, which is a user friendly interactive UI for the statistics of a group of Steemians, hereby those who are active in the CN community. It has the potential to be used for other groups of Steemians with some simple modifications to this function.

<!--more-->


Shiny is an R package that makes it easy to build interactive web apps straight from R. It is very easy to use even for non-R users. The single command `scner()`  displays a webpage, on which a flexible data frame shows the data of the members in the CN community. The users can easily filter or order each column. If the users type an ID,  then a brief report for the ID  will appear. 

![scner.jpg](https://cdn.steemitimages.com/DQmUESa2r9eZdXAvfZ98BvrNwdcXHzYK5uKdrkbHXL1HUqg/scner.jpg)

#### How did I implement them?

I added the new function `scner()` in  'R/shiny.r', as well as the internal functions `scner_ui()` and `scner_server()`  which are the UI function and server function for `scner()`.  Auxiliary files were added into the /inst folder.  Each part of the functions are well documented. Other files were updated automatically by compilation. 

Link to relevant lines in the code on GitHub can be found mainly in my latest commit (click to see the details):

- [new function: scner()](https://github.com/pzhaonet/steemr/commit/8ebff10ce993ea22662faf5d1b37c84d6c8daba5)
