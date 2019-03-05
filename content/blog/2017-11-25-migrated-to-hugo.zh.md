---
title: '全面迁站：从 Wordpress 到 Hugo'
author: 赵鹏
date: '2017-11-25'
slug: migrated-to-hugo
summary: "从今天起，我的旧博客 dapengde.com 停止更新。旧博客的全部帖子已经搬到了 pzhao.org."
tags:
  - R
  - markdown
bibliography: [zhaor.bib]
categories: []
banner: img/banners/logo-openr.png
---

从今天起，我的旧博客 dapengde.com 停止更新。旧博客的全部帖子已经搬到了 [pzhao.org](http://www.pzhao.org)，欢迎收藏（ctrl + d）和[订阅](http://www.pzhao.org/zh/index.xml)。

<!--more-->

半年多以前，我用 R 语言的 blogdown 包搭建了新网站，与旧博客并存至今。[当时我就说](http://www.pzhao.org/archives/19323/)，我要等着益辉同学把blogdown 的使用说明书“迁站”一章写好，就照步骤把旧博客内容全搬过去。前些日子，[blogdown 书](https://bookdown.org/yihui/blogdown)终于出版了，从 wordpress 搬到 hugo 的迁站方法写得很详细。迁站的时机成熟了。

![](https://media.defense.gov/2012/Mar/19/2000168920/670/394/0/120319-F-JZ014-905.JPG)

然而，迁站的过程并不是很顺利。我照着书里推荐的步骤，试图用 [travis-exitwp](https://github.com/yihui/travis-exitwp) 将 wordpress 导出的 xml 文件转换成 Hugo 的markdown 文件。前面都还好，到了最后一步（第8步），我始终得不到右下角的绿色对勾，自然也得不到文件的下载链接。起初我以为是 xml 文件太大的缘故（10 M，五百多篇帖子），于是试着只导出少量帖子来生成 xml，从头操作，但是一觉睡醒还没得到下载链接。

于是改变策略，我给 wordpress 博客安装了插件 [wordpress-to-hugo-exporter](https://github.com/SchumacherFM/wordpress-to-hugo-exporter)，直接将帖子导出为 Hugo 的markdown 格式。除了文件名里的中文乱码外，我相当满意。于是将文件批量重命名，只保留日期。文件内容可以用益辉写的 [convert.R 代码](https://github.com/yihui/oldblog_xml/blob/master/convert.R)来清理。

不过，对我来说仍然不够，看来还得自己动手，才能丰衣足食。因为我用的是 hugo-academic 主题，网页上会显示每篇帖子的摘要，需要每篇帖子的 yaml 里设置一个 “summary” 条目。这个好办，用 R 语言把每篇帖子的第一段摘出来当作 summary 插进去就行了（R 代码附后）。

此外，我还想在每篇帖子末尾增添一个“原文链接”，链到旧博客，万一哪篇帖子格式没转好呢？这也好吧，markdown 的 yaml 里有个 url 条目，稍微改一下插到文末就行了（R 代码附后）。

这就是 hugo 静态网站的好处。有 R 语言在手，以后我就可以对这些 markdown 格式的帖子为所欲为了。而且，GitHub、简书、 steemit、Stackoverflow、统计之都等诸多网站都原生支持 markdown， 发的帖子只需稍微整理，就能发到博客上，颇有万佛朝宗的盛况。

Hugo-academic 主题我很满意，唯一不足的是缺个归档页面，一目了然展示全部帖子清单。看来得以后自己动手做一个。

旧博客 dapengde.com 虽然不更新了，但会仍然放在那里，发挥余热。前些天，还有朋友[来我四年前写的帖子后面留言](http://dapengde.com/archives/14752#comment-153909)呢。

增加 summary 和原文链接的代码：

```
for (i in dir('postold')){
  txt <- readLines(paste0('postold/', i), encoding = 'UTF-8')
  summ <- txt[grep('---', txt)[2]+1]
  summ <- gsub('"', '', summ)
  newline <- paste0('summary: "', summ, '"')
  linkzh <- '原文链接'
  newline2 <- paste0('\n[', linkzh, '](http://dapengde.com', substring(txt[grep('url', txt)[1]], 6), ')\n')
  txtnew <- c(txt[1:3], newline,  txt[4:length(txt)], newline2)
  writeLines(txtnew, paste0('postnew/', i), useBytes = TRUE)
}
```
