---
title: "[New Features on beginr] Automatically generate a self-contained package"
author: 赵鹏
date: "2019-01-26"
slug: beginr-features-packr
tags: 
  - R
  - beginr
  - news
banner: img/banners/logo-beginr.png
---


Most R beginners think that developing an R package is a mission impossible. It is not true. With the new function `packr()` , users can create a user-defined useful R packages easily. They can specify in `packr()`a group of packages (e.g. foo_1, foo_2, foo_x) which they often use and the new package name, say `foobar`, then a new package called `foobar` will be generated. 

<!--more-->


When loading the `foobar` function, the package group, i.e. foo_1, foo_2, and foo_x are loaded simultaneously. Moreover, a few functions are available in the `foobar` package , which are well documented in the help. Briefly speaking, these functions can update the package group to the latest versions, check the conflicts with other loaded packages, list the dependencies, and so on. The user can share the `foobar` package to friends or the community as well. 

The  core codes of `packr()` are written in [R/packr.R](https://github.com/pzhaonet/beginr/blob/master/R/packr.R), which calls multiple scripts and templates in [inst/skeleton](https://github.com/pzhaonet/beginr/tree/master/inst/skeleton).


