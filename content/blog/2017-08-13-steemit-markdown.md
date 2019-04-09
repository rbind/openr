---
title: "中文段首加空格和增加段落间距 （steemit markdown）"
author: dapeng
date: "2017-08-13 09:05:33"
slug: steemit-markdown
categories: [cn]
tags: 
  - cn
  - cn-reader
  - markdown
  - steemit
---

原文链接: [steemit](https://steemit.com/cn/@dapeng/steemit-markdown), [cnsteem](https://cnsteem.com/cn/@dapeng/steemit-markdown), [chainbb](https://chainbb.com/cn/@dapeng/steemit-markdown), [busy](https://busy.org/cn/@dapeng/steemit-markdown), [markdown](https://raw.githubusercontent.com/pzhaonet/steem_mirror/master/content/post/steemit-markdown.md)

<br>

　　有朋友在 steemit 的 cn-reader 的微信群里问了一个 markdown 中文排版的问题：如何为中文段首增加空格，以及改变段落间的间距。这个简单：使用中文的全角空格。


![quanjiao.jpg](https://steemitimages.com/DQmQjSRg9PkM2gGmsqa7jm5wNxorgGgWQid3on1QwPeaoLa/quanjiao.jpg)

　　

　　一般的中文输入法都有上述设置界面。点一下弯月符号（或快捷键shift+空格）就变成满月，这就是全角。此时按空格键，就会输入一个汉字宽度的空白。所以，段首输入两个全角空白就行了。

　　不过，如果是紧跟在非普通文本（全文第一段，插图，代码等）后面，这种方法会失效，那么可以在全角空格前面加上个`<br>`就行了。

　　一般来说，在markdown编辑器里输入全角空格后再换行，就会多插入一行空白。下面我们用这种方法输入一行空白。

　　

　　

　　但连续几个空行 steemit 就不支持了。那么可以输入：

`<br>`

也同样是插入一个空行。输入几个`<br>`就插入几个空行。下面，我们插入两个空行。<br><br>

　　`<br>`其实是 html 语言的代码。“全角空格”是html界的魔法占位符。善用“全角空格”这个小魔法，就可以实现诸如　　对　　齐　　等其他功能。

　　要想使用复杂的格式，就需要复杂的命令或按钮来排版，容易偏离对内容的关注。而 steemit 使用的 markdown 语法，在内容和形式之间达到了最微妙的平衡，让你用最简单的指令，实现日常99%以上的排版需求。

　　不过，markdown 也尊重其他1%用户的特殊需求。原则上，markdown 支持 html，所以，要想对你的帖子的格式进行复杂排版，那么就学习 html 吧，少年！

　　中文段首空格原本是用来印刷时方便划分自然段的。在网络时代，自然段完全可以通过段落间距看得出来，所以段首空格丧失了原本的意义。不过，作为对纸质书和印刷时代的怀念，用一下段首空格，不失为一种情怀吧。
