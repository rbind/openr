---
title: "[New Features on steemr] Functions for accounts and comments report!"
author: dapeng
date: "2018-07-03 09:59:42"
slug: new-features-on-steemr-functions-for-accounts-and-comments-report
tags: 
  - utopian-io
  - post
  - steemr
  - R
banner: img/banners/logo-steemr.png
---

#### What features did I add?

New functions were added to the steemr pakcage, which now can retrieve the account data and the comment data and plot diagrams automatically. 

<!--more-->

  - `gaccounts()` retrieves the account data from the server, makes a summary of the account data, and plots a time series of the daily new accounts automatically. 

Here is an example, showing the daily new steem accounts in a diagram and a table from 2018/01/01 to 2018/07/01 produced by `gaccounts()` :

![gaccounts.jpeg](https://cdn.steemitimages.com/DQmcyD4WAEAjNXa5eYHmuTF3NPWB62oRPxdX7ZLHE4onCBF/gaccounts.jpeg)

```
          date  Freq
1   2017-12-31  1161
2   2018-01-01  1397
3   2018-01-02  8638
4   2018-01-03  6901
5   2018-01-04  2660
6   2018-01-05  7979
7   2018-01-06  4940
8   2018-01-07  8391
9   2018-01-08  4340
10  2018-01-09  5122
...
178 2018-06-26   545
179 2018-06-27   460
180 2018-06-28   405
181 2018-06-29   376
182 2018-06-30   353
183 2018-07-01   321
```

  - `gcomments()` retrieves the comment data from the server, makes a summary of the comment data, and plots a time series of the daily comments of a given ID automatically.


Here is an example , showing the daily comments (posts and replies) of my own in a diagram and a table produced by `gcomments()` :

![gcomments.jpeg](https://cdn.steemitimages.com/DQmXV6mdahviypxkCDavFAXDs6q5Y5z4tQYrwmvnW7PECN9/gcomments.jpeg)

```
        date Freq
1 2017-07-17    9
2 2017-07-18    3
3 2017-07-19    8
4 2017-07-20    9
5 2017-07-21    1
6 2017-07-22    4
...
311 2018-06-27   10
312 2018-06-28   10
313 2018-06-29    3
314 2018-06-30    4
315 2018-07-01   15
316 2018-07-02   10
```

These main functions are supported by some other functions:

  - `adailyf()`, which produces a daily summary and a daily diagram from a give data set,
  - `pdate()` and `xatf()`, which were tailored to plot time series of Steem data. 


The old functions were renamed for better understanding. The meaning of the beginning letter in a function name:
  - a: analysis
  - g: get data
  - p: plot a diagram

The script files were re-organized, according to the functions.

Some minor literal changes and small bugs were fixed as well.


#### How did I implement them?

I split the former 'R/steemr.R' into 'R/plothour.r', 'R/analysis.r', and 'R/get.r'.

I created new scripts 'R/internal.r' for internal used function, 'R/plot.r' for plotting functions, and 'R/import.r' for importing some external packages

I added the new functions into 'R/plot.r', 'R/analysis.r' and 'R/get.r'

Links to relevant lines in the code on GitHub can be found mainly in my latest commits (click to see the details):

- [v0.0.8. Re-organized. New functions.](https://github.com/pzhaonet/steemr/commit/842ddc86a681b0253b321f7665b91ae71fa54240).
- [bugs fixed. code improvement.](https://github.com/pzhaonet/steemr/commit/4e0f0da847035d9cd7a543c1b1abdb0b20021b62)
- [minor bugs fixed: lattice::](https://github.com/pzhaonet/steemr/commit/dbe3067d47d9d688f1e8a5ef1c95bfa9594cd84a)
- [a small format fixed](https://github.com/pzhaonet/steemr/commit/062db75b03295a613b371e59ae2243ddb33b96c8)
- [a minor bug fixed](https://github.com/pzhaonet/steemr/commit/83c76052046a833f8615dd2a7b74d8121cd225bc)
