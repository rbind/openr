---
title: "R pinyin 包教程：安装和快速入门"
author: Peng Zhao
date: "2019-04-09"
slug: pinyin-tutorial-quick-start
tags: 
  - R
  - pinyin
  - tutorial
banner: img/banners/logo-pinyin.png
---


-   学习目标
    -   了解 R ‘pinyin’ 包的用途。
    -   学会为 ‘pinyin’ 搭建运行环境。
    -   掌握 ‘pinyin’ 包的基本用法
-   依赖条件
    -   Windows/mac/Linux 操作系统
    -   R 语言
    -   R pinyin 包
    -   RStudio IDE (推荐)
-   难度
    -   容易

<!--more-->

R ‘pinyin’ 包是什么
-------------------

顾名思义，‘pinyin’ 是一个将中文字符转换成汉语拼音的 R 语言包。除了拼音，它还能转换成四角号码、五笔字型，或者用户自定义的任何符号。

至于什么是汉语拼音，就不用多做解释了。除中国大陆地区外，新加坡、马来西亚、菲律宾和美国唐人街等，都在使用汉语拼音。台湾自2008年开始，中文译音使用原则也采用汉语拼音。

五笔字型是除汉语拼音外常用的中文输入法。四角号码是除拼音、部首检字法外重要的检字法。

R ‘pinyin’ 包相当于一个字典。如果掌握了它的用法，你会发现，它不只是个字典。

搭建环境
--------

使用 ‘pinyin’ 包之前，必须安装 R 语言。R 是免费、开源、跨平台的编程语言，对像我这样的非专业程序员非常友好。

R 语言的安装见官方平台 [Comprehensive R Archive Network (CRAN)](https://cran.r-project.org/)，或者参考相关教材（例如我写的 《*[学 R：零基础学习 R 语言](http://xuer.dapengde.com/)*》)。为了保证本教程的完整性，这里简述一下 Windows 操作系统里 R 语言的安装。

1.  在 [CRAN](https://cran.r-project.org/) 主页的 ‘Download and Install R’ 列表里选择适合你的平台的软件包。Windows 用户点击 ‘[Download R for Windows](https://cran.r-project.org/bin/windows/)’。
2.  点击 ‘[base](https://cran.r-project.org/bin/windows/base/)’。
3.  点击 ‘[Download R 3.5.3 for Windows](https://cran.r-project.org/bin/windows/base/R-3.5.3-win.exe)’。这是目前的最新版。
4.  双击下载得到的 ‘R-3.5.3-win.exe’，然后一路点击 ‘Next…’ 按钮，就完成了安装。

R 默认的编辑器简陋得不像话。我们大力推荐用户使用第三方编辑器，例如免费跨平台的 *RStudio IDE*。访问[RStudio 的下载页面](https://www.rstudio.com/products/rstudio/download/#download)，根据你的操作系统来选择合适的软件包。这里，我们下载 ‘RStudio 1.1.463 - Windows Vista/7/8/10’。双击下载得到的文件，一路点击 ‘Next…’ 就行了。.

图 1 展示了 RStudio 的用户界面。

![RStudio IDE](https://cdn.steemitimages.com/DQmc656HK9LmfyXJUK8EnxKHJ3bAB9hTV3eEJaHGupkDM6b/pinyin2.jpg)

安装和加载 ‘pinyin’ 包
----------------------

‘pinyin’ 在 CRAN 已上线，可以在 RStudio 里使用常规的 R 包安装方式进行安装稳定版：

    install.packages('pinyin')

或者安装开发版，比稳定版要新：

    devtools::install_github("pzhaonet/pinyin")

然后，使用下面的语句加载：

    require('pinyin')

    ## Loading required package: pinyin

‘pinyin’ 包的函数
-----------------

用户可以使用下面的命令，来查看 ‘pinyin’ 包的所有函数和他们的参数：

    lsf.str("package:pinyin")

    ## bookdown2py : function (folder = "py", remove_curly_bracket = TRUE, other_replace = NULL, 
    ##     dic = NA)  
    ## file.rename2py : function (folder = "py", dic = NA)  
    ## file2py : function (folder = "py", backup = TRUE, sep = " ", other_replace = NULL, 
    ##     encoding = "UTF-8", dic = NA)  
    ## load_dic : function (dic_file = NA, select = 1)  
    ## pinyin : function ()  
    ## py : function (char = "", sep = "_", other_replace = NULL, dic = pydic())  
    ## pydic : function (method = c("quanpin", "tone", "toneless"), multi = FALSE, 
    ##     only_first_letter = FALSE, dic = c("pinyin", "pinyin2"))

函数的用法总结在图 2 里。

img(‘pinyin-functions.png’)

在这些函数里, `py()` 是主函数。初学者可以通过这个函数来对 ‘pinyin’ 包有个初步印象。下面详细介绍这个函数的用法。

将单个汉字转成拼音
------------------

`py()` 函数最简单的用法是转换单个的汉字，例如：

    py('春')

    ##     春 
    ## "chūn"

> 练习 1：将你的姓的汉字转成拼音。

将多个汉字转成拼音
------------------

待转换的汉字可以是个长度大于 1 的向量。例如：

    py(c('你', '好', '坏'))

    ##     你     好     坏 
    ##   "nǐ"  "hāo" "huài"

也可以是个字符数大于 1 的字符串：

    py("你好坏")

    ##        你好坏 
    ## "nǐ_hāo_huài"

体会一下上面两个例子的差别。

如果要转换的汉字保存在表格里，`py()` 可以直接转换整列的汉字，就像这样：

    testd <- data.frame(stringsAsFactors=FALSE,
                        x1 = c('我', '一定', '是个', '天才'),
                        x2 = c('我', '确', '是个', '天才'))
    testd$x1py <- py(testd$x1)
    testd$x2py <- py(testd$x2)
    testd

    ##     x1   x2     x1py     x2py
    ## 1   我   我       wǒ       wǒ
    ## 2 一定   确  yī_dìnɡ      què
    ## 3 是个 是个  shì_ɡàn  shì_ɡàn
    ## 4 天才 天才 tiān_cái tiān_cái

> 练习 2：将你的全名转成拼音。