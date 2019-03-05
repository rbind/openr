---
title: "[New Features on steemr] Now steemr supports SteemSQL queries!"
author: Peng Zhao
date: "2018-06-18 15:06:48"
slug: steemr-steemsql
tags: 
  - R
  - steemr
  - news
banner: img/banners/logo-steemr.png
---


In the recent week, steemr has been updated from version 0.0.0 to version 0.0.5. Users can simply ignore 0.0.1 to 0.0.4, which were slightly modified to meet the requirements by CRAN. However, users cannot miss version 0.0.5, which now supports SteemSQL queries!

The main features of version 0.0.5 are listed as follows:

<!--more-->


- The following functions support SteemSQL queries with the parameter `method` to specify the server, and `sql_id` and `sql_password` to specify the SteemSQL ID and password, respectively:

  ```R
  follower(method = 'steemsql.com', 
           sql_id = your_id, 
           sql_password = your_password)
  id_info(method = 'steemsql.com', 
          sql_id = your_id, 
          sql_password = your_password)
  post_df(method = 'steemsql.com', 
          sql_id = your_id, 
          sql_password = your_password)
  post_id(method = 'steemsql.com', 
          sql_id = your_id, 
          sql_password = your_password)
  post_info(method = 'steemsql.com', 
            sql_id = your_id, 
            sql_password = your_password)
  post_links(method = 'steemsql.com', 
             sql_id = your_id, 
             sql_password = your_password)
  ```

  For example, users can get all the posts by an author from SteemSQL with a single command:

  ```R
  post_id(id = author_id, 
          method = 'steemsql.com', 
          sql_id = your_id, 
          sql_password = your_password)
  ```

  

  Of course, the pre-requirements is that you should have a valid SteemSQL ID. Go to https://steemsql.com and apply one.

  If you don't have a SteemSQL ID, you can simply ignore the `method` parameter, and retrieve data from steemdb.com by default.

- The documentation has been improved.

- Some minor literal chagnes.

#### How did I implement them?
I added the SQL queries with the R RODBC package and added the options that users can choose the server. Link to relevant lines in the code on GitHub can be found mainly in my latest commits:

https://github.com/pzhaonet/steemr/commit/617f36e6ae5c4aa0d06f1bc311f30afa75d38afb

The following figure shows how I updated a function as an example:

![2018-06-18-001.jpg](https://cdn.steemitimages.com/DQmYP1LxPnhqGMUXmpMLyNRhscmUgfaHwnwcughxec8MJzS/2018-06-18-001.jpg)
