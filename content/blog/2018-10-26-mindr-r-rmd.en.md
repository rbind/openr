---
title: "[R: New Features on mindr] Support LaTeX Equations. Conversion between .R scripts and .Rmd documents"
author: dapeng
date: "2018-10-26 11:25:54"
slug: mindr-r-rmd
tags: 
  - post
  - R
  - mindr
---

### New Features

The new version 1.1.7 brings more exciting features.

- Keep the LaTeX equations when converting markdown files into mindmaps, as a reply to [specter119's comment](https://github.com/pzhaonet/mindr/issues?q=is%3Aissue+author%3Aspecter119).

  I used some regular expressions to extract the LaTeX codes from the markdown files, and changed them into extended mindmap syntax supported by [Docear](http://www.docear.org/).

  Commit: [keep LaTeX equations; re-organize the codes](https://github.com/pzhaonet/mindr/commit/f7350e2b5a734d475a05059ed6efd242a2029a89)

![mindr2.png](https://cdn.steemitimages.com/DQmSLqPn4qEAtcWxMouvcJ4vdYfMKNsT7zHz5sQQwfbJok2/mindr2.png)

Figure 1. A mind map with LaTeX equations  converted by mindr from a markdown file 

- Convert .R scripts into R markdown (.Rmd) or markdown (.md) documents, and vice versa, so that users can convert .R scripts into mind maps by using mindr.

  I added two functions to convert the following elements in .R scripts into R markdown documents.

  - code (.R) --->  code block (.Rmd, .md)
  - comments beginning with `#` ---> text body (.Rmd, .md)
  - comments beginning with markdown headings ---> headings (.Rmd, .md)

  Commit: [new features: conversion between .R and .md/.Rmd](https://github.com/pzhaonet/mindr/commit/e7bfee3f258d84e17eec57e578639bebaa673ea2)

![mindr1.jpg](https://cdn.steemitimages.com/DQmeejaHnewHiFcMChGGuq72p3ZvzWqV3HLW5rRAuqJ9Qam/mindr1.jpg)

Figure 2. Conversion between a .R script and a .Rmd file


