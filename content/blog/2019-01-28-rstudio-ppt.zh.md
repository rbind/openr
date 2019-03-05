---
title: '往 ppt 里插入 500 张图片的小伎俩'
author: 赵鹏
date: '2019-01-28'
slug: rstudio-ppt
summary: "别说 500 张，5000 张也不在话下。"
tags:
  - markdown
  - R
  - tutorial
categories: []
banner: img/banners/logo-openr.png
---

今天要做个 ppt，内涵几十张照片，每页一张。
本来想手动，突然想起来，新版 RStudio 夹带了 新版 pandoc， 而 pandoc > 2.0.5， 可以用 markdown 做 ppt。

<!--more-->

方法是这样：


````
---
title: "title"
output: powerpoint_presentation
---

```{r, results='asis', echo = FALSE}
imgs <- dir('c:/image', full.names = T)
for(img in imgs) cat('##\n![](', img, ')\n\n')
```
````

xaringan 也一样。

````
```{r, echo=FALSE, results='asis'}
imgs <- dir('c:/image', full.names = T)
for (img in imgs) cat('![](', img, ')\n---\n')
```
````

别说几十张，就是 500张， 5000 张也不在话下。
