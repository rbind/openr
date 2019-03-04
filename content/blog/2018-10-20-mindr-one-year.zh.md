---
title: '外行 R 包开发手记：mindr'
author: "赵鹏"
date: '2018-10-20'
slug: mindr-one-year
summary: "相反，在用户的要求下，mindr 在成长，越来越酷。"
tags:
  - post
  - mindr
  - R
categories: []
banner: img/banners/logo-mindr.png
---

在 CRAN 发布的几个包里， 我对 mindr 情有独钟。它像 pinyin 包一样，结构简单清晰。它得到的用户反馈不像 bookdownplus 包那样让我手足无措。相反，在跟用户的互动中，mindr 在成长，越来越酷。开发升级 mindr，是个很愉快的过程。

<!--more-->


(1)

mindr 最初的功能只有两个：一是把 markdown 文本里的标题提取出来，转成思维导图；二是反向操作，把思维导图里的节点按级别转换成 markdown。

想不起来当初是什么让我萌生了开发 mindr 的念头。最大的可能，是在写《学 R》的时候，我想给出版社呈现一个漂亮的大纲。

![](https://discourse-cdn-sjc1.com/business4/uploads/tidyverse/original/2X/9/9753b6328f86c3f09b7c0a5193cb9c5f51fe89ba.jpeg)

对，应该就是这样的，要不然还能是什么？记得我打开 Xmind，把书稿里的标题一个一个拷贝粘贴进来。这时老毛病又犯了：这个过程很机械枯燥，为什么不能自动完成呢？

于是搜索了一下现成的 R 语言包，没找到。我曾经怀疑是不是被我漏掉了，直到后来 mindr 的用户给我发信，说 mindr 是他发现的唯一一个做思维导图的包。这印证了我当时没找到确实是因为不存在。

既然不存在，那么能不能自己动手写一个？目标是思维导图，它的文件结构是什么样的？

我电脑里总共就装了两个思维导图软件，一个是 XMind，另一个就是 FreeMind。

XMind 生成的思维导图文件，用文本编辑器打开后，是一团乱麻。

而 FreeMind 的文件，打开后是逻辑清晰的可读代码。

更关键的是，XMind 可以导入 FreeMind 的文件。不仅 XMind，各大思维导图软件都支持 FreeMind。

这就好办了。几条正则表达式查找替换，核心代码只有几十行，mindr 就这样轻松诞生了。

(2)

刚一诞生，就出了件[怪事](http://www.pzhao.org/archives/19414/)：mindr 突然得到了很多星星 (star)。

原来，在一个名叫[黑客新闻](https://news.ycombinator.com/item?id=14682567)的地方，它被人围观，评头论足。

我不知道这是个什么论坛，但是我猜，围观的这些人可能都是专业程序员。所以我的感觉就像是一个小孩第一天上幼儿园。

有人上来就说，mindr 没用。思维导图应该用手拿笔画才有用。然后就有人说，现在很多人都用电脑软件画，谁还手绘呀……

有人说，有很多现成的库可以用，pandoc 加个什么 filter 就能转换了，为啥又用 R 写了一个？然后有人说，可能作者只会 R 吧……

更有人说，mindr 带给他的最大收获，是获悉了 bookdown 这个神器……

有意思。非常有意思。

![](https://discourse-cdn-sjc1.com/business4/uploads/tidyverse/original/2X/3/3b51829766beb6bb64aef4d4ca0e792572a06efd.png)

(3)

mindr 基本没遇见太大的 bug。因为它太简单了，而且用户很少，下载量不过几千。

要说最大的 bug，就是[益辉提出](https://community.rstudio.com/t/bookdown-contest-submission-mindr-convert-a-bookdown-project-into-a-mind-map-and-vice-versa/15121/2?u=dapeng)的，mindr 错把某处代码里以 “#” 开头的注释当成了章节标题。

这个我有点意外，因为mindr 从一开始就考虑到将三个反引号开头、三个反引号结束的代码块排除在外了，并且拿我自己的书试验过，都把代码块正确干掉了。莫非是我正则表达式用错了？

仔细一查，原来是 mindr 出错的这本书比较特殊，是有关编程的教程，里面出现了四个反引号开始和结束的代码块，里面还嵌着代码块，像个俄罗斯套娃，把没见过世面的 mindr 吓傻了。

等镇定下来，升级之后，这个问题基本解决。之所以说“基本”，是因为 mindr 仍然处理不了三个反引号开头，四个反引号结尾的代码块。mindr 认为他们没有成双成对。这种情况，不仅 mindr 处理不了，typora 也处理不了，sublime 的markdown 插件也处理不了。然而 pandoc 似乎完美处理了。

没啥好说的，业余就是业余。

![](https://discourse-cdn-sjc1.com/business4/uploads/tidyverse/original/2X/9/9165086d21772e9ae06d405cef10e26e709e0fc2.png)

(4)

用户给 mindr 提了很多建议。

[有人说](https://github.com/pzhaonet/mindr/issues/7)，能不能把 tibble 数据表转换成思维导图。我都不知道什么是 tibble 数据表，也不知道这样做的意义，本想敷衍了事，那人却详细地提出了他的需求，并给了贴心的示例，弄得我不好意思泼冷水。于是花了点工夫，可以从一个近似的数据生成他想要的图。

![](https://user-images.githubusercontent.com/4011804/36383199-b87064c4-158b-11e8-9ca4-cbbd8c1abddb.jpg)

[有人说](https://github.com/pzhaonet/mindr/issues/11)，能不能别借助第三方软件，而是直接在 R 的界面来展示 markdown 和 FreeMind 的思维导图？这个对我来说超纲了，但是搜了一下，有人开源了一个叫 markup 的包，我修改了一番，就拿来用了。

![](https://discourse-cdn-sjc1.com/business4/uploads/tidyverse/original/2X/9/9bb0d68237d8f7a71979cd1318a401c4ff31eff8.jpeg)

[还有人说](https://github.com/pzhaonet/mindr/issues/9)，能不能在 markdown 和 FreeMind 相互转换时，保留标题里的超级链接？还有人说，能不能用思维导图来展示电脑里文件夹和子文件夹的结构？[还有人](https://github.com/pzhaonet/mindr/issues/12)说，能不能添加一个过滤器，来指定把某个扩展名的文件参加转换？这些功能，虽然我觉得用到的人少之又少，但一听我就知道该如何下手，就当练手，一个一个都实现了。

现在只剩下[最后一个问题](https://github.com/pzhaonet/mindr/issues/5)了：能不能将 markdown 里的 LaTeX 公式在转换得到的思维导图里保留下来？

有这种想法的人真疯狂，不过我喜欢。

因为我已经找到了一个很绝妙的解决方案，简单到令人发指。

可惜这里写不下。
