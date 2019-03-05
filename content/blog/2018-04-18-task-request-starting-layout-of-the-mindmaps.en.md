---
title: "[Task Request] Starting layout of the mindmaps"
author: Peng Zhao
date: "2018-04-18 16:00:39"
slug: task-request-starting-layout-of-the-mindmaps
tags: 
  - R
  - mindr
banner: img/banners/logo-mindr.png
---


As an R package, mindr is used to convert markdown files into mindmaps, and vice versa. It can also convert [tibble dataframes](https://steemit.com/utopian-io/@dapeng/new-features-mindr-supports-tibble-dataframes) into mindmaps. A brief introduction can be found in one of my previous posts: [mindr: an R package that creates a markdown post out of a mind map](https://steemit.com/utopian-io/@dapeng/mindr-an-r-package-that-creates-a-markdown-post-out-of-a-mind-map). Thanks to the support from utopian.io!

<!--more-->


mindr has a function `markmap`, which creates interactive web mindmaps with the JavaScript 'markmap' library. Here is an example:

```
folder <- system.file("examples/md", package = "mindr")
markmap(folder = folder, remove_curly_bracket = TRUE)
```

It converts the following markdown file, which is the skeleton of the bookdownplus textbook, into an interactive web mindmap:



```
# Basic {#basic}
## Markdown Syntax {#markdown_syntax}
### What is Markdown {#what_is_markdown}
### Basic syntax {#basic_syntax}
### Chapters {#chapters}
### Figures and tables {#figures_and_tables}
### References {#references}
### Theorems, lemma, definitions, etc. {#theorems__lemma__definitions__etc_}
### Export Word document {#export_word_document}
### Equations numbering {#equations_numbering}
## R, RStudio and bookdown {#r__rstudio_and_bookdown}
## LaTeX and Pandoc {#latex_and_pandoc}
## Workflow {#workflow}
# Simple {#simple}
# Lifestyle {#lifestyle}
## Journal {#journal}
## Poem book {#poem_book}
## Music {#music}
# Office {#office}
## Mail {#mail}
### Arguments for mail content
### Mail themes
## Calendar {#calendar}
# Academic {#academic}
## Articles {#articles}
## Thesis {#thesis}
## Poster {#poster}
## Chemistry {#chemistry}
# Advanced {#advanced}
## Chinese {#chinese}
## Mind Map {#mind_map}
## Create Your Own Templates {#customize}
# FAQ {#faq}
# Bibliography {-}
```

![mindmap.jpg](https://cdn.utopian.io/posts/76292519efd8b3c6f4ed6b285171b8474480mindmap.jpg)

By default the child nodes of this mindmap are expanded. A user of mindr left a message, asking how  to start with the child nodes collapsed, like this:



![](https://user-images.githubusercontent.com/22788747/31603595-3d2cb746-b293-11e7-9ebf-6150ab907fc1.JPG)



Currently, the user has to click the circle of the node to expand or collapse. 

The task is to add an option to the `markmap()` function, which allows users to decide the starting layout of the mindmap, such as the child nodes collapsed or expanded.

#### Components

Once the task will be completed, the returned results of the following functions will be changed:

```
mindr::markmap()
```

PS. The example showed above looks long. I used it just because it was taken from a real book and included in the current version of mindr. After I posted this article, @tdre suggested that a smaller, more concise markdown file and mind map illustration would have been enough to get the point across in this case and made for a faster read. Thanks to @tdre. I totally agree. Here is a smaller example.  A mini markdown file for testing is:

```
# New Projects
## What is the project about?
## Technology Stack
## Roadmap
## How to contribute?
# New Features
## What feature(s) did you add?
## How did you implement it/them?
# Bug Fixes
```

Save this file as `test.md` in a folder named `/md` in your work directory, and run:

```
markmap('md')
```

Then you get a mindmap in your viewer with all the child nodes expanded:

![mindr1.jpg](https://steemitimages.com/DQmbscT3pXUjFP3c5G1Pk11gmjsgd6NfnA18bn9qRsEVhTJ/mindr1.jpg)

The task is to add an option/parameter to the `markmap()` function, so that the mindmap can start with the given child  nodes collapse, such as:

![mindr2.jpg](https://steemitimages.com/DQmU8tcNLKHbdyrc8RYzwAEdfQVQtUYPboZt6JnyFCxnzuY/mindr2.jpg)

or

![mindr3.jpg](https://steemitimages.com/DQmSxs5fVTnfFpVxsB3pkPDENSjsJ6CC3AP4FWB8cxathCy/mindr3.jpg)

or

![mindr4.jpg](https://steemitimages.com/DQmX9gQznUh7ggfGD17NB1jqJkJFR42GixK2uwvDRVxFJgK/mindr4.jpg)
