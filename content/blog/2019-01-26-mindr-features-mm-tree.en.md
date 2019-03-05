---
title: "mindr v.1.2.0 released: universal function and directory tree"
author: Peng Zhao
date: "2019-01-26"
slug: mindr-features-mm-tree
tags: 
  - R
  - mindr
  - news
banner: img/banners/logo-mindr.png
---


The new version 1.2.0 mainly brings four exciting features.

<!--more-->


1. Suggested by [@yihui](https://github.com/yihui), an argument of 'method' was added to each main functions. Users can choose the method of regular expression or pandoc to pick out the outline of a markdown file. 
2. Suggested by [the issue from the users](https://github.com/pzhaonet/mindr/issues/11), now mindr can save the mind map as an HTML widget file and share the mind map on web.
3. A new function `tree()` can create a mind map from a directory on your computer. See the following image as a demo.
4. A universal function `mm()` can convert the file formats automatically according to the suffix of the input file. This is a big step of mindr, because `mm()` wraps (almost) all the previous features into one function. Users do not have to memorize other functions.

![2019-01-27-002.png](https://cdn.steemitimages.com/DQmT3fxiojY6Lg7x3EdmPV7J8XpP54V73FRunejw18ANz3G/2019-01-27-002.png)


