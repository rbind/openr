---
title: "Build a mirror/backup site for your own steem posts in 30 minutes - 30 分钟搭建自己的 steem 镜像备份网站"
author: 赵鹏
date: "2017-11-06 09:44:42"
slug: build-a-mirror-backup-site-for-your-own-steem-posts-in-30-minutes-or-30-steem
tags: 
  - steemr
  - R
  - markdown
banner: img/banners/logo-steemr.png
---

Yesterday, I built two mirror sites for my steem posts ([mirror 1](https://dapeng.netlify.com/)，[mirror 2](https://steemit.netlify.com/)) as backups, which are synced automatically everyday, thanks to steemsql and steemdata. The mirror sites are very useful:

<!--more-->

1. for emergency, in case that steemit.com and busy.org are down,
2. as backups, in case that steemsql and steemdata are gone,
3. for revision, where the posts are allowed to be modified even after 7 days,
4. for more replies, thanks to disqus, 
5. for a stable looking, no matter how the interface of steemit changes in the future, and
6. for fast browsing, especially when your posts are more than 100.

Both of these sites are free of costs, and updated automatically. 

How long does it take to build a site like them?

Following my steps, it takes less than half an hour, if you are an expert on R language. For newbies, it depends on how long it takes you to learn R. Anyway, you will save much time that I wasted in many failed attempts.

![mirror1.jpg](https://steemitimages.com/DQmVGn1eWfueYNVC9Xw4Hy41F9xDPR16jdGojPCDcJsfVxv/mirror1.jpg)

Here are the steps.

### Build a Hugo site with R blogdown

1. Install R and RStudio.
2. Created a blogdown project from RStudio's menu.

### Download your posts from steemsql or steemdata

1. R RODBC can visit steemsql database, and R mongolite can visit steemdata database. Either is OK.
2. Download the target posts, and organize them into markdown files with R.
3. Copy the markdown files into the contents folder in your site folder.
4. Run the build_site() function in R blogdown.

### Publish your site folder to Github

Create a new repo on Github, and publish your site folder.

### Deploy with Netlify

1. Log in Netlify.com with your github account. 
2. Created a new site, choose your site folder from github, and use hugo_0.19 as the command.
3. Wait seconds or minutes, and you can visit your mirror sites!

### Sync automatically everyday

1. Write a .bat script on Windows, or .sh script on Linux, to call your R script, which downloads the new posts, builds the site, and syncs with Github repo.
2. Use the task scheduler on Windows or crontab on Linux to run the .bat or .sh automatically everyday or every hour or whatever.

That's all. Wish you success!


![mirror2.jpg](https://steemitimages.com/DQmbNZ7kw2ynuig2qZjhmDPHKynQobL2iiSatQsGJgQJZiB/mirror2.jpg)

