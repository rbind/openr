---
title: 'oflyhigh： Linux 下安装和使用 R'
author: oflyhigh
date: '2018-05-25'
slug: oflyhigh
tags:
  - R
  - xuer
banner: img/banners/logo-xuer.png
summary: "本书是以 Windows 操作系统来介绍 R 语言的。那么，Linux 下如何安装和使用呢？"
---

本文经作者 @oflyhigh 授权转载（[原文链接](https://steemit.com/r/@oflyhigh/r)），略有改动。

---

最近， @dapeng 巨著《学 R》上市销售，掀起了一股学 R 的热潮。比如美女 @dancingapple 也开始学 R，这不禁让人颇有些紧迫感，人长得美，还会 R，让别人咋办啊？不行，人丑更得多读书，我也要学 R。

可是我舍不得买书啊，那么就看 @dapeng 免费教程好了，可是一看，竟然都是在 Windows 下操作，可恶，Windows 我是用来发帖子聊 QQ 的，怎么能用来学 R，于是研究一下在 Linux 下咋玩吧。

# 安装

在Linux（ubuntu )下安装还是很方便的。

首先更新一下系统

```
sudo apt-get update
sudo apt-get upgrade
```

然后执行

```
sudo apt-get install r-base r-base-dev
```

就会安装R啦。当然了，这种方式安装的版本可能旧一点，不过我就是试试啦，不纠结这事，感兴趣的朋友可以试试其它安装方式。

# 开发环境

上述安装命令中的`r-base-dev`就是R的开发环境啦。

命令行中敲

```
R
```

回车，就会启动开发环境

![img](https://cdn.steemitimages.com/0x0/https://cdn.steemitimages.com/DQmeq8ZGnFiMMhid3AHhs67TJHEnGYuEnugyYpd1gngsPYm/image.png)

然后我们就可以在里边瞎搞了。

# Hello World

每学习一门语言，我做的第一件事就是写一个"Hello World!"出来，如果"Hello World!"运行起来，我就可以放心地和别人吹嘘我又掌握了一门高深的编程语言。

随便写两条打印语句试试

```
print("Hello World!")
print("Hello World!")
```

![img](https://cdn.steemitimages.com/0x0/https://cdn.steemitimages.com/DQmTm5yxXV8kktBeT5Z4VrNRt9NmuaMiguUYfs6hrfBaywd/image.png)

看来这些语言都差不多嘛。嗯，我可以放心的和别人吹嘘了我会R了。（在steemit上吹容易被识破，还是线下吹吧）

# 执行

有时候我们可能不想这样交互式的运行R，那么能否直接执行R的脚本呢？看一下R的帮助，试试能不能找出咋弄？

```
R --help
```

额，帮助信息有点长，不往这里贴了。不过还好找到一些貌似用来运行脚本的参数，来试试看。

vi编辑一个文件，写上`print("Hello World!");`保存为`hello.R`，然后执行下列指令：

```
R --slave -f hello.R
```

输出如下：
![img](https://cdn.steemitimages.com/0x0/https://cdn.steemitimages.com/DQme4XZvMfqMt9CGD5KGnmQ1vpDfGH3m6YyCTANw7tZ6xib/image.png)
✌，就是这个味，哦不对，就是这个结果。

# 继续

接下来该怎么办？

咳咳，我已经掌握了R，我不会告诉你我已经可以熟练使用神马诸如加减乘除乘方开方之类的运算操作，神马cat\paste字符串连接之类的我也可以信手拈来，甚至我还会用高深的sprintf用来格式化输出。

你问我还有啥不会的，这个问题还用问吗？~~还有啥是我不会的~~我不会的我岂能告诉你。

不过讲真，想好好学R，还是看 @dapeng 的教程，或者买 @dapeng 《学R》这本书吧，只有专业的、系统的教程，才是适合拿来好好学习的。