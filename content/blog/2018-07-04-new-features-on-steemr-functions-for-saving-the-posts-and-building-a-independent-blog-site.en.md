---
title: "[New Features on steemr] Functions for saving the posts and building an independent blog site!"
author: Peng Zhao
date: "2018-07-04 11:58:18"
slug: new-features-on-steemr-functions-for-saving-the-posts-and-building-a-independent-blog-site
tags: 
  - R
  - steemr
  - news
banner: img/banners/logo-steemr.png
---


- Do you want to backup your Steem posts in a local disk? The new function`bmd()` (build markdown files) saves the posts in the local path as markdown files easily. 

<!--more-->

The following example shows how to get all the posts by @dapeng and save the posts as markdown files in the local PC with `bmd()` :

```
tgidposts <- gidposts(id = 'dapeng', method = 'appbase_api')
bmd(post_df = tgidposts)
```

Then the user gets the markdown files '*.md', each of which is a Steem post. The use can view them via any text editor (recommended: [Typora](https://steemit.com/utopian-io/@dapeng/typora-the-best-cross-platform-markdown-editor-or-typora)).

If the parameter 'if_yaml' is TRUE, each md file will get a header with the title, posting time stamp, tags, original links, etc., which would be very useful for other R packages, such as R blogdown or R bookdown.

```
bmd(post_df = tgidposts, if_yaml = TRUE)
```

![2018-07-04-001.jpg](https://cdn.steemitimages.com/DQmQvaMnfE8X1jbjEHUoySKdytFxXEF33vymLzjSu2Z3hhj/2018-07-04-001.jpg)


> A screenshot of the markdown file created by steemr `bmd()` function.

- Do you want to build an independent blog site with your posts? The new function `bblog()` builds a Hugo blog from the given posts.

The following example shows how to build a blog site from all the Steem posts by @dapeng with `bblog()` :

```
bblog(author = 'dapeng', post_df = tgidposts, initial = TRUE)
```

The user will get a folder, containing the structure of a Hugo blog site. It can be viewed locally with the R blogdown package, or deployed by netlify.com. More details could be found in the [R blogdown book](https://bookdown.org/yihui/blogdown/).

![2018-07-04-002.jpg](https://cdn.steemitimages.com/DQmRFrbpq7HPcyU1R3ioVcn28DuriZj6ibSvD7rMi8uzrbh/2018-07-04-002.jpg)

> A screenshot of the blog site created by `bblog()` function.

Yes, you can visit this blog site even when steemit.com or busy.org is down!

Currently only simple blog template *xmin* is available. In the future more templates will come!  For example, here is a backup site of my own:

![2018-07-04-004.jpg](https://cdn.steemitimages.com/DQmewwQ1ZvCowWip3hYNpt8ju4jH721krsAaNWZbHPLpzbp/2018-07-04-004.jpg)

- Some minor literal changes in the documentation were performed and small bugs were fixed.

#### How did I implement them?

I added these new functions in  'R/build.r'.

I created a template for the Hugo blog in 'inst/template/blogdown_xmin.zip'.

I added a `clear_title()` function in 'R/internal.r' as an internal function to support the two functions mentioned above.

Links to relevant lines in the codes on GitHub can be found mainly in my latest commits (click to see the details):

- [new functions: bmd() bblog()](https://github.com/pzhaonet/steemr/commit/47b7477a5c76aa8cbb50fcd8d15be349423cbc8b)
- [updated readme.md](https://github.com/pzhaonet/steemr/commit/02bf59f5dbbead7ce345a2c7c625884f38a21039)
- [update the template](https://github.com/pzhaonet/steemr/commit/356d348a41e69e2c7f06b2699283eeed0184dd59)
