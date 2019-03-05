---
title: "[New Project] steemr: an R package to download, play with, and visualize Steem data"
author: 赵鹏
date: "2018-06-12 10:18:51"
slug: new-project-steemr-an-r-package-to-download-play-with-and-visualize-steem-data
tags: 
  - R
  - steemr
  - news
banner: img/banners/logo-steemr.png
---


When I became active on steemit.com in July 2017, the first thing for me to do was to find an R package to process Steem data. As an R user and package developer, it would have been amazing if I could easily download my posts, my operations, my communications with others on Steem, and analyze the data with the power of R language.

Unfortunately, I found nothing.

<!--more-->

Then I started to  write R functions on my own based on Steemdb, SteemData and SteemSQL. Some of these functions were used in a series of data analysis posts with the title 'Steem Watch', and others were used to build the site steemr.org.

![](https://steemitimages.com/0x0/https://gateway.ipfs.io/ipfs/QmTY9hEDUcSZQcdf5grhA1GcW1XnZ5y4orXjiY9hiAyuJ7)
Logo for steemr. Designed by @maiyude

steemr.org gained an impressive reputation in the community. However, as most of its components were based on SteemData, its heart was broken when SteemData was down. It was a pity that these codes were not really shared in the community and now they are useless, --- unless SteemData comes back.

![](https://steemitimages.com/DQmWDzc2TNk429yRotiFHCCZk6KKPEh3aQ8i5zJiLyfWW3y/steemrmap.jpg)

Visitor map of steemr.org

Luckily, the rest of steer.org still works. Then I decided to open the source of steemr.org and develop a brand new R package. It is like the organ transplantation. Steemr.org is dead, while the steemr package can use some useful parts from steemr.org.

![](https://steemitimages.com/DQmZ16mP1YE9JSbNcA86aUCw82kCWssNJ1EEQohXaKt72LR/steemr20171109.gif)

One of steemr.org's features: display all the posts of a user

In the meanwhile, my book *[Leaning R: for Rookies (in Chinese)](http://xuer.pzhao.net)* was published last month. Readers began to give me exciting feedback. It would be helpful to show them how to use R in the Steem community. I would expect that some of them could join me in developing steemr, which would be a valuable gift to the Steem community.

#### What is the project about?

steemr is an open source R package for playing with Steem data with R language. It is used to download, post process, analyze,  and visualize Steem data on the basis of the powerful statistic power of R. Currently, the version 0.0.0 can:

- obtain the complete post list for a given account,
- obtain the complete account information from steemdb.com,
- organized the 'follower' and 'following' information for a given account,
- obtain the following history of a given account,
- download the vote records of a given post, and
- download the complete data of the latest 100 posts of a given account.

![steemr.jpg](https://cdn.steemitimages.com/DQme3DVwGfWUPVHtiCzgVkjxbTz3256EccQdMW7hnBvzKVz/steemr.jpg)

A screenshot of running the current version (v.0.0.0) of steemr with RStudio

#### Technology Stack

steemr is developed in R language with the support of the RCurl package and the XML package.

#### Roadmap

In the future, I am going to add much more features to steemr, such as 

- building a personal blog website from the posts of a given account,
- building a book (in html, pdf, epub, word) from the posts of a given account,
- visualization of the Steem data in a variety of ways, such as statistical distributions, time series, word clouds,
- support for SteemSQL query and data analysis, and
- building a user-friendly web UI for those who knows nothing of R language.

![](https://steemitimages.com/DQma9ULTms89jkrCjvwvCcntLBa6Tj1DVXbWbokqYD4C3Vy/a8-1.jpeg)

One of steemr's future features: easily plot a word cloud from an ID' posts. image taken from [one of my Steem Watch posts](https://steemit.com/cn/@dapeng/steem-hannahwu).

#### How to contribute?

Anyone can get in touch with me by leaving me a reply on steem @dapeng or on https://github.com/pzhaonet/steemr.
