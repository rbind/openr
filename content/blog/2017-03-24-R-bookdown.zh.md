---
title: R bookdown 写学术论文
author: 赵鹏
date: '2017-03-24'
slug: r-bookdown
categories: []
tags:
  - R
  - markdown
  - bookdown
  - post
summary: "用 bookdown 写英文的科研期刊论文，配置起来是很简单的，只需在bookdown提供的[官方演示文档](https://github.com/rstudio/bookdown-demo)里做简单修改即可。"
banner: img/banners/logo-openr.png
---

*1*

最近，我使用 R 语言的 bookdown 扩展包接连做了三件事：先是整理出一本跟[ R 语言有关的书](http://dapengde.com/archives/19122)，然后把博客的帖子整理出一本[纯文本的中文书](http://dapengde.com/archives/19150)，这两天我又在用它来写一篇打算投稿的学术期刊论文。

<!--more-->

用 bookdown 写英文的科研期刊论文，配置起来是很简单的，只需在bookdown提供的[官方演示文档](https://github.com/rstudio/bookdown-demo)里做简单修改如下：

首先，index.Rmd 的文件头 yaml 部分，将 documentclass 设为 article，并关闭图表目录和文章目录即可：

    documentclass: article
    lof: no
    lot: no
    toc: no

然后，_output.yml 文件内容全部清空，然后添加指令生成 word\_document2 文档、 pdf\_document2 文档和 html\_document2 文档，参数为default即可。也就是说，\_output.yml 文件内容只需3行：

    bookdown::word_document2: default 
    bookdown::pdf_document2: default
    bookdown::html_document2: default

 就能生成足够美观的三种格式的文档了。

*2*

写论文期间发生了一件事，让我饱受刺激。

我的科研论文有个计算公式，昨天发现其中一个数值不小心敲错了。后续计算都是建立在这个计算的基础上，所以后续计算全错。虽然不影响结论，但严格来讲，论文里所有的数据都得改。

![enter image description here](https://blogs.helmholtz.de/hejus/wp-content/uploads/sites/15/2014/10/writinghardwork.jpg)

放在以前，这是让人崩溃的灾难。幸亏，这次我写论文用了 bookdown。

这篇研究论文是用 Rmd 格式写的，里面绝大部分数据不是手动敲进去的，而是调用了 R 代码，图表也是用 R 代码插入的，走的是“可重复性研究”的思路。现在，我只要把 R 代码里那个敲错的数据改过来，运行代码，后续计算就全部自动更新，而论文 Rmd 文件里调用代码的输出结果，会在导出的 pdf 或 word 文档也相应自动更新，节省了大量时间，还减少了敲数字或拷贝粘贴出错的可能，怎一个爽字了得！

在 bookdown 发布之前，其实 rmarkdown 也有这个功能，但因为公式、交叉引用、参考文献方面的欠缺， rmarkdown 对我来讲比较鸡肋，一直未能用在论文写作上。现在有了 bookdown ，可以甩开膀子使劲儿用。可以说， bookdown 把 rmarkdown 原有的价值做了更充分的挖掘。

写学术论文的过程比较煎熬，多年来我都不享受。而经过昨天的事件，我在写论文的过程里发现了很多快乐。我甚至有种变态心理，希望发现更多的计算错误，然后稍微一改，“叮！”论文全部自动更新。

老子陪你玩。好享受。

*3*

二娃德生前不久生病了，医生开了止咳糖浆。德生开始很拒绝，后来喜欢上了糖浆的味道。即使病好了，也经常要求喝止咳糖浆。

我问：“这是药，咳嗽才能喝。你咳嗽了吗？”

德生：“咳咳！咳咳！我咳嗽啦！”

学术论文写作使用 bookdown ，就是止咳药里添加的糖浆味道，让人不咳嗽的时候也想喝两盅，上瘾。

PS：今天在google.com以“bookdown”为关键词搜中文网页，我的博客已经出现在首页啦！