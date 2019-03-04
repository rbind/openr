---
title: "rosr News: a Shiny GUI and RStudio addin for choosing and creating sub-projects"
author: dapeng
date: "2019-01-31"
slug: rosr-shiny
tags: 
  - utopian-io
  - post
  - R
  - rosr
banner: img/banners/logo-rosr.png
---

'rosr' is an R package for creating reproducible academic project with integrated various academic elements, including data, bibliography, codes, images, manuscripts, dissertations, slides and so on. These elements are well connected so that they can be easily synchronized and updated. Users don't have to repeat copying and pasting their results and figures from time to time. It will be easy for the scientific researchers to use, even if they are R beginners, or even non-R-users.

<!--more-->


### New Features

In my previous about 'rosr', I planned 

1. to add more choices of the sub-projects with demos  to the arguments of the functions
2. to make a GUI for creating or maintaining a project for code-haters. 

Now these two tasks have been accomplished! And even more!

For Plan 1, individual functions for creating each sub-project as well as self-defined templates were created, shown in the following commits:

- [individual functions for each task of creating](https://github.com/pzhaonet/rosr/commit/78e832f575a7a6e39bc085a98544fd68e8e89bba)
- [self-defined templates](https://github.com/pzhaonet/rosr/commit/1ec6a597a22f1db9dbfd2e921bfab22f1feb90f5)

For Plan 2, a shiny app as well as a RStudio addin were created, shown in the following commits.

- [add shiny app](https://github.com/pzhaonet/rosr/commit/96334625e34f307fa2359231bab8f150f4c1f2e4)
- [add skeleton of the project](https://github.com/pzhaonet/rosr/commit/6f7b26304b099e36190d9c74cb5c18b06aabf2da)


Now non-R users don't have to run any R codes after installation. Just click the 'Addins' button in RStudio and you can find "Create a rosr project". 

![](https://github.com/rbind/pzhao/raw/master/static/img/rosr-addin.png)



Then a sheet will pop out, with all useful templates of journal manuscripts, posters, slides, books, dissertations and websites.

Click the elements you want, and click 'create'. You will get everything you like.

![](https://github.com/rbind/pzhao/raw/master/static/img/rosr-screenshot.png)

Furthermore, functions for reading and processing equations, for removing special characters, for installation of packages, as well as for collecting and displaying templates were added.

- [add internal functions](https://github.com/pzhaonet/rosr/commit/f7136797763fc971e51c885f534bb56bc773d333)
- [functions for processing maths expressions](https://github.com/pzhaonet/rosr/commit/1fec36dd677f84a61421b1c6717c63e33d3656f8)
- [functions for installing packages and for displaying templates](https://github.com/pzhaonet/rosr/commit/3193642c7f175d3a83676c00a85711608878f6d8)

Codes were improved by re-writing functions and adding comments.

- [use functions to avoid repeating codes](https://github.com/pzhaonet/rosr/commit/df08cbc70e97960e9019835f3f38b9c235473e8f)
- [add comments](https://github.com/pzhaonet/rosr/commit/1e5c0b0a58b64c871fa3794b8239934f8c9708a8)
- [update readme and description](https://github.com/pzhaonet/rosr/commit/2f409f782df40a75edd78bbb465f3bd11ba2d732)

