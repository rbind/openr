---
title: "[Tutorial for steemr] Installation + Retrieving and Analyzing Steemians' profiles"
author: dapeng
date: "2018-07-06 14:15:00"
slug: steemr-tutorial-gid
tags: 
  - utopian-io
  - post
  - steemr
  - R
  - tutorial
banner: img/banners/logo-steemr.png
---

### What Will I Learn?

-   Setting-up of the environment which steemr requires.
-   Using the function `gid()` to retrieve a Steemian's profile from the block chain or the data servers.
-   Using other R functions to enhance and analyze the data retrieved by `gid()`.

<!--more-->

### Requirements

-   Windows/mac/Linux OS
-   R environment
-   R steemr package
-   R steemr2 package
-   RStudio IDE (recommended)

### Difficulty

-   Intermediate

### Installation

***R***

R is a free, open-source, cross-platform programming language, which is very friendly to non-professional programmers. Although R was born for statistical analysis, nowadays it is popular not only in scientific research but also in industry. This tutorial will demonstrate how beginners can easily use R to process Steem data.

The installation of R can be found on the official website of the [Comprehensive R Archive Network (CRAN)](https://cran.r-project.org/) or in many textbooks such as *[Learning R: R for Rookies](https://steemit.com/cn/@dapeng/xuer-sale)*. For the tutorial's integrity, here is a brief description for Windows users. Mac and Linux users can simply follow the official manual by CRAN.

1.  Go to [CRAN](https://cran.r-project.org/). Click the right link in the list of 'Download and Install R' according to your platform. Here we click '[Download R for Windows](https://cran.r-project.org/bin/windows/)'.
2.  Click '[base](https://cran.r-project.org/bin/windows/base/)'.
3.  Click '[Download R 3.5.1 for Windows](https://cran.r-project.org/bin/windows/base/R-3.5.1-win.exe)'.

3.5.1 is the newest version number of R. It could be updated in the future.

Now we get a file 'R-3.5.1-win.exe' on the local disk. Double click it and click the 'Next...' button to complete the installation.

***RStudio***

The default R editor is primitive. We highly recommend the users to use a third-party editor, such as the free, cross-platform editor *RStudio IDE*.

1.  Go to the [download webpage of RStudio](https://www.rstudio.com/products/rstudio/download/#download).
2.  Click the download link according to your platform. Here we download [RStudio 1.1.453 - Windows Vista/7/8/10](https://download1.rstudio.org/RStudio-1.1.453.exe).

1.1.453 is the newest version number of RStudio. It could be updated in the future as well.

Now we get a file 'RStudio-1.1.453.exe' on the local disk. Double click it and click the 'Next...' button to complete the installation.

***'steemr' and 'steemr2' packages***

The 'steemr' package is availalbe on [CRAN](https://cran.r-project.org/package=steemr). However, we suggest the development version, which could be installed from github. The 'steemr2' package, forked from kharoof/steemR,  is available only on github.

The 'devtools' must be installed first. Open RStudio, and run the following codes.

    install.packages('devtools')

With the 'devtools' package, we could install the pacakge from github.

    devtools::install_github('pzhaonet/steemr')
    devtools::install_github('pzhaonet/steemr2')

### Basic usage of `gid()`

Load the 'steemr' and 'steemr2' packages:

    require('steemr')
    
    ## Loading required package: steemr
    
    require('steemr2')
    
    ## Loading required package: steemr2

The function name 'gid' means 'get ID information'. It is very easy to get a Steemian's profile. Simply run the code:

    gid('dapeng')
    
    ##        id             created      rep balance savings  vesting
    ## 1: dapeng 2016-10-14 11:03:39 67.00708  39.849       0 5027.933
    ##    vesting_delegated vesting_received
    ## 1:          4901.351         1514.774
    ##                                                                                       profile_links
    ## 1: https://cdn.steemitimages.com/DQmconigpzDwQGFdsDhV746bdfACHvZxeuQgSyotym6wgBV/peng_new_100.jpg  
    ##               profile_about profile_location
    ## 1: 事了拂衣去，深藏身与名。

It is a data frame with @dapeng's profile.

As we need this data frame for future use, it can be assigned to a variable:

    myid <- gid('dapeng')

What information do we have in 'myid'? Let's see the names of the columns:

    names(myid)
    
    ##  [1] "id"                "created"           "rep"              
    ##  [4] "balance"           "savings"           "vesting"          
    ##  [7] "vesting_delegated" "vesting_received"  "profile_links"    
    ## [10] "profile_about"     "profile_location"

The column names are self-explanary. We could extract any column by using the `$` operator. For example, let's see @dapeng's reputation.

    myid$rep
    
    ## [1] 67.00708

> Exercise 1: retrieve your own profile. Exercise 2: retrieve your friends' profiles.

### Advanced usage of `gid()`

Let's go further into `gid()`.

Two parameters are available for `gid()`:

-   `id` specifies the ID of interest, which is mandatory.
-   `mothod` specifies the data server to connect, which is optional. By default, `gid()` uses 'appbase\_api'.

We could get the ID data from steemdb.com as well, which provides much more information:

    myid_steemdb <- gid(id = 'dapeng', method = 'steemdb.com')
    myid_steemdb
    
    ## $`_id`
    ## [1] "dapeng"
    ## 
    ## ...
    ## ...
    ## ...
    ## $following_count
    ## [1] "95"
    ## 
    ## $proxy_witness
    ## [1] "0.000"
    ## 
    ## $total_balance
    ## [1] "39.849"
    ## 
    ## $total_sbd_balance
    ## [1] "1,321.780"
    ## 
    ## $scanned
    ## [1] "2018-07-06 11:01"
    ## 
    ## $`_dirty`
    ## [1] "1"

It is a long list with sufficient information of the ID. We could use the name() function to see what information we have got:

    names(myid_steemdb)
    
    ##  [1] "_id"                              
    ##  [2] "active"                           
    ##  [3] "active_challenged"                
    ##  [4] "average_bandwidth"                
    ##  [5] "average_market_bandwidth"         
    ##  [6] "balance"                          
    ##  [7] "can_vote"                         
    ##  [8] "comment_count"                    
    ##  [9] "created"                          
    ## [10] "curation_rewards"                 
    ## [11] "delegated_vesting_shares"         
    ## [12] "guest_bloggers"                   
    ## [13] "id"                               
    ## [14] "json_metadata"                    
    ## [15] "last_account_recovery"            
    ## [16] "last_account_update"              
    ## [17] "last_active_proved"               
    ## [18] "last_bandwidth_update"            
    ## [19] "last_market_bandwidth_update"     
    ## [20] "last_owner_proved"                
    ## [21] "last_owner_update"                
    ## [22] "last_post"                        
    ## [23] "last_root_post"                   
    ## [24] "last_vote_time"                   
    ## [25] "lifetime_bandwidth"               
    ## [26] "lifetime_market_bandwidth"        
    ## [27] "lifetime_vote_count"              
    ## [28] "market_history"                   
    ## [29] "memo_key"                         
    ## [30] "mined"                            
    ## [31] "name"                             
    ## [32] "next_vesting_withdrawal"          
    ## [33] "other_history"                    
    ## [34] "owner"                            
    ## [35] "owner_challenged"                 
    ## [36] "post_count"                       
    ## [37] "post_history"                     
    ## [38] "posting"                          
    ## [39] "posting_rewards"                  
    ## [40] "proxied_vsf_votes"                
    ## [41] "proxy"                            
    ## [42] "received_vesting_shares"          
    ## [43] "recovery_account"                 
    ## [44] "reputation"                       
    ## [45] "reset_account"                    
    ## [46] "reward_sbd_balance"               
    ## [47] "reward_steem_balance"             
    ## [48] "reward_vesting_balance"           
    ## [49] "reward_vesting_steem"             
    ## [50] "savings_balance"                  
    ## [51] "savings_sbd_balance"              
    ## [52] "savings_sbd_last_interest_payment"
    ## [53] "savings_sbd_seconds"              
    ## [54] "savings_sbd_seconds_last_update"  
    ## [55] "savings_withdraw_requests"        
    ## [56] "sbd_balance"                      
    ## [57] "sbd_last_interest_payment"        
    ## [58] "sbd_seconds"                      
    ## [59] "sbd_seconds_last_update"          
    ## [60] "tags_usage"                       
    ## [61] "to_withdraw"                      
    ## [62] "transfer_history"                 
    ## [63] "vesting_balance"                  
    ## [64] "vesting_shares"                   
    ## [65] "vesting_withdraw_rate"            
    ## [66] "vote_history"                     
    ## [67] "voting_power"                     
    ## [68] "withdraw_routes"                  
    ## [69] "withdrawn"                        
    ## [70] "witness_votes"                    
    ## [71] "witnesses_voted_for"              
    ## [72] "followers"                        
    ## [73] "followers_count"                  
    ## [74] "followers_mvest"                  
    ## [75] "following"                        
    ## [76] "following_count"                  
    ## [77] "proxy_witness"                    
    ## [78] "total_balance"                    
    ## [79] "total_sbd_balance"                
    ## [80] "scanned"                          
    ## [81] "_dirty"

If you have a SteemSQL ID and password, you could use the ssql function to build a connection to SteemSQl,

    mysql <- ssql(uid = your_steemsql_id, pwd = your_steemsql_password)

You have to replace `your_steemsql_id` and `your_steemsql_password` with your own.

Then get data from SteemSQL:

    myid_steemsql <- gid(id = 'dapeng', method = 'steemsql.com', sql_con = mysql)

> Exercise 3: get your own profile from steemdb.com. Exercise 4: get your friends profiles from steemdb.com.

### Enhancement of `gid()`

We could use other R functions to enhance the query by `gid()`.

For example, *[WinDa Choir](https://steemit.com/dlive/@dapeng/c452e870-54e2-11e8-8cf9-1b93be2e52ab)* is a group formed from me and three friends of mine on Steem. The members are:

    winda <- c('winniex', 'windowglass', 'davidke20', 'dapeng')

Now I need a list of the profiles of the members. The `lapply()` function could retrieve multiple IDs' profiles with one single line.

    winda_p <- lapply(winda, gid)
    winda_p
    
    ## [[1]]
    ##         id             created      rep balance savings  vesting
    ## 1: winniex 2017-09-20 05:00:42 61.42898   6.256       0 2104.818
    ##    vesting_delegated vesting_received
    ## 1:          916.7597         48.25345
    ##                                                                                                                                                                      profile_links
    ## 1: https://steemitimages.com/DQmdp5K7PsqX6uFyDD3zrqYj6zvy9773XjshybhWbHY6KY2/kitten-163627_960_720.jpg  https://cdn.pixabay.com/photo/2016/12/09/08/09/texture-1893788_960_720.jpg
    ##                profile_about profile_location
    ## 1: From the very beginning,                  
    ## 
    ## [[2]]
    ##             id             created      rep balance savings  vesting
    ## 1: windowglass 2017-10-09 04:16:03 54.51495   0.006       0 1727.516
    ##    vesting_delegated vesting_received
    ## 1:          701.2447                0
    ##                                                                                                                                       profile_links
    ## 1: http://img1.ph.126.net/JIGlaEsqKaLZXd25cKoD2w==/1286059168610796619.jpg  http://img1.ph.126.net/5iZjixj-wLawyMNjmL6mug==/6632751118002457471.jpg
    ##             profile_about profile_location
    ## 1: 不要被我的声音骗了呀……                 
    ## 
    ## [[3]]
    ##           id             created      rep balance savings  vesting
    ## 1: davidke20 2017-08-16 01:07:06 58.77397   6.023       0 616.8284
    ##    vesting_delegated vesting_received
    ## 1:          120.4208                0
    ##                                                                                                                                                  profile_links
    ## 1: https://i.imgur.com/viuSsXg.jpg  https://steemit-production-imageproxy-thumbnail.s3.amazonaws.com/DQmReeS8DTkceS6RShqfz9FVnuF5Te84mXLohiLMT7xVyQ8_1680x8400
    ##                                       profile_about profile_location
    ## 1: Mediocre old man with slight interests in crypto     Kuala Lumpur
    ## 
    ## [[4]]
    ##        id             created      rep balance savings  vesting
    ## 1: dapeng 2016-10-14 11:03:39 67.00708  39.849       0 5027.933
    ##    vesting_delegated vesting_received
    ## 1:          4901.351         1514.774
    ##                                                                                       profile_links
    ## 1: https://cdn.steemitimages.com/DQmconigpzDwQGFdsDhV746bdfACHvZxeuQgSyotym6wgBV/peng_new_100.jpg  
    ##               profile_about profile_location
    ## 1: 事了拂衣去，深藏身与名。

We get a list with the profiles of all the Winda members.

For convienance, the `do.call()` function can convert the list into a simple data frame like this:

    winda_df <- do.call(rbind.data.frame, winda_p)
    winda_df
    
    ##             id             created      rep balance savings   vesting
    ## 1:     winniex 2017-09-20 05:00:42 61.42898   6.256       0 2104.8184
    ## 2: windowglass 2017-10-09 04:16:03 54.51495   0.006       0 1727.5159
    ## 3:   davidke20 2017-08-16 01:07:06 58.77397   6.023       0  616.8284
    ## 4:      dapeng 2016-10-14 11:03:39 67.00708  39.849       0 5027.9328
    ##    vesting_delegated vesting_received
    ## 1:          916.7597         48.25345
    ## 2:          701.2447          0.00000
    ## 3:          120.4208          0.00000
    ## 4:         4901.3508       1514.77416
    ##                                                                                                                                                                      profile_links
    ## 1: https://steemitimages.com/DQmdp5K7PsqX6uFyDD3zrqYj6zvy9773XjshybhWbHY6KY2/kitten-163627_960_720.jpg  https://cdn.pixabay.com/photo/2016/12/09/08/09/texture-1893788_960_720.jpg
    ## 2:                                http://img1.ph.126.net/JIGlaEsqKaLZXd25cKoD2w==/1286059168610796619.jpg  http://img1.ph.126.net/5iZjixj-wLawyMNjmL6mug==/6632751118002457471.jpg
    ## 3:                     https://i.imgur.com/viuSsXg.jpg  https://steemit-production-imageproxy-thumbnail.s3.amazonaws.com/DQmReeS8DTkceS6RShqfz9FVnuF5Te84mXLohiLMT7xVyQ8_1680x8400
    ## 4:                                                                                https://cdn.steemitimages.com/DQmconigpzDwQGFdsDhV746bdfACHvZxeuQgSyotym6wgBV/peng_new_100.jpg  
    ##                                       profile_about profile_location
    ## 1:                        From the very beginning,                  
    ## 2:                           不要被我的声音骗了呀……                 
    ## 3: Mediocre old man with slight interests in crypto     Kuala Lumpur
    ## 4:                         事了拂衣去，深藏身与名。

Now we can save the data frame as a spread sheet, which could be opened with Excel.

    write.csv(winda_df, file = 'winda.csv', row.names = FALSE)

> Exercise 5: get the profiles of a group of Steemians in which you are involved.

### Analysis of the ID profiles

With the data retrieved via `gid()`, we could produce a summary report of the *Winda Choir* members:

    summary(winda_df)
    
    ##       id               created                         rep       
    ##  Length:4           Min.   :2016-10-14 11:03:39   Min.   :54.51  
    ##  Class :character   1st Qu.:2017-05-31 15:36:14   1st Qu.:57.71  
    ##  Mode  :character   Median :2017-09-02 15:03:54   Median :60.10  
    ##                     Mean   :2017-06-22 23:21:52   Mean   :60.43  
    ##                     3rd Qu.:2017-09-24 22:49:32   3rd Qu.:62.82  
    ##                     Max.   :2017-10-09 04:16:03   Max.   :67.01  
    ##     balance          savings     vesting       vesting_delegated
    ##  Min.   : 0.006   Min.   :0   Min.   : 616.8   Min.   : 120.4   
    ##  1st Qu.: 4.519   1st Qu.:0   1st Qu.:1449.8   1st Qu.: 556.0   
    ##  Median : 6.139   Median :0   Median :1916.2   Median : 809.0   
    ##  Mean   :13.034   Mean   :0   Mean   :2369.3   Mean   :1659.9   
    ##  3rd Qu.:14.654   3rd Qu.:0   3rd Qu.:2835.6   3rd Qu.:1912.9   
    ##  Max.   :39.849   Max.   :0   Max.   :5027.9   Max.   :4901.4   
    ##  vesting_received  profile_links      profile_about     
    ##  Min.   :   0.00   Length:4           Length:4          
    ##  1st Qu.:   0.00   Class :character   Class :character  
    ##  Median :  24.13   Mode  :character   Mode  :character  
    ##  Mean   : 390.76                                        
    ##  3rd Qu.: 414.88                                        
    ##  Max.   :1514.77                                        
    ##  profile_location  
    ##  Length:4          
    ##  Class :character  
    ##  Mode  :character  
    ##                    
    ##                    
    ## 

From the summary, we could find the statistics of the minimum (Min), median, mean, and maximum (Max) of the registration time, reputation, steem power (vesting), and delegation.

The data frame could be visualized in diagrams as well:

    barplot(winda_df$rep, names.arg = winda_df$id, main = 'Reputation of Winda')

<img src="https://raw.githubusercontent.com/pzhaonet/steemr-book/master/img/fig-gid-1-1.png" style="display: block; margin: auto;" />


We could try another example: the authors of the Steem Handbook.

[Steem Handbook](https://steemit.com/steem/@steemh/steem-handbook-calls-for-support) is a tutorial to help Steemians to survive on Steem and develop their social communications. It is written by multiple authors from the CN community. The authors of Part I are:

    steemh <- c("dapeng","hepeng.chn","incrediblesnow","ivysrono","jaffer","lixing","maiyude","meixia","oflyhigh","rivalhw","skenan","tumutanzi","vickylin","wang-peilin","woolfe19861008","yellowbird")

Similarly to the example of Winda, we can get the profiles of these authors easily:

    steemh_l <- lapply(steemh, gid)
    steemh_df <- do.call(rbind.data.frame, steemh_l)
    summary(steemh_df)
    
    ##       id               created                         rep       
    ##  Length:16          Min.   :2016-07-25 03:11:30   Min.   :42.20  
    ##  Class :character   1st Qu.:2017-04-21 10:03:48   1st Qu.:53.43  
    ##  Mode  :character   Median :2017-09-10 08:17:12   Median :57.72  
    ##                     Mean   :2017-07-20 18:50:48   Mean   :58.73  
    ##                     3rd Qu.:2017-12-26 14:46:03   3rd Qu.:65.03  
    ##                     Max.   :2018-03-13 10:48:12   Max.   :75.38  
    ##     balance             savings             vesting         
    ##  Min.   :   0.0000   Min.   :0.0000000   Min.   :    3.631  
    ##  1st Qu.:   0.7468   1st Qu.:0.0000000   1st Qu.:  107.391  
    ##  Median :  21.1785   Median :0.0000000   Median :  523.849  
    ##  Mean   : 121.8104   Mean   :0.0001875   Mean   : 5542.820  
    ##  3rd Qu.:  52.0455   3rd Qu.:0.0000000   3rd Qu.: 6770.373  
    ##  Max.   :1118.6010   Max.   :0.0030000   Max.   :31354.894  
    ##  vesting_delegated vesting_received profile_links      profile_about     
    ##  Min.   :   0.00   Min.   :    0    Length:16          Length:16         
    ##  1st Qu.:  19.89   1st Qu.:    0    Class :character   Class :character  
    ##  Median : 105.38   Median :    0    Mode  :character   Mode  :character  
    ##  Mean   :1133.98   Mean   : 6390                                         
    ##  3rd Qu.:1101.05   3rd Qu.:  931                                         
    ##  Max.   :6009.93   Max.   :49274                                         
    ##  profile_location  
    ##  Length:16         
    ##  Class :character  
    ##  Mode  :character  
    ##                    
    ##                    
    ## 

Now we can plot a histogram which displays the distribution of the authors' reputations.

    beginr::plothist(steemh_df$rep, show_normline = T, show_skewness = FALSE)



<img src="https://raw.githubusercontent.com/pzhaonet/steemr-book/master/img/fig-gid-2-1.png" style="display: block; margin: auto;" />

The reputation ranges  from 42 to 75, indicating that the authors include both rookies and high-level steemians. The median of the authors' repuation is 58. Half of the authors have a reputation between 52 and 56. Yes, most of the authors are from the middle class.

As `gid()` imports the Steemians' profile data into R, the users are free to use many powerful R functions to do whatever they want.

> Exercise 6: plot a hist diagram for the Steem Power (SP) of the group in which you are involved.

