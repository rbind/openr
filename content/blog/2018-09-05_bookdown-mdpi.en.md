---
title: A template for MDPI academic journals
author: Peng Zhao
date: '2018-09-05'
slug: bookdown-mdpi
categories: []
summary: "Write academic papers of Copernicus journals with R markdown syntax."
tags:
  - bookdown
  - bookdownplus
  - R
banner: img/banners/logo-bookdownplus.png
---

This is a submission to the [1st bookdown contest](https://blog.rstudio.com/2018/07/27/first-bookdown-contest/).


- Write academic papers in the layout of MDPI journals with R markdown syntax.
- Support ~ 200 MDPI journals.
- Create multiple file formats, including .pdf, single .html, gitbook, .md, .epub, docx.

<!--more-->

## Introduction

Last year, [one of my papers](http://www.mdpi.com/2073-4433/8/6/111) was published on the academic journal *atmosphere*, which belongs to  the Multidisciplinary Digital Publishing Institute ([MDPI](http://www.mdpi.com/)). To be honest, this draft was written in Microsoft Word, although MDPI provides a nice LaTeX template. I could not hate LaTeX more at that moment. It had annoyed me enough.

Later, I met bookdown. I found that I could hardly resist the attraction of bookdown. A decision was made to create a bookdown template for MDPI journals on the basis of the LaTeX template: I would enjoy the production of LaTeX, while I would not have to struggle with the pain.

The bookdown-MDPI template was firstly included in the bookdownplus package in 2017. It had not been updated until the 1st Bookdown Contest. The new version of the bookdown-MDPI template is more tailored for markdown users rather than LaTeX users. It will be included in the R bookdownplus pakcage after the contest, if I win ;)

## An Example with Its Repo

Repo: https://github.com/pzhaonet/bookdown-mdpi

Screenshots of the pdf output are as follows. Users can view mdpi.docx, mdpi.epub, mdpi.html,  mdpi.pdf, and mdpi.tex.

![](https://github.com/pzhaonet/bookdown-mdpi/raw/master/showcase/mdpi_1.png)

![](https://github.com/pzhaonet/bookdown-mdpi/raw/master/showcase/mdpi_3.png)

![](https://github.com/pzhaonet/bookdown-mdpi/raw/master/showcase/mdpi_4.png)

## Technical details

MDPI provides a [LaTeX template](http://www.mdpi.com/authors/latex) which is free for using. I modified it as 'tex/template_article_mdpi.tex', i.e. something was moved from the original LaTeX template to the yaml of 'index.Rmd'. Users could simply compare them and then get an idea how to convert a LaTeX template into a bookdown template.

Any suggestions are welcome. Just PR the repo!

