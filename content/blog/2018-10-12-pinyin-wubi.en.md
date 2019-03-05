---
title: "[R: New Features on pinyin] Convert Chinese Characters into Sijiao and Wubi codes"
author: 赵鹏
date: "2018-10-12 13:31:42"
slug: pinyin-wubi
tags: 
  - pinyin
  - R
  - news
banner: img/banners/logo-pinyin.png
---

#### What features did I add?

- Four times faster for converting.
- At the beginning of the year 2018 I received an issue report by [psychelzh](https://github.com/pzhaonet/pinyin/issues/3#issue-295041288) about a polyphone error. Now a new pinyin library has been added, which more or less solved the polyphone problem.
- Convert Chinese characters into Sijiao codes (literally [four corner code](https://en.wikipedia.org/wiki/Four-Corner_Method)).
- and Wubi codes (literally [five-stroke](https://en.wikipedia.org/wiki/Wubi_method)).
- Some minor bugs were fixed.

<!--more-->


[![](https://cdn.steemitimages.com/DQmRtco1JZ19PSvq8RKGNN8CYxNKzzHqNdtUqqFjam1b2Zz/pinyin-test.jpg)](https://cdn.steemitimages.com/DQmRtco1JZ19PSvq8RKGNN8CYxNKzzHqNdtUqqFjam1b2Zz/pinyin-test.jpg)
Figure 1:  Test the new features in RStudio IDE

#### How did I implement them?

- Following [Qu Cheng](https://github.com/canalcheng)'s suggestions in personal communications, I converted the pinyin library into an environment to accelerate the converting procedure by the `pylib()` function.
- A new pinyin library '/inst/lib/zh2.txt' was added and a parameter `dic = c('zh', 'zh2')` in the `pylib()` function  allows the users to choose a preferable library for  polyphone.
- New functions `fclib()` and `four_corner()` imports a four-corner library and converts Chinese characters into four-corner codes, according to Qu Cheng's suggestions.
- A new function `wubi()` imports a five-stroke library and converts Chinese characters into five-stroke codes, again according to Qu Cheng's suggestions.
- The downstream functions `bookdown2py()`, `file.rename2py()`, `file2py()` were updated to support the updates mentioned above.

Each part of the functions are well documented. Other files were updated automatically by compilation. 

Link to relevant lines in the code on GitHub can be found mainly in my latest commit (click to see the details):

- [Faster. Users can preload the library. A simple library was added. Four-corner codes are supported.](https://github.com/pzhaonet/pinyin/commit/cbdd753a86744debdfccae1ce63c7870d4e808e1)
- [Convert Chnese characters into Wubi codes](https://github.com/pzhaonet/pinyin/commit/59aaf6aea73c6d73aaec9c6dcc38d402f98e06de)

