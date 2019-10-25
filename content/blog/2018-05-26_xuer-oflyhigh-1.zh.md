---
title: 'oflyhigh： Linux 下安装 R 扩展包'
author: oflyhigh
date: '2018-05-26'
slug: oflyhigh-1
tags:
  - R
  - xuer
banner: img/banners/logo-xuer.png
summary: "一个曼德勃罗集合（Mandelbrot set）的例子。"
---

本文经作者 @oflyhigh授权转载（[原文链接](https://steemit.com/r/@oflyhigh/5m2s1h-r)），略有改动。

---

### 运行脚本

昨天我摸索出来执行R脚本的命令为：

```
R --slave -f hello.R
```

今天发现原来有一个专门的指令做这个工作：

```
Rscript
```

比如对于上述命令，我们可以修改为：

```
Rscript hello.R
```

除此之外，我们还可以用`-e`来直接执行一些语句，比如：

```
Rscript -e "1+1"
Rscript -e 'print("Hello World");'
Rscript -e "print(\"Hello World\");"
Rscript -e "print(\"Hello World\");1+1;2+2"
```

### 安装软件包

在使用Python语言时，我们知道可以使用`pip`指令来安装所需的软件包，那么R语言环境下，我们如何安装呢？答案是在R环境的提示符下直接使用类似如下指令即可：

```
install.packages("example_package")
```

比如我想安装一个caTools的东西（我也不知道是啥），这样做就可以鸟：

```
install.packages("caTools")
```

注：我是在普通用户账户下执行的R，所以执行上述指令是会提示我：

> Would you like to use a personal library instead? (y/n) y

也就是说数据包被安装的本地，如果想安装到全局，估摸应该用`sudo R`来启动R环境（我瞎猜的，本地安装挺好，就不去测试了）

加载安装好的软件包，使用类似如下指令即可：

```
library(caTools)
```

### 见识一下

尽管"Hello World!"已经超级强大了，但是还是想见识一下更加强大的功能，在R语言的维基百科页面有一个曼德勃罗集合（Mandelbrot set）的例子，略作修改拿来运行一下，长长见识。

```
#install.packages("caTools")  # install external package
library(caTools)             # external package providing write.gif function
jet.colors <- colorRampPalette(c("#00007F", "blue", "#007FFF", "cyan", "#7FFF7F",
                                 "yellow", "#FF7F00", "red", "#7F0000"))
dx <- 400                    # define width
dy <- 400                    # define height
C  <- complex(real = rep(seq(-2.2, 1.0, length.out = dx), each = dy),
              imag = rep(seq(-1.2, 1.2, length.out = dy), dx))
C <- matrix(C, dy, dx)       # reshape as square matrix of complex numbers
Z <- 0                       # initialize Z to zero
X <- array(0, c(dy, dx, 20)) # initialize output 3D array
for (k in 1:20) {            # loop with 20 iterations
  Z <- Z^2 + C               # the central difference equation
  X[, , k] <- exp(-abs(Z))   # capture results
}
write.gif(X, "Mandelbrot.gif", col = jet.colors, delay = 25)
```

![Mandelbrot.gif](https://cdn.steemitimages.com/0x0/https://cdn.steemitimages.com/DQmddxperCLjNdqCzAdgFTyhg6YNz5chzNZ65kL7sfvoZ7N/Mandelbrot.gif)

虽然不知道是什么鬼，但是很漂亮，不是吗？