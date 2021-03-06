---
title: '外行 R 包开发手记：pinyin'
author: 赵鹏
date: '2018-10-19'
slug: pinyin-one-year
summary: "这样一个爹不疼妈不爱的包，原以为就这样了此残生，没想到突然意外焕发了生机。"
tags:
  - bookdown
  - R
  - pinyin
categories: []
banner: img/banners/logo-pinyin.png
---

玩 bookdown 直接催生了两个包的诞生。上一篇说了  bookdownplus， 这回说说 pinyin。

时隔一年多，我再回头去看 pinyin 这个包，就跟回顾 bookdownplus 是类似的：这玩意儿也算个包？

<!--more-->


(1)

先说说 pinyin 包的来历。使用 bookdown 写书，bookdown 会以各章标题为名称，来生成对应的 html 文件。如果标题是英文，那 html 文件就跟标题相同，而标题一般是不会重复的，html 文件自然也不会重名；如果标题是中文，那 html 就生成一串谁也看不懂的字符，只要不重复就行。然而我发现了一个问题，就是如果标题是中英文混合，那么 bookdown 只提出其中的英文，来作为 html 文件的标题，这样出现不同章节重名的可能性非常大。

例如，如果某章的标题是“R 语言入门”，另一章标题是“R 语言进阶”，通过bookdown 生成的 html 文件，这两章都是 r.html。一发现重名，bookdown 就报错（后来新版 bookdown 解决了这个问题，不表）。

当然，手动在标题后面用花括号指定一下 html 的文件名就行了，但是我突然有了个主意：何不写个 R 包，自动把标题里的汉字转换成拼音呢？

一年多过去，回顾一下，这个想法真是蠢极了。因为，写完《学 R》一书，我就再也没有写过一本像样的中文书或中文文档，这个预想的功能一次也没用上。完全是屠龙之技。

不过当时还是很兴奋的。年轻嘛，就像钱锺书说的，“年轻的时候，我们容易把自己的创作冲动理解为创作才能。”捋袖子就干，pinyin 包很快就写好并发布到 CRAN 了。它不仅能把 markdown 文档标题的中文转换成拼音，还顺带着能把任一汉字字符串转换成拼音，还能把一个文件夹的所有中文文件名都批量重命名为拼音，这个工作太了不起了，太伟大了，直到放了一段时间，我再回头看，我的天，我引以为荣的这个所谓的包，本质上不就是个查找替换吗。

顿时意兴阑珊。

(2)

pinyin 包在 CRAN 的发布跟 bookdownplus 一样，也遇到了很多意想不到的周折，类似的就不重复说了。值得一提的是， pinyin 包因为自身的特殊性，遭遇了一些特殊的待遇。

比如说，CRAN 要求给出函数的示例。

我的示例是把几个中文字符转换成拼音的拉丁字母。

CRAN 说不行，示例里不能含有中文字符。

一个处理中文的函数，不让拿中文字符示例？于是我把示例删了。

CRAN 说不行，必须给示例。

我……我就在函数里添加了个参数，让它默认为 NA，然后函数内部判断它是不是 NA。如果是 NA，就打印一段文字：“The stupid fault belongs to CRAN.” 示例的时候用默认值。

这回 CRAN 通过了。

但是这对用户不友好啊。于是我就用中文写了一篇 vignette，方便中文用户看到中文示例。

这样度过了短暂的一段平静时光。突然有一天，CRAN 发信来，说这个 vignette 有这样那样的问题，要求 2018 年元旦之前必须整改，否则取缔。

这是个群发邮件，发给多个包的作者，我却没读懂。过了一段时间再读，仍然读不懂。有个同病的包作者还发信问我是怎么解决的，我回信说我没解决。

业余真是要命啊。

圣诞节我就度假去了，把这事儿抛到了九霄云外。一直到了 5 月，《学 R》一书出版，有读者发信问：照书上说的方法安装 pinyin 包，装不上去，CRAN 上没有。

我一看，CRAN 果不食言，把 pinyin 给下架了。

书里的字改不了，为了避免读者误解，我把 pinyin 包的 vignette 删掉，重新提交了一次。CRAN 的规则虽然很硬，但管理员还是很友好的，于是 pinyin 重新上架了。所以如果用 `beginr::plotpkg('pinyin')` 来回顾一下 pinyin 包的日下载量，就会发现今年上半年是空白，那就是取缔期。

(3)

这样一个爹不疼妈不爱的包，原以为就这样了此残生，没想到突然意外焕发了生机。

生机来自美国的一位华人用户。他在科研工作里遇到一点麻烦，需要将三十多万个中文姓名转换成拼音。此外，他还要比较很多汉字的字型。他发信给我，说 pinyin 包帮他解决了这个问题。而他将 pinyin 包的函数做了优化，转换效率提高了四倍以上，并且稍加修改，支持将汉字转换成四角号码和五笔代码。他一口气把新代码都发给了我。

几十亿人里，八竿子打不着的两个人，以这种方式取得了联系，这种感觉我很难去描述。我发明的屠龙之技，意外地被另一个世界的勇士真的拿去屠龙了，这种感觉也很难去形容。

我把他的代码稍作修改，加入了 pinyin 包，把这位热心用户列入了合作作者。

再后来，又有人说，pinyin 包转换的五笔字符是 98 版，能不能支持 86 版？

啥，五笔还有不同的版？

我强忍着好奇心没去深究，只是找了个 86 版的五笔字典，加入了 pinyin 包。并且，为了避免将来在这个问题上无休无止，我重新架构了一下 pinyin 包，允许用户想用什么字典就用什么字典，只需要预先载入一下即可。也就是说，用户指定个文本文件，里面是逗号分隔的两列，那么，pinyin 包就按这个对应关系，对汉字或其他单个字符进行转换。

本质上，就是个映射好的查找和替换。

我想，这回应该算是一劳永逸了吧。
