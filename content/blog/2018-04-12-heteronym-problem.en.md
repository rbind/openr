---
title: "[Task Request] Heteronym problem"
author: Peng Zhao
date: "2018-04-12 08:56:48"
slug: heteronym-problem
tags: 
  - R
  - pinyin
banner: img/banners/logo-pinyin.png
---


Heteronym is a common lingual phenomenon in the most languages.  Wikepedia:

> A heteronym (also known as a heterophone) is a word that has a different pronunciation and meaning as another word but the same spelling. 

<!--more-->

For the Chinese language, the definition should be 'the same character' instead of 'the same spelling', as Chinese is not a spelling language. There are around 4000 frequently used Chinese characters, more than 1000 of which are heteronyms. The choice of the correct pronunciation of a character depends on the context.

Currently the [R pinyin package](https://steemit.com/utopian-io/@dapeng/pinyin-an-r-package-that-converts-chineses-characters-into-latin-letters-r) cannot handle heteronyms correctly. The Chinese language library which pinyin is using does not consider the context.

This is why [a bug was reported](https://steemit.com/utopian-io/@nydaily/4tbqsv-wrong-translation-of-heteronyms) by @nydaily as follows:

```
> pinyin::pinyin('我是一只小小鸟')
[1] "wǒ_shì_yī_zhī_xiǎo_xiǎo_diǎo"
> pinyin::pinyin('音乐')
[1] "yīn_lè"
> pinyin::pinyin('月亮')
[1] "rù_liánɡ"
```

The correct pronunciations of these characters should be:

-  '我是一只小小鸟' :  "wǒ shì yī zhī xiǎo xiǎo niǎo"
- '音乐': "yīn yuè"
- '月亮': “yuè liang”

pinyin was intended to avoid problems in non-Asian computers which might not support Chinese display. Technically I knew this bug and I thought that heteronym would not be a problem. Now it seems that there is a demand for pinyin to improve this feature. Thanks to @nydaily for the bug report, which makes much sense. I am sorry that this report could not be approved by utopian.io because there was no license file in the repo. Now I have added a license file.

The task is to return the correct pinyin for hereronyms when converting Chinese characters into pinyin.

#### Components

Once the task will be completed, the returned results of the following functions will be changed:

```
pinyin::bookdown2py()
pinyin::file.rename2py()
pinyin::file2py()
pinyin::pinyin()
```
