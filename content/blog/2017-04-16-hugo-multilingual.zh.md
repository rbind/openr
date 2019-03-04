---
title: Hugo 网站 academic 主题的多语言界面
author: 赵鹏
date: '2017-04-16'
slug: hugo-multilingual
categories: []
tags: ["R", "blogdown", "post"]
summary: "双语界面是科研网站排在第一梯队的需求。我对Hugo的架构并不熟悉，原以为会很麻烦，结果弄一会儿就搞定了，原来这么简单。"
banner: img/banners/logo-openr.png
---

几年前我弄过[双语博客](http://dapengde.com/archives/15265)， 后来放弃了，因为 WordPress 的双语方案有些遗留问题让我不爽，另外我没有精力写英文博客。现在，新网站是个科研网站，博客可以只出现在中文版里，而英文版只放自己的学术情况就行了，不用像博客更新那么频繁。所以，双语界面几乎是排在第一梯队的需求。

我对Hugo的架构并不熟悉，原以为会很麻烦，结果弄一会儿就搞定了，原来这么简单。有些步骤在[主题的说明文档里](http://dapengde.com/blogdown_demo_academic/post/getting-started/)提到了，但不够全。完整的步骤是这样的(看起来长，是因为我啰嗦，其实很快就能设置完)：

<!--more-->

1、开启双语。这需要在`config.toml`里末尾找到：

```
[languages.en]
  languageCode = "en-us"
```

这说明网站现在是英文的。在后面添加中文，也就是：

```
[languages.en]
  languageCode = "en-us"

[languages.zh]
  languageCode = "zh-cn"
```

2、设置默认语言。这需要在`config.toml`里开头不远处找到：

```
# Default language to use (if you setup multilingual support)
defaultContentLanguage = "zh"
defaultContentLanguageInSubdir = true
```

原先是en，改成zh就可以让网站默认打开是中文。


3、菜单栏增加中文界面。菜单栏就是网页顶部那一排按钮。这需要在`config.toml`里找到菜单栏的设定：

```
[[menu.main]]
  name = "Home"
  url = "#about"
  weight = 1
```

上面是默认语言英语的设置。在下面添加中文设置，格式是

```
[[languages.zh.menu.main]]
  name = "主页"
  url = "#about"
  weight = 1
```

这样，就把`Home`按钮替换成了`主页`按钮。其他按钮类似。

4、其他地方的翻译。这需要把`\themes\hugo-academic\i18n\` 文件夹拷贝到根目录，然后删掉里边不需要的语言文件。我们只保留`en.yaml`和`zh.yaml`。用文本编辑器打开`zh.yaml`，把里边翻译不当的地方修改一下，比如 interests 翻译成了“兴趣爱好”，我改成了“研究领域”。

5、新增帖子的双语。这个最好办，每次在`content\`文件夹里新增文件时，如果要增加英文，就在文件扩展名前面加个`.en`就行了。例如，我在`content\talk\`下面新建了个`egu-2017.md`，里面是中文，会出现在中文界面上。那么我想让这个项目也在英文版出现，只需把`egu-2017.md`复制一份，命名为`egu-2017.en.md`，那么这个项目就会在英文界面出现了。打开`egu-2017.en.md`把里面的中文改成英文即可。

6、在菜单栏增加中英文界面切换的按钮。只需在`config.toml`里的菜单设置出增加：

```
[[menu.main]]
  name = "中文"
  url = "../zh"
  weight = 7
  
[[languages.zh.menu.main]]
  name = "EN"
  url = "../en"
  weight = 7
```

至此，双语界面全部搞定。