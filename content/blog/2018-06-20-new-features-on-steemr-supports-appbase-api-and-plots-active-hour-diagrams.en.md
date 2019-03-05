---
title: "[New Features on steemr] supports AppBase API and plots active hour diagrams!"
author: Peng Zhao
date: "2018-06-20 10:44:24"
slug: new-features-on-steemr-supports-appbase-api-and-plots-active-hour-diagrams
tags: 
  - steemr
  - R
  - news
banner: img/banners/logo-steemr.png
---


- I have submitted steemr to CRAN and now it is [available](https://CRAN.R-project.org/package=steemr). Users can install steemr directly from CRAN:

<!--more-->


  ```
  install.packages('steemr)
  ```

  

- Users can use `method = 'appbase_api'` to download Steem data from AppBase API:

  ```
  ```

  

- A new powerful function `hourrose()` was added to plot a diagram of an ID's active hours in a day based on the post or comment time.

  ```
  hourrose(my_df = posts, col_time = 'created')
  ```

  ![](https://steemitimages.com/0x0/https://cdn.steemitimages.com/DQmRo9HESgtkrSZnvZN9bLq74SXSgT7k7wXuZurqucyFxkv/guess-2-5-hr.png)

  This 24-hour clock shows the active hours of an ID.  Users can even choose whether to display another parameter, such as vote number on these posts. Here is a screenshot of plotting such a image in RStudio IDE.

  ![steemr-hourrose.jpg](https://cdn.steemitimages.com/DQmfHm3cpHZuXPGE873Q41C55f8A6yEi711kPXPQcVfwWMv/steemr-hourrose.jpg)

  More feature of this function can be found in the help documentation:


  ```
  help(hourrose)
  ```

- Although SteemData is gone, I still added the query method from steemdata.com. I wish SteemData could come back some day. I love it.
- The documentation has been improved.
- Some minor literal chagnes.

#### How did I implement them?
I added the AppBase API option to the `id_info()` function and `post_id()` function with the support from ' kharoof/steemR' repo. 

I added the queries for SteemData with the R mongolite package and added the options that users can choose the server.  

I added a new function `hourrose()` originated from a windrose plotting method but tailored for Steem data.

![2018-06-20-004.jpg](https://cdn.steemitimages.com/DQmfMFaoppHg1H1TYBqspTPbabUvwLBoqsVWFaD9K3qh9aC/2018-06-20-004.jpg)

All these changes can be found in 'R/steemr.R'.

Links to relevant lines in the code on GitHub can be found mainly in my latest commits:

- https://github.com/pzhaonet/steemr/commit/8062db25a5b21708d5f1297e639bc19c2ec79b2b
- https://github.com/pzhaonet/steemr/commit/6740ddc9024609ee0dbbae7e14fd73b0e18b0402

