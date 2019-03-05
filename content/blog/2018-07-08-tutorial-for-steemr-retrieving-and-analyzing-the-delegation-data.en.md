---
title: "[Tutorial for steemr] Retrieving and Analyzing the delegation Data"
author: Peng Zhao
date: "2018-07-08 21:08:06"
slug: tutorial-for-steemr-retrieving-and-analyzing-the-delegation-data
tags: 
  - steemr
  - R
  - tutorial
banner: img/banners/logo-steemr.png
---

### What Will I Learn?

-   Using the function `gdelegation()` to retrieve and visualize the delegation data.
-   Using the function `gspmv()` to retrieve the value of Steem per MVests.
-   Using other R functions to enhance and analyse the data retrieved by `gdelegation()`.

<!--more-->

### Requirements

-   Windows/mac/Linux OS
-   R environment
-   R steemr package
-   RStudio IDE (recommended)

### Difficulty

-   Intermediate

### Basic usage of `gdelegation()`

Load the 'steemr' package:

    require('steemr')
    
    ## Loading required package: steemr

The function name 'gdelegation' means 'get the delegation data'. You could easily get the delegation data if you have a SteemSQL ID and password. Simply use the `ssql()` function to build a connection to SteemSQl,

    mysql <- ssql(uid = your_steemsql_id, pwd = your_steemsql_password)

You have to replace `your_steemsql_id` and `your_steemsql_password` with your own.

Then run the code to get the delegation records of @dapeng:

    myid <- 'dapeng'
    ## dlgt <- gdelegation(id = myid, sql_con = mysql)
    dlgt
    
    ##         ID     tx_id delegator  delegatee vesting_shares
    ## 1   189912 111344325    dapeng     justyy            0.0
    ## 2  2586287 464486800    dapeng    cnbuddy      3045049.0
    ## 3  2586326 464489466    dapeng    team-cn      4060064.8
    ## 4  2586348 464490700    dapeng    cnbuddy      4060064.5
    ## 5  2586442 464497235    dapeng julian2013       609009.6
    ## 6  2586454 464498225    dapeng    maiyude      1015015.9
    ## 7   189047 106837325    dapeng     justyy      2059990.3
    ## 8   471086 194798414    dapeng    cnbuddy      1024245.2
    ## 9   876298 250314037    dapeng     steemh      5111763.5
    ## 10 1269416 317662869    dapeng     jaffer       204017.0
    ## 11 1267717 312768666    dapeng     steemh       204049.7
    ## 12 2607953 468560846    dapeng     justyy       202969.2
    ## 13  468046 181975431 angelfund     dapeng      3074182.4
    ## 14 1589761 371652248    dapeng     jaffer            0.0
    ## 15 2429164 438333724    dapeng     steemh            0.0
    ##              timestamp
    ## 1  2017-09-26 10:36:18
    ## 2  2018-07-01 01:06:06
    ## 3  2018-07-01 01:09:51
    ## 4  2018-07-01 01:11:33
    ## 5  2018-07-01 01:21:27
    ## 6  2018-07-01 01:22:42
    ## 7  2017-09-19 23:17:30
    ## 8  2018-01-07 21:09:06
    ## 9  2018-02-13 15:20:51
    ## 10 2018-03-27 19:39:06
    ## 11 2018-03-24 17:27:51
    ## 12 2018-07-04 13:23:03
    ## 13 2017-12-29 10:15:54
    ## 14 2018-04-30 10:27:12
    ## 15 2018-06-11 17:11:24

There are 15 records with 6 columns with the self-explanatory column names.

The records only show the vesting shares. How much is the SBD? We could use the fuction `gspmv()` function, which means 'get the value of Steem per Mvests':

    spmv <- gspmv()
    spmv
    
    ## [1] 492.7857

Then we are able to convert the vesting shares into SBDs.

    dlgt$sbd <- dlgt$vesting_shares * spmv / 1000000

> Exercise 1: Get the delegation records of your own ID. How many delagation events have you had as the delegator and ghe delegatee, respectively?

It is easy to pick out the records where @dapeng was the delegator:

    dlgt[dlgt$delegator == myid, c(4,6,7)]
    
    ##     delegatee           timestamp       sbd
    ## 1      justyy 2017-09-26 10:36:18    0.0000
    ## 2     cnbuddy 2018-07-01 01:06:06 1500.5565
    ## 3     team-cn 2018-07-01 01:09:51 2000.7417
    ## 4     cnbuddy 2018-07-01 01:11:33 2000.7416
    ## 5  julian2013 2018-07-01 01:21:27  300.1112
    ## 6     maiyude 2018-07-01 01:22:42  500.1853
    ## 7      justyy 2017-09-19 23:17:30 1015.1337
    ## 8     cnbuddy 2018-01-07 21:09:06  504.7333
    ## 9      steemh 2018-02-13 15:20:51 2519.0038
    ## 10     jaffer 2018-03-27 19:39:06  100.5366
    ## 11     steemh 2018-03-24 17:27:51  100.5528
    ## 12     justyy 2018-07-04 13:23:03  100.0203
    ## 14     jaffer 2018-04-30 10:27:12    0.0000
    ## 15     steemh 2018-06-11 17:11:24    0.0000

or the delegatee:

    dlgt[dlgt$delegatee == myid, c(2,6, 7)]
    
    ##        tx_id           timestamp      sbd
    ## 13 181975431 2017-12-29 10:15:54 1514.913

### Advanced usage of `gdelegation()`

Let's go further into `gdelegation()`.

Three parameters are available for `gdelegation()`:

-   `id` specifies the ID of interest, which is mandatory.
-   `sql_con` specifies the connection to SteemSQL, which is mandatory.
-   `if_plot` specifies whether to visualize the delegation records in a figure. Optional.

We could plot a figure to view the delegation records like this:

    dlgt <- gdelegation(id = myid, sql_con = mysql, if_plot= T)

<img src="https://github.com/pzhaonet/steemr-book/raw/master/img/gdelegation-1-1.png" style="display: block; margin: auto;" />

@dapeng does not have many records. We could give another example: @cnbuddy.

    dlgt_cnbuddy <- gdelegation(id = 'cnbuddy', sql_con = mysql, if_plot= T)

<img src="https://github.com/pzhaonet/steemr-book/raw/master/img/gdelegation-2-1.png" style="display: block; margin: auto;" />

> Exercise 2: Plot the diagram of your own delegation records.

### Analysis of the data retrieved via `gdelegation()`

Using other R functions, we could easily get some statistics of the delegation data. Here we give an example.

Although there are 457 records in @cnbuddy's delegation history, some people appeared in @cnbuddy's delegator list for multiple times. Let's see how many unique delegators:

    length(unique(dlgt_cnbuddy$delegator))
    
    ## [1] 213

What is the maximum and minimum delegation? We can use the `summary()` function:

    dlgt_cnbuddy$sbd <- dlgt_cnbuddy$vesting_shares * spmv / 1000000
    summary(dlgt_cnbuddy$sbd[dlgt_cnbuddy$sbd > 0])
    
    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ##    1.002    2.018   50.272  247.939  323.215 3035.386

Who delegated more than 3000 sbd to @cnbuddy? The `which.max()` function could help:

    dlgt_cnbuddy[which.max(dlgt_cnbuddy$sbd), ]
    
    ##         ID     tx_id delegator delegatee vesting_shares
    ## 118 305513 150380546    skenan   cnbuddy        6159648
    ##               timestamp      sbd
    ## 118 2017-11-22 22:24:03 3035.386

> Exercise 4: Find the maximum and minimum delegation that an ID has ever got.

