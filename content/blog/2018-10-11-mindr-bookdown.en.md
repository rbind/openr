---
title: "[R: New Features on mindr] Supports the new format  of  FreeMind. Displays mind maps directly. Supports bookdown projects."
author: 赵鹏
date: "2018-10-11 08:29:24"
slug: mindr-bookdown
tags: 
  - R
  - mindr
  - news
banner: img/banners/logo-mindr.png
---


In the recent months, I have received many kind feedbacks and helpful suggestions from mindr users. I did not improve or enhance mindr until the latest week. Now the new version 1.1.5 brings more exciting features.

<!--more-->


- Create mind maps out of a directory.

  I added a new function `dir2()` to create a mind map out of a directory in the user's computer.

  Commit: [compitable with both the old and new versions of mindmaps. new function](https://github.com/pzhaonet/mindr/commit/0109d784422ea125b730371e689c90b26657b6a2)

- Support the new format of FreeMind mind maps.

  The new format of FreeMind mind maps uses `/>`rather than `</node>` as the ending of a node. I added the compatibility for both the old and the new.

  Commit: [compitable with both the old and new versions of mindmaps](https://github.com/pzhaonet/mindr/commit/0109d784422ea125b730371e689c90b26657b6a2) 

- Display FreeMind mind maps directly, as a reply to [askhari139's comment](https://github.com/pzhaonet/mindr/issues/8#issue-299619384). 

  I added a new parameter to the function `markmap(input = c('.md', '.mm'))`. Now it can display not only markdown files, but also FreeMind mind maps in a markmap widge.

  commit: [display .mm files directly](https://github.com/pzhaonet/mindr/commit/b1e1f9159f4b75fa695f9791ff447d3493b51d06)

- Filter for file types were added, as a reply to [wuffi's comment](https://github.com/pzhaonet/mindr/issues/12#issue-338185363). Support hyperlinks in FreeMind mind maps, as a reply to [instantkaffee's comment](https://github.com/pzhaonet/mindr/issues/9#issue-314193635).

  I added a new paramter  `pattern` to the funcrtion `md2mm`, by which the uses can decide what files to import. By default, the '.md' and '.Rmd' files are imported.

  Commit: [file filter](https://github.com/pzhaonet/mindr/commit/550e9a0801451cb6077ade5893299e3e252532ce)

- Enhance the support for bookdown projects, according to [Yihui's suggestions](https://community.rstudio.com/t/bookdown-contest-submission-mindr-convert-a-bookdown-project-into-a-mind-map-and-vice-versa/15121/2?u=dapeng).

  I added a parameter 'bookdown_style' to the function `md2mm`. If the user choose the bookdown style, then mindr will put 'index.Rmd' before all the rest files, and lower the levels of the chapter headings if there is `# (Part)`, `# (APPENDIX)` or `# Reference`. The identification of chapter headings were improved as well.

  Commit: [enchance the support for bookdown project](https://github.com/pzhaonet/mindr/commit/8f8a639d2f3622610e930603f262b0678ae5ae12)

  A mind map produced from the bookdown project *[the Blogdown Book](https://bookdown.org/yihui/blogdown/)* is as follows.

  [![](https://discourse-cdn-sjc1.com/business4/uploads/tidyverse/original/2X/9/9165086d21772e9ae06d405cef10e26e709e0fc2.png)](https://discourse-cdn-sjc1.com/business4/uploads/tidyverse/original/2X/9/9165086d21772e9ae06d405cef10e26e709e0fc2.png)

- Some minor bugs were fixed, partly according to [jooyoungseo's comment](https://github.com/pzhaonet/mindr/issues/10#issue-317041556)

  Commits: 

  - ['invalid URLs' fixed](https://github.com/pzhaonet/mindr/commit/9ee25e627ab6127d146ae31be9a63fbf8909999d)
  - [users can specify the root of a mind map by markup()](https://github.com/pzhaonet/mindr/commit/1504accd874c48d8ad719a8be9347325604954b5)
