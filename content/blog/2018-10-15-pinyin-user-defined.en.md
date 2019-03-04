---
title: "[R pinyin: New Features] User customized dictionaries"
author: dapeng
date: "2018-10-15 14:34:03"
slug: pinyin-user-defined
tags: 
  - utopian-io
  - post
  - R
  - pinyin
banner: img/banners/logo-pinyin.png
---

The pinyin package intended to convert Chinese characters into pinyin. However, more demands were called by users. That was why the features of converting to four-corner codes and five-stroke codes (version 98) were added. After my previous update, the utopian moderator @justyy kindly [suggested](https://steemit.com/utopian-io/@justyy/re-dapeng-pinyin-wubi-20181012t201139924z) adding the Five-Stroke-86 as well. I totally agree, and I think there could be more.

<!--more-->


The pinyin package now has two new features:

- Supporting Five-stroke-86. 
- User can customize his/her own dictionary, so  that the pinyin package can convert Chinese characters (or other characters) according to the dictionary.

![pinyin2.jpg](https://cdn.steemitimages.com/DQmc656HK9LmfyXJUK8EnxKHJ3bAB9hTV3eEJaHGupkDM6b/pinyin2.jpg)

#### How did I implement them?

I modified the `pylib()` (renamed as `pydic()`) so as to be more flexible and open to different dictionaries. A Five-Stroke-86 dictionary was created. I also wrote a new function `load_dic()` to load the dictionaries. The main function `pinyin()` was renamed as `py()`, which can convert Chinese characters (or other characters) into the destined characters.

Each part of the functions are well documented. Other files were updated automatically by compilation. 

Link to relevant lines in the code on GitHub can be found mainly in my latest commit (click to see the details):

- [flexible for user-defined dictionaries](https://github.com/pzhaonet/pinyin/commit/5e11f1cbe90d5529eea6f3947fb80c7fe6177e81)
- [bugs fixed](https://github.com/pzhaonet/pinyin/commit/fab7581c4dad7cd278ee9328a14ba2ad7a3f3377)
- [Update readme.md](https://github.com/pzhaonet/pinyin/commit/773bfb9ec8d2142e43c5f0678e8aca586c7a2460)
- [remove unnecessary data](https://github.com/pzhaonet/pinyin/commit/69388fdf4ebe90e7cda794fcfdf82f827b06c493)
- [pass the CRAN check](https://github.com/pzhaonet/pinyin/commit/5657147f6cba87a45897902ce794ff22caf64bd5)

