---
title: '用 markdown 的逻辑写 R 脚本注释'
author: "赵鹏"
date: '2018-10-27'
slug: r-with-markdown
summary: "代码里的注释很重要，读者是未来的自己。好的注释不仅能把事儿说清楚，还可以写得波澜壮阔，跌宕起伏。"
tags:
  - post
  - R
  - markdown
  - mindr
categories: []
banner: img/banners/logo-mindr.png
---


## 九阳真经

跟很多业余程序员一样，我意识到给代码写注释的重要性时，已经很晚了。有多晚？差不多就是隔一段时间再打开自己写的旧代码时。我惊讶得下巴都快掉了：这是我亲手写的吗？怎么一点都看不懂？这要是有人打假说我是抄袭，那恐怕连我自己都举双手赞成。

代码里的注释很重要，读者是未来的自己。好的注释不仅能把事儿说清楚，还可以写得波澜壮阔，跌宕起伏。就像我在 《[学 R](https://xuer.pzhao.org)》一书里写的：

> 如果你乐意，那么完全可以在注释里偷偷写一部小说，就像《倚天屠龙记》里有人在《楞伽经》夹缝处写下《九阳真经》一样。
>
> --- 《学 R》第一章 “初见”

<!--more-->


然而，作为一名未经规范培训的 R 语言爱好者，我一直不太清楚注释里的说明文字怎么写才好。在网上搜吧，例如流传甚广的[来自Google的R语言编码风格指南](https://nanx.me/rstyle/)，对注释的建议寥寥几笔就说完了。看别人怎么写吧，但大家的写法五花八门，随心所欲。印象深刻的，就是有个同事会以 telnet 时代 BBS 签名档的风格来写注释。开始我也跟风，后来时间一久，觉得麻烦，便不在乎了，怎么写全看心情。

## R 脚本到思维导图

这两天，我想把 ggplot2 捡起来，就翻出了当初做的笔记。这是个 .R  脚本，其中包含了函数的示例代码和注释说明文字。就像上一篇吐槽说的那样，ggplot2 的函数和语法，——可能是上了岁数，年岁越大越难掌握新语言，——我总是记不住。这回，我想一劳永逸解决这个问题。方法我都想好了：做个思维导图，设置成电脑的桌面墙纸，天天看得见，反复洗脑。

挽起袖子正打算画这个思维导图，心念一动：前些天开发的 mindr，能把 markdown 文档转成思维导图，背后的逻辑很简单：就是从文本文件里提取 `#` 开头的行，按 `#` 的个数来确定层次，套进思维导图的 node 里就行了。那么，只要 .R 脚本的注释按 markdown 的章节标题风格来写，就能用 mindr 直接转成思维导图。

![](https://github.com/pzhaonet/mindr/raw/master/showcase/mindr_concept1.png)

于是，就稍微修改了一下笔记里的注释格式，然后一条 `mindr::md2mm()`指令，这图就华丽丽地亮相了。

[![ggplot2.png](https://cdn.steemitimages.com/DQmPgyzj2sd7gWLQNKC8wgmCZsZtev2o93qH4tW84a6Aeai/ggplot2.png)](https://cdn.steemitimages.com/DQmPgyzj2sd7gWLQNKC8wgmCZsZtev2o93qH4tW84a6Aeai/ggplot2.png)

## .R 变成 .Rmd 

这让我想起一个雪藏的心愿：如果能把 R 脚本（.R）一键转换成 R Markdown (.Rmd) 文档就好了。

不知别人是啥情况，对我来说，一个 .Rmd 文档，往往萌芽于一个 .R 脚本：最初是要完成一个工作而写了段代码，后来决定分享出去，就把脚本内容拷贝粘贴到一个 .Rmd 文件里，将注释修改成标题和正文。

然而，这样的麻烦在于，同一内容就出现了 .R  和 .Rmd 两个版本，不方便后期维护。

我试过反向操作，就是改为从 .Rmd 为源头，需要其中的代码时，就用 `knitr::purl()` 提取出来。但试过几次就放弃了：调试代码，还是在 .R 里面方便。`knitr::purl()` 为啥就没有个逆函数呢？(更新：`knitr::spin()`可以将 .R 转换成 .Rmd。感谢 yihui 的提示。)

这回，既然走到了 .R 与思维导图转换的这一步，我想要的功能呼之欲出。

经过一番奋战，mindr 新增一个 `r2md()` 函数，将 .R 脚本转换成 .Rmd 文件，背后的映射（捡起了 ggplot2 之后我就不由自主开始用这个词）规则是这样的：

| .R                             | .Rmd                                     |
| ------------------------------ | ---------------------------------------- |
| "`#` + 空格" 开头的注释行      | 保留不变，自动成为章节标题               |
| "`#` + 非空格字符"开头的注释行 | 去掉开头的`#`，成为正文文字              |
| 代码行                         | 前后添加一对连续的三个反引号，成为代码块 |

也就是说，按上表左栏的规则来写注释，以后就可以方便地转成 .Rmd文件了。例如，下面这个 .R 脚本：

```R
# Calculation --------
#This is a chapter about calculation.
## Assign x --------
#Assign x some values.
x <- 1:6
## Assign y --------
#Assign y some values.
y <- 11:16
# Plot --------
plot(x, y)
```

说明一下：有些行末尾加上了 `--------`，这样是为了在 RStudio 里显示大纲视图（其实四个 `-` 就够了，八个是为了更醒目）：

![outline.jpg](https://cdn.steemitimages.com/DQmaUZ5poerko6956f4j6FvEAmzo2GRdb231aQ8GxmpBKUD/outline.jpg)

用 `mindr::r2md()` 转换得到的 .Rmd 是这样的：

```markdown
# Calculation
This is a chapter about calculation.
## Assign x
Assign x some values.
​```{r}
x <- 1:6
​```
## Assign y
Assign y some values.
​```{r}
y <- 11:16
​```
# Plot
​```{r}
plot(x, y)
​```
```



很满意。唯一纠结的，是第二条规则，因为"`#` + 非空格字符"开头的话，不是很美观。可能 "`#'` + 一个空格"更好看一点。试一段时间再说吧。大不了让用户自定义。



![](https://github.com/pzhaonet/mindr/raw/master/showcase/mindr_concept2.png)

## .Rmd 变成 .R

一不做二不休，干脆把事情做绝，让 mindr 把上面那个同心圆画完。

前面说过，将 .Rmd 变成 .R，已经有现成的方案了，那就是 `knitr::purl(documentation)`。`documentation = 0` 时，只提取出代码行；`= 2` 时，把代码之外的文字也全部提取出来，每行前面添加个 "`#'` + 一个空格"作为注释行；`= 1` 时……好像跟 2 一样。

我以前一直这样用，但不是很中意：主要是因为代码块的标题后面添加若干 `-`后，在 RStudio 里以大纲视图的形式展示。例如，上文显示的 .Rmd 文件，用 purl() 得到的 .R 是这样的：

```r
#' # Calculation
#' This is a chapter about calculation.
#' ## Assign x
#' Assign x some values.
## ------------------------------------------------------------------------
x <- 1:6

#' ## Assign y
#' Assign y some values.
## ------------------------------------------------------------------------
y <- 11:16

#' # Plot
## ------------------------------------------------------------------------
plot(x, y)
```

由于 .Rmd 里的代码块都没有标题，所以长长的小横线加在了一个空注释行的末尾，而我希望作为大纲视图展示的是原来 .Rmd 文件里的章节标题。具体来说，映射应该是这样的：

| .Rmd                          | .R                                                |
| ----------------------------- | ------------------------------------------------- |
| 章节标题（"`#` + 空格" 开头） | 后面添加 ` --------`，在 RStudio 里以大纲视图展示 |
| 正文                          | 开头加个"`#`"，成为注释行                         |
| 代码块                        | 去掉前后的三个反引号，成为代码行                  |

一番动手，给 mindr 添加了个 `md2r()` 函数，把这功能实现了。

mindr 的同心圆闭合了。从此，曲谐，他们过上了幸福的生活。

（更新：上述方案并不完美。补充方案见《[用 markdown 的逻辑写 R 脚本注释（2）](http://www.pzhao.org/zh/post/r-with-markdown2/)》）

![](https://github.com/pzhaonet/mindr/raw/master/showcase/mindr_concept.png)

