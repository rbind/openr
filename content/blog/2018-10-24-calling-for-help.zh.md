---
title: '如何在 R 语言相关论坛求助'
author: "赵鹏"
date: '2018-10-24'
slug: how-to-call-for-help
summary: "求助！求助！十万火急！求助帖发布之后，是不是急着等人响应？可惜惊叹号没啥用。如果按以下格式发帖，效果会胜过十万个惊叹号。"
tags:
  - post
  - R
categories: []
banner: img/banners/logo-openr.png
---


求助！求助！十万火急！

在 R 语言相关论坛发布求助帖之后，是不是急着等人响应？可惜惊叹号没啥用。如果按以下格式发帖，效果会胜过十万个惊叹号。

<!--more-->


# 1. 模板

## 1.1 帖子标题

求助：在做啥的时候遇见的啥问题{用一句话概述遇到的问题}

## 1.2 正文

### 问题描述 

我在进行啥操作，目的是得到啥啥结果，但是遇到了如下问题：……

### 我的代码、示例数据和运行结果

贴出代码和数据，让别人拷贝粘贴过去就能直接重现这个问题，以便得到最快的帮助。推荐使用  reprex 包的`reprex()` 函数 和基础包的 `dput()` 函数。详见后面的示例。

### 我的系统环境

在 R 里运行 `sessionInfo()` 函数，将返回的信息贴出来。

-----

# 2. 发帖示例

[这](https://d.cosx.org/d/420238--)是一位朋友在统计之都论坛提的一个问题。原帖已经写得很好了，然而仍有改善的空间。让我们根据上面的模板，将这篇求助帖修改如下：

原标题：

> 如何将数字转化为时间格式

修改：

>  求助： 如何将 5, 930, 2235  这样格式的数字转换为 0:05, 9:30, 22:35  这样格式的时间？

从原标题看不出这究竟是个提问帖还是个经验总结帖。修改后，即使不用看正文，也一眼就看清具体问题是什么。

原正文：

> 大家好
>
> 我有一列从0-2355的数字，我希望把它们转换成0:00， 23:55这样的时间格式
>
> 尝试了 times <- format(otter$time, format = "%h-%m")
> 或是运算otter$time <- as.numeric(substr(otter[,3],1,2))*60 + as.numeric(substr(otter[3,],3,4))
>
> 都没有成功，请问有什么方法可以实现转换？
> 谢谢。

修改后：

### 问题描述 

我有一列格式为一到四位数的数字，如 0, 2355 等，我希望把它们转换成 0:00， 23:55 这样的时间格式，但没有成功。

### 我的代码、数据和运行结果

为了解决这个问题，我进行了如下测试，得到的都不是预期结果：

``` r
mydata <- c(840, 850, 900, 5, 10, 2355)
format(mydata, format = "%h-%m")
#> [1] " 840" " 850" " 900" "   5" "  10" "2355"
as.numeric(substr(mydata,1,2))*60 + as.numeric(substr(mydata,3,4))
#> [1] 5040 5100 5400   NA   NA 1435
```

### 我的系统环境

``` r
sessionInfo()
#> R version 3.5.1 (2018-07-02)
#> Platform: x86_64-w64-mingw32/x64 (64-bit)
#> Running under: Windows 7 x64 (build 7601) Service Pack 1
#> 
#> Matrix products: default
#> 
#> locale:
#> [1] LC_COLLATE=Chinese (Simplified)_People's Republic of China.936 
#> [2] LC_CTYPE=Chinese (Simplified)_People's Republic of China.936   
#> [3] LC_MONETARY=Chinese (Simplified)_People's Republic of China.936
#> [4] LC_NUMERIC=C                                                   
#> [5] LC_TIME=Chinese (Simplified)_People's Republic of China.936    
#> 
#> attached base packages:
#> [1] stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> loaded via a namespace (and not attached):
#>  [1] compiler_3.5.1    magrittr_1.5      htmltools_0.3.6  
#>  [4] tools_3.5.1       yaml_2.2.0        Rcpp_0.12.18     
#>  [7] stringi_1.2.4     rmarkdown_1.10.13 knitr_1.20       
#> [10] htmldeps_0.1.1    digest_0.6.17     stringr_1.3.1    
#> [13] evaluate_0.11
```

----

# 3.小技巧

下面的小技巧，告诉你如何把你的代码快捷优雅地贴出来。

仍然以上面的帖子为例，假如你出问题的代码是这样的：

``` r
mydata = read.csv("data.csv")
format(mydata, format = "%h-%m")
as.numeric(substr(mydata,1,2))*60 + as.numeric(substr(mydata,3,4))
```

要想别人重现你的故障，别人需要知道代码里用到的数据 mydata 是什么。上面这种情况，为了让别人没拿到 data.csv 文件也能正常运行你的后续代码，可以在上面的代码后面添加一条 `dput()`函数即可。

为了省事，系统环境报告函数也可以附在后面。所以，你要分享的代码应该改为：

``` r
mydata = read.csv("data.csv")
format(mydata, format = "%h-%m")
as.numeric(substr(mydata,1,2))*60 + as.numeric(substr(mydata,3,4))
dput(mydata)
sessionInfo()
```

然后，选中上面这些所有要分享的代码行，ctrl+c，再运行 reprex() 函数，这样就把代码和运行结果都存进了剪贴板，ctrl+v 贴到你的帖子里就行了。

珍爱生命，有效求助。节省别人的时间，才能快速得到帮助。