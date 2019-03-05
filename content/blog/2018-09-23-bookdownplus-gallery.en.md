---
title: "bookdownplus gallery: a web app for displaying and sharing bookdown templates"
author: Peng Zhao
date: "2018-09-23 16:34:39"
slug: bookdownplus-gallery
tags: 
tags: 
  - bookdown
  - bookdownplus
  - R
  - news
banner: img/banners/logo-bookdownplus.png
---



<p>Many years ago, I collected some LaTeX templates when learning LaTeX. However, my interest in LaTeX was gone after submitting my PhD dissertation. I should have deleted these templates if they had not been so small. They would never be useful in the future, I thought.</p>

<p>In 2017, I started writing the book <a href="https://xuer.pzhao.org"> <em>Learning R: R for Rookies</em> </a>. Unexpectedly, MS Word could not satisfy me with the typesetting. You know what I mean if you have experience (and pain) in writing a long book or dissertation with Word. Actually I suffered more, but I do not want to talk about it. I was sure that LaTeX could, but I would rather not use it.</p>

<p>Like a bolt out of the blue, I found <a href="https://CRAN.R-project.org/package=bookdown">bookdown</a>.</p>

<!--more-->


<p>From then on, I could not help spending time on this amazing tool. My book was completed with bookdown. My manuscripts, produced by bookdown, were submitted to academic journals and accepted. I wrote my papa-and-son diaries on bookdown.org. All the LaTeX templates were brought back to life: I packed them in an R package: <a href="http://www.pzhao.org/en/post/bookdownplus-released/">bookdownplus</a>.</p>

<p>Bookdownplus was supppsed to be a shortcut to bookdown. In the recently year, I have been doing my best to provide the beginners (and me) a friendly way to using bookdown. However, I struggled with two annoying problems. The first one is how the users (including me) can easily choose the right template. The second one is how the users (including me) can easily contribute their own templates to bookdownplus.</p>

<p><a href="https://bookdownplus.netlify.com">The web app for bookdownplus</a>  is intended to solve these problems. Users can search for elegant bookdown templates of interest, download the template package, and leave their comments. Furthermore, contributors' templates, if submitted to the <a href="https://github.com/pzhaonet/bookdownplus">bookdownplus repository</a>, can view their templates on this website as soon as possible.</p>

<p>In another word, this web app is a showcase of the R bookdownplus package, or a window of bookdown templates.</p>

<p><a href="https://bookdownplus.netlify.com"><img src="https://github.com/pzhaonet/bookdownplus-web/raw/master/static/img/webshot.png" alt="" /><br/></a></p>

<h3>What is bookdownplus?</h3>

<p><a href="https://CRAN.R-project.org/package=bookdownplus">bookdownplus</a> is an open-source software package that helps users write many kinds of books and articles, including academic journal articles, theses and dissertations, programming books (especially in R language), even guitar books, chemical equations, mails, calendars, and diaries. bookdownplus works on the basis of <a href="https://github.com/rstudio/bookdown">bookdown</a>.</p>

<p>You don't know which template to choose? <a href="https://bookdownplus.netlify.com">The web app for bookdownplus</a>  is a gallery of them, each with a title of the template name.</p>

<h3>Share your own templates</h3>

<p>If you are willing to share your bookdown templates, just upload them to the <a href="https://github.com/pzhaonet/bookdownplus">bookdownplus repo</a>. They will be displayed in the gallery automatically once accepted.</p>

<p>From the version 1.5, bookdownplus opens a widest-ever door to contributors. Here is how:</p>

<ol>
<li>Make sure that your template works successfully with bookdown.</li>
<li>Prepare a folder in your working directory by running <code>bookdownplus::share('your_template_name')</code> . Follow the instructions in each subfolder and create the required files.

<ul>
<li>(Mandatory) 'your_template_name/demo.zip' is the compressed file from your bookdown project folder.</li>
<li>(Optional) 'your_template_name/showcase/' contains the sample files (e.g. pdf, image files). An image file 'cover.png' is recommended, which will be used as the cover image in the gallery.</li>
<li>(Optional) You could write a 'your_template/readme.txt' (in markdown syntax), which will be displayed as the text in the gallery.</li>
</ul></li>
<li>Upload your template folder 'your_template_name/' in to '<a href="https://github.com/pzhaonet/bookdownplus/tree/master/upload">upload/</a>' of the bookdownplus repo.</li>
<li>Add the template information, including the template name, the contributor's name, and a brief introduction, into 'upload/-list.csv'.</li>
<li>Create a Pull Request to bookdownplus.</li>
</ol>

<p>Wait for the response, and your template will be available in the gallery.</p>

<p>Any suggestions? Please contact me!</p>
