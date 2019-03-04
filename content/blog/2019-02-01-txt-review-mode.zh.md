---
title: "纯文本编辑器的审阅模式"
author: dapeng
date: "2019-02-01"
slug: txt-review-mode
summary: "似乎没有完美的解决方案。"
tags: 
  - post
  - R
  - git
  - LaTeX
banner: img/banners/logo-openr.png
---

这里说的审阅模式，指的是像 Microsoft Office Word 里的 Review 模式，可以显示修订前后的不同。

<!--more-->

界面是这样的：

![](https://liminalpages.com/wp-content/uploads/2016/01/TrackedChangesExampleInsertDelete.jpg)

Word 有诸般不爽，我尽量不用，然而它的审阅模式却是很实用的功能。纯文本编辑器里，想显示两个纯文本的不同，我目前找到了三个方案：

1. total commander 的文件比较功能。
2. NotePad ++ 的文件比较插件。其他编辑器，如 sublime 和 vim 都有类似插件。
3. git 方案。

这几个方案自用是无妨，但是跟别人协作起来不大好，还得强迫别人装这装那，学这学那，人家一甩袖子不干了。而且，操作起来总是不如 Word 那样所见即所得用起来舒服（也可能是习惯使然）。office 要是添个纯文本编辑器就好了。

我们所有个哥们儿，装了一套 overleaf 系统给内部使用。 overleaf 有历史版本比较和 review 功能，虽然它是为 LaTeX 设计的，但变相用作文本协作编辑器也算是差强人意。

目前看起来，最容易的方式是用 RStudio，开启 git 功能，配合上我的 [rmd 包](http://www.pzhao.org/zh/post/rmd) 提供的各种外围服务，把 RStudio 打造成一个平易近人 markdown 编辑器。

RStudio 开启 git 功能的方法是：

- 安装 [git](https://git-scm.com/downloads) 或 [GitHub Desktop](https://desktop.github.com/)。
- RStudio 设置:
  - Tools ➞ Global Options ➞ Git/SVN
  - Tools ➞ Project Options ➞ Git/SVN

