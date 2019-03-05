---
title: "[New Features on steemr] Functions for delegation report and CNer report!"
author: Peng Zhao
date: "2018-07-09 12:26:30"
slug: steemr-delegation-cner
tags: 
  - R
  - steemr
  - news
banner: img/banners/logo-steemr.png
---

#### What features did I add?

- The new function`gspmv()` retrieves the value of Steem per MVests from the server. 


- The new function`gdelegation()` retrieves the delegation data from the server, makes a summary, and plot a time series automatically. 

<!--more-->

Here is an example, showing the delegation records of mine in a diagram and a table produced by `gdelegation('dapeng')` :

![gdelegation.jpeg](https://cdn.steemitimages.com/DQmY3H5SBNzHeqNqThbTBfngxocYTwWJkWAAPMLy89xZmUE/gdelegation.jpeg)

```
        ID     tx_id delegator  delegatee vesting_shares           timestamp
...
3  1269416 317662869    dapeng     jaffer       204017.0 2018-03-27 17:39:06
4  2429164 438333724    dapeng     steemh            0.0 2018-06-11 15:11:24
6   468046 181975431 angelfund     dapeng      3074182.4 2017-12-29 09:15:54
7  1589761 371652248    dapeng     jaffer            0.0 2018-04-30 08:27:12
8  2586287 464486800    dapeng    cnbuddy      3045049.0 2018-06-30 23:06:06
9  2586326 464489466    dapeng    team-cn      4060064.8 2018-06-30 23:09:51
10 2586348 464490700    dapeng    cnbuddy      4060064.5 2018-06-30 23:11:33
11 2586442 464497235    dapeng julian2013       609009.6 2018-06-30 23:21:27
12 2586454 464498225    dapeng    maiyude      1015015.9 2018-06-30 23:22:42
...
```

- As the Steemians who are active in the CN category have now built a CN community, the function `gcner()` retrieves the account profiles of the community members  and processes the data. Here is a table obtained by `gcner()`:

```
N   rep         sp          esp online    steem      sbd     vp        value level intro             name
228   1.0 75.72 140116.981 9.065152e+05    699   17.113 4388.761  90.90 1.876932e+05     5    NA        sweetsssj
210   2.0 75.36  31249.809 7.822462e+04    708   23.659  480.664  77.39 4.140846e+04     4    NA         oflyhigh
130   3.0 72.98  24247.788 7.350785e+04    716  236.704 2957.416  45.54 3.498470e+04     4    NA           ace108
415   4.0 72.69  16469.155 6.270835e+04    705   30.196   31.670  92.40 2.161388e+04     4    NA          rivalhw
168   5.0 74.05  16124.248 6.236688e+04    719  267.093 2901.328  52.98 2.435279e+04     4    NA          deanliu
```

The 'intro' column is unavailable yet, which will be filled with the self-introduction post of each ID in the future.

- The `acnsub()` function produces a summary of the CN sub-categories, i.e. the categories beginning with 'cn-', which can help the CNers choose the tags when posting. 


  Here is a diagram of the Top 20 active CN sub categories and a table produced by `acnsub()` as an analysis of the data between June 28 to 2 July, 2018.

  ![acnsub.jpeg](https://cdn.steemitimages.com/DQmSaqJ1YDDu1ttMFC18GLR1G9dpLUJte4TEqg4o4G2AVTD/acnsub.jpeg)

  ```
                      tags Freq
  30             cn-reader  163
  22           cn-malaysia   48
  34              cn-stats   36
  11     cn-cryptocurrency   23
  32               cn-shui   17
  39              cn-voice   11
  17              cn-funny    8
  21         cn-literature    7
  12            cn-drawing    6
  7                cn-book    5
  9                cn-chat    5
  18              cn-games    5
  44       teamcn-homework    5
  4                 cn-ask    4
  6                cn-blog    4
  8         cn-calligraphy    4
  10            cn-contest    4
  15               cn-food    4
  37              cn-study    4
  40              cn-weiqi    4
  16           cn-foodporn    3
  19          cn-interview    3
  24 cn-monthlyachievement    3
  29        cn-programming    3
  31            cn-reading    3
  42            cn-writing    3
  2                  cn-31    2
  20               cn-kids    2
  23              cn-money    2
  27        cn-photography    2
  ```

  <U+200B>

- Some minor literal changes in the documentation were performed and small bugs were fixed.

#### How did I implement them?

I added these new functions in  'R/analysis.r'  and 'R/get.r', as well as an internal function in 'R/internal.r'. Other files were updated automatically by compilation. 

Link to relevant lines in the code on GitHub can be found mainly in my latest commit (click to see the details):

- [New functions: gspmv(), gdelegation(), gcner(), acnsub().](https://github.com/pzhaonet/steemr/commit/7d976f17c1fb657821cb281aabc4916d784dfb3e)

