---
title: "[Task Request on beginr] Documentation for each function friendly to R beginners"
author: Peng Zhao
date: "2018-06-15 15:30:21"
slug: beginr-task-documentation
tags: 
  - R
  - beginr
banner: img/banners/logo-beginr.png
---


> The documentation level of R is already much higher than average for open source software and even than some commercial packages (esp. SPSS is notorious for its attitude of "You want to do one of these things. If you don't understand what the output means, click help and we'll pop up five lines of mumbo-jumbo that you're not going to understand either.")
>
>    -- Peter Dalgaard
>
> <U+200B>      R-help (April 2002)

<!--more-->


Although the R package beginr is published on [CRAN](https://cran.r-project.org/package=beginr), its documentation is insufficient, only because beginr was submitted to CRAN too soon and I had no time to improve the documentation. 

The documentation of a function in an R package could be displayed by running the `help()` function. For example, the documentation of the `errorbar()`function in beginr can be displayed when running:

```
library('beginr')
help(errorbar)
```

Then the user will see the following information:

```
Description

add error bars to a scatterplot.

Usage

errorbar(x, y, xupper = NULL, xlower = NULL, yupper = NULL, ylower = NULL, 
    col = "black", lty = 1)
Arguments

x numeric
y numeric
xupper	numeric
xlower	numeric
yupper	numeric
ylower	numeric
col	colors
lty	numeric
Value errorbars in a plot

Examples

x <- seq(0, 2 * pi, length.out = 100)
y <- sin(x)
plot(x, y, type = "l")
errorbar(x, y, yupper = 0.1, ylower = 0.1)
```

The Description, Usage and Argument are too brief. As beginr is developed for R beginners, a detailed documentation would help.

A desired example of the documentation for an R function can be found when running the following function:

```
help(sd)
```

A detailed documentation will appear as follows:

```
Standard Deviation

Description

This function computes the standard deviation of the values in x. If na.rm is TRUE then missing values are removed before computation proceeds.

Usage

sd(x, na.rm = FALSE)
Arguments

x	
a numeric vector or an R object which is coercible to one by as.double(x).
na.rm	
logical. Should missing values be removed?
Details

Like var this uses denominator n - 1.

The standard deviation of a zero-length vector (after removal of NAs if na.rm = TRUE) is not defined and gives an error. The standard deviation of a length-one vector is NA.

See Also

var for its square, and mad, the most robust alternative.

Examples

sd(1:2) ^ 2
```

The task is to write a friendly documentation for each function in beginr.

The suggested tool is RStudio. Open 'R/foo.R' (this file name is stupid and I will change it later) with a text editor (RStudio is recommended), and add the documentation in the header of each function. After the documentation is done, I will re-build the package, then the 'man/*.Rd' files will be updated automatically.


#### Components

Each function will have a detailed help information from the documentation.

Open 'R/foo.R'  with a text editor. Each function begins with a short description, followed by several lines beginning with `#'`, then the function body . For example, the `errorbar()` function begins at line 198, and looks like this:

```
#' add error bars to a scatterplot.
#'
#' @param x numeric
#' @param y numeric
#' @param xupper numeric
#' @param xlower numeric
#' @param yupper numeric
#' @param ylower numeric
#' @param col colors
#' @param lty numeric
#'
#' @return errorbars in a plot
#' @export
#' @examples
#' x <- seq(0, 2 * pi, length.out = 100)
#' y <- sin(x)
#' plot(x, y, type = 'l')
#' errorbar(x, y, yupper = 0.1, ylower = 0.1)
#'
errorbar <- function(x, y, ......
```

The first line 'add error bars to a scatterplot' is a short description about the function `errorbar()`. This description is sufficient. However, the lines beginning with `#' @param` are not sufficiently documented.  For instance, line  200:

```
#' @param x numeric
```

only mentions that x should be numeric. A desired documentation for this line should be written as:
 
```
#' @param x A numeric vector plotted as the coordinates of points. 
```

which is much better and more friendly to users.

I would suggest that this task had better be claimed by an R user, because most of the '@param' lines are self-explanatory to an R expert. He/she could run the function `example(function_name)` to test each function in beginr, and get to understand what these parameters are really are.

