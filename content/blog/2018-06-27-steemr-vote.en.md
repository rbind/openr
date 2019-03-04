---
title: "[New Features on steemr] Functions as vote reports!"
author: dapeng
date: "2018-06-27 14:44:03"
slug: steemr-vote
tags: 
  - utopian-io
  - post
  - R
  - steemr
banner: img/banners/logo-steemr.png
---



'[steemr](https://cran.r-project.org/package=steemr)' is an open source R package for playing with Steem data in [R environment](https://en.wikipedia.org/wiki/R_(programming_language)). It is used to download, post process, analyze,  and visualize Steem data on the basis of the powerful statistic power of R. 

<!--more-->

#### What features did I add?

- Following the [suggestions](https://steemit.com/utopian-io/@dapeng/new-features-on-steemr-supports-appbase-api-and-plots-active-hour-diagrams#@justyy/re-dapeng-new-features-on-steemr-supports-appbase-api-and-plots-active-hour-diagrams-20180620t135957681z) from the utopian moderator,  default values of the parameters were removed from the functions, and

- the database URI for SteemSQL was defined in an independent function `steemsql_connection()`. Many thanks to the moderator!

- New functions about the vote information were added, including
  - `who_not_vote()`, which shows which followers have not voted a post yet,
  - `voter()`,  which gives a vote report of given IDs with all the vote records, a summary, as well as a time series plot of daily votes, and

  ![2018-06-27-003.jpeg](https://cdn.steemitimages.com/DQmPysueYr87edLrzqc7Ee2wYMvKL7uTqbAmcPWAyQs2R6J/2018-06-27-003.jpeg)

  > A diagram produced by `voter()` .

  - `voter_sum()`,  which give a report of the voters of a series of posts with a summary and a pie diagram.

![2018-06-27-002.jpeg](https://cdn.steemitimages.com/DQmcpfseZQXJLVpn4jLbKKcc5xQD4nxB1Z4iEx9F76aDi9T/2018-06-27-002.jpeg)

>  A pie diagram produced by `voter_sum()`. 

- Some minor literal changes.



#### How did I implement them?

I added these new functions in 'R/steemr.r'. For easy maintenance, the `hourrose()`function was moved into a single 'R/hourrose.r' file.

![2018-06-27-001.jpg](https://cdn.steemitimages.com/DQmT5fnsefADRvvEgYh8mfC6QKnm5swGK1Kmm7JMEj9oZJE/2018-06-27-001.jpg)

> A screenshot showing that I was writing the functions with the RStudio IDE.

Links to relevant lines in the code on GitHub can be found mainly in my latest commits as follows:

- [add a database URI function. remove the default value of id](https://github.com/pzhaonet/steemr/commit/70dcfca572b7c3a317a72fd004cf08c3749c53c3)
- [new functions: who_not_vote(), voter()](https://github.com/pzhaonet/steemr/commit/07cde76df593d40edd83dd8c0e515b7fc45b0f5b)
- [new function: voter_sum()](https://github.com/pzhaonet/steemr/commit/510199b27fb196be54361057fcce47a1f9059a9b)
- [documentation updated. bugs fixed.](https://github.com/pzhaonet/steemr/commit/d0fe42c8c6436a909227697796a803ae795bd88b)

