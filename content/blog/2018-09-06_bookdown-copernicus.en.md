---
title: A template for Copernicus academic journals
author: 赵鹏
date: '2018-09-06'
slug: bookdown-copernicus
categories: []
summary: "Write academic papers of Copernicus journals with R markdown syntax."
tags:
  - R
  - bookdown
  - bookdownplus
  - markdown
  - news
banner: img/banners/logo-bookdownplus.png

---

This is a submission to the [1st bookdown contest](https://blog.rstudio.com/2018/07/27/first-bookdown-contest/).

- Write academic papers of Copernicus journals with R markdown syntax.
- Support ~ 40 Copernicus journals.
- Support both the two-columned pdf version and the discussion version.
- Create multiple file formats, including .pdf, single .html, gitbook, .md, .epub, docx.

<!--more-->

## Introduction

[Copernicus Publications](https://www.copernicus.org) is a publisher of scientific literature which publishes around 40 peer-reviewed open access scientific journals and other publications on behalf of the European Geosciences Union (EGU). Many years ago, one of my manuscripts was submitted to the academic *Biogeosciences* (BG). I wrote it with LaTeX. BG is one of the top journals in my research area. I believe I will submit to BG again in the future and I would not use LaTeX again. Therefore I created the bookdown template for Copernicus.

The bookdown-copernicus template was firstly included in the bookdownplus package in 2017. It used to be named as 'article' and 'discussion'. For the 1st bookdown contest I merged them into one and improved the structure of the files for easier use.

## An Example with Its Repo

Repo: https://github.com/pzhaonet/bookdown-copernicus

Copernicus journal papers are open-access. A submitted manuscript, if accepted, is firstly published online as a discussion version, the layout of which is easy for computer monitors. Here is my example:

![](https://github.com/pzhaonet/bookdown-copernicus/raw/master/showcase/copernicus2_1.png)

![](https://github.com/pzhaonet/bookdown-copernicus/raw/master/showcase/copernicus2_2.png)

![](https://github.com/pzhaonet/bookdown-copernicus/raw/master/showcase/copernicus2_4.png)

![](https://github.com/pzhaonet/bookdown-copernicus/raw/master/showcase/copernicus2_5.png)

![](https://github.com/pzhaonet/bookdown-copernicus/raw/master/showcase/copernicus2_7.png)

After successful discussions, the manuscript is published in a two-column printed version:

![](https://github.com/pzhaonet/bookdown-copernicus/raw/master/showcase/copernicus_1.png)

![](https://github.com/pzhaonet/bookdown-copernicus/raw/master/showcase/copernicus_2.png)

![](https://github.com/pzhaonet/bookdown-copernicus/raw/master/showcase/copernicus_3.png)

Users can easily specify the layout in the yaml of the bookdown-copernicus template.

Users can view mdpi.docx, mdpi.epub, mdpi.html,  mdpi.pdf, and mdpi.tex as well.

## Technical details

Copernicus provides a [LaTeX template](https://publications.copernicus.org/for_authors/latex_instructions.html) which is free for using. I modified it as 'tex/template_article.tex', i.e. something was moved from the original LaTeX template to the yaml of 'index.Rmd'. Users could simply compare them and then get an idea how to convert a LaTeX template into a bookdown template.

Any suggestions are welcome. Just PR the repo!

