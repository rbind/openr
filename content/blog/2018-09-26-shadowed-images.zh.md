---
title: '给 Hugo 网站的插图添加阴影'
author: 赵鹏
date: '2018-09-26'
slug: shadowed-images
summary: "做了个 bookdownplus 的展示网站，想给所有插图添加个阴影。"
tags:
  - bookdownplus
  - markdown
  - tutorial
categories: []
banner: img/banners/logo-bookdownplus.png
---

最近一年多，有个东西一直困扰着我，就像半夜酣睡时飞来一只蚊子，时不时在耳朵边哼哼几声，很烦。挥手赶走它继续睡，过一会儿又过来哼哼。好几次我犹豫着要不要爬起来彻底消灭它，想着想着就又睡着了，于是就一直凑合。

这只蚊子就是我自己开发的 bookdownplus 包。

<!--more-->


关于自己是怎么被自己的包给坑住的，以后再慢慢说。这里只是说说一个小技术问题。

前两天，我做了个 bookdownplus 的[展示网站](https://bookdownplus.netlify.com)，用来秀手头现有的 bookdown 模板，尤其是生成的 pdf 文件截图。由于网页背景是白的，而 pdf 截图背景也是白的，所以两页 pdf 的截图放在网页里就直接连起来了：

![](https://github.com/pzhaonet/bookdownplus-web/raw/master/static/img/no-shaddow.png)

这哪有书的样子？于是，我想给每张图加个阴影，就像以前我做的那样：

![](https://github.com/pzhaonet/bookdownplus/raw/master/inst2/showcase/bookdownplus_thesis_classic.jpg)

这虽然好看，但这是用 powerpoint 一张一张做的，神烦（这是 bookdownplus 坑之一）。bookdownplus 以后的计划是接受别人贡献的模板。每有新模板，我都手动去做个图吗？

这时突然想起一个叫 css 的东西。话说这个东西就像鬼，我只听说过，从来没见过——也不是没见过，而是总视而不见。等于没见过。

我又感觉蚊子来哼哼了。这回索性坐起来研究了一下。

这个网站，用的是 [hugo-creative-portfolio-theme](https://github.com/kishaningithub/hugo-creative-portfolio-theme) 主题，blogdown 搭建。搭建好的文件夹里，有个"themes/hugo-creative-portfolio-theme/static/css" ，里面一大堆 .css 文件。

我就从网上搜了一句，写进 custom.css 里：

```css
.jf-image-shadow {
box-shadow: inset 2px 2px 5px black, 2px 2px 5px black;
}
```

然后，帖子里插图就不用 `![]()` markdown 语法了，而是改用 html：

```html
<img class = "jf-image-shadow" src="https://github.com/pzhaonet/bookdownplus/raw/master/inst2/classic/showcase/cover.png" />
```

于是，全体插图就都自带阴影了。

![](https://github.com/pzhaonet/bookdownplus-web/raw/master/static/img/shadowed.png)
