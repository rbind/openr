---
title: 《学 R》书中代码
author: Peng Zhao
date: '2017-06-14'
slug: xuer-codes
tags:
  - R
  - xuer
banner: img/banners/logo-xuer.png
---

这里列出《学 R》一书里的所有示例代码，以便读者使用。


<!--more-->

## 第一章 初见

```
co2
summary(co2)

3 * (2 + 2)
9 ^ 0.5 # 开平方
sqrt(9)  # 也是开平方

pi

options(digits = 22)  # 最大支持 22 位
pi

options(digits = 7) 
pi

exp(1)  # 计算 e
e = exp(1) 
e <- exp(1)  
exp(1) -> e
e

x <- round(e)^2
x

x <- c(61, 45, 55, 46, 56, 79, 86, 57, 56, 56, 57, 71)
x

x[4]

y <- co2 # 转存
y[10] # 看看第十个数据

x + 100

plot(y)  # 作图

(x[1] + x[2] + x[3] + x[4] + x[5] + x[6] + x[7] + x[8] + 
   x[9] + x[10] + x[11] + x[12]) / 12  # 计算平均值
sum(x) / length(x)
mean(x)
summary(x)
```

## 第二章 数据

```
dir.create('c:/r4r')
write.csv(as.data.frame(t(matrix(
  co2, 12, dimnames = list(
    month.abb, unique(floor(time(co2))))))),
   file = 'c:/r4r/co2.csv')

mydata1 <- read.table(file = "clipboard", header = TRUE)
mydata1

myfile1 <- file.choose()

myfile1 <- "c:/r4r/co2.csv"
myfile1
myfile2 <- "c:/r4r/co2.csv"
myfile2

file.show(myfile2) # 查看文件

mydata2 <- read.table(file = myfile2, 
                      header = TRUE, sep = ",")
mydata2

mydata2 <- read.csv(file = myfile2)

mydata2 <- read.csv(file = "c:/r4r/co2.csv")

plot(mydata2)

summary(mydata2)

mydata2[37, 10]

mydata2[c(2, 4, 6, 8, 10, 12, 14, 16, 18, 20,
          22, 24, 26, 28, 30, 32, 34, 36, 38), 10]

mydata2[seq(from = 2, to = 39, by = 2), 10]

mydata2[2:39, 10]

mydata2[, 10]  # 第10列全部。

mydata2[37, ]  # 第37行全部。

mydata2[, 'Sep']

mydata2$Sep

names(mydata2) # 或 colnames(mydata2)
names(mydata2)[1] <- 'year'
names(mydata2)

rownames(mydata2)
rownames(mydata2) <- mydata2$year
rownames(mydata2)

mydata2['1995', 'Sep']

sum(mydata2['1995', 2:13]) / 12

sum(mydata2['1996', 2:13]) / 12 - 
  sum(mydata2['1995', 2:13]) / 12

mydata2['1996', ] - mydata2['1995', ]

colMeans(mydata2[, 2:13]) # 排除掉第一列后，对整列求平均

mydata2$mean <- rowMeans(mydata2[, 2:13])

mydata2$median <- apply(X = mydata2[, 2:13], 
                        FUN = median, MARGIN = 1)

diff(mydata2$Sep)
```

## 第三章 作图

```
mydata2 <- as.data.frame(t(matrix(
  co2, 12, 
  dimnames = list(month.abb, unique(floor(time(co2)))))))  

mydata2$year <- as.numeric(rownames(mydata2))

plot(mydata2$Sep)

example(plot)

plot(x = mydata2$year, y = mydata2$Sep)

plot(mydata2)

pairs(mydata2)

demo(graphics)

plot(x = mydata2$year, y = mydata2$Sep, 
     xlab = "Year", ylab = "CO2 in Sep", 
     ylim = c(300, 400), type = "l")
	 
mydata2 <- read.table(file = myfile2,
                      header = TRUE, sep = ",")

plot(x = mydata2$year, y = mydata2$Sep, type = "p")

plot(x = mydata2$year, y = mydata2$Sep, type = "p", pch = 20)

plot(x = mydata2$year, y = mydata2$Sep, 
     type = "p", pch = 'z')
	 
plot(x = mydata2$year, y = mydata2$Sep, type = "l", lty = 2)

plot(x = mydata2$year, y = mydata2$Sep, type = "l", lty = 2, 
     col = 'blue')

colors()

colors()[26]

plot(x = mydata2$year, y = mydata2$Sep, type = "p", pch = 20,
     col = colors()[27:(27 + 39 - 1)], cex = 3)
	 
demo(colors)
demo()
demo(persp)

rainbow(n = 39)
plot(x = mydata2$year, y = mydata2$Sep, type = "p", pch = 20,
     col = rainbow(n = 39), cex = 3)
	 
myco2 <- unlist(mydata2[, 1:12])
myco2 <- round(myco2)
myyear <- rep(mydata2$year, 12)
mymonth <- rep(1:12, each = nrow(mydata2))
n <- diff(range(myco2)) # 彩虹分割的颜色数量
mycolor <- rainbow(n)[myco2 - min(myco2) + 1]
plot(x = mymonth, y = myyear, 
     col = mycolor, cex = 10, pch = 15)
	 
image(t(as.matrix(mydata2[1:12])), col = rainbow(n))

plot(x = mydata2$year, y = mydata2$Sep)
abline(h = 350)
abline(h = 360, v = 1980, col = 'red')
abline(h = seq(from = 320, to = 340, by = 5), 
       v = seq(from = 1970, to = 1990, by = 5), col = 'grey')
abline(a = -2240, b = 1.3)
legend(x = 1970, y = 350, legend = 'Sep', pch = 1)
legend("topleft", legend = 'Sep', pch = 1)

plot(x = 1:12, y = mydata2['1959', 1:12], 
     xlab = 'Month', ylab = expression(CO[2]),
     ylim = c(310, 370), 
     type = "l", lty = 2, col = 'blue')
lines(x = 1:12, y = mydata2['1997', 1:12], col = 'red')
points(x = 1:12, y = mydata2['1997', 1:12], col = 'red', type = 'l')

plot(x = 1:12, y = mydata2['1959', 1:12], 
     xlab = 'Month', ylab = '1959',
     type = "l", lty = 2, col = 'blue')
par(new = TRUE)
plot(x = 1:12, y = mydata2['1997', 1:12], ylab = '1997', 
     type = "l", lty = 1, col = 'red')

# 1. 告诉R在右侧为副坐标轴留出空间。
par(mar = c(5,4,4,4))
# 2. 画第一张图。
plot(x = 1:12, y = mydata2['1959', 1:12], 
     xlab = 'Month', ylab = '1959',
     type = "l", lty = 2, col = 'blue')
# 3. 告诉R，下一张图跟第一张图叠加。
par(new = TRUE)
# 4. 画第二张图，但暂时不画坐标轴，也不标标签。
plot(x = 1:12, y = mydata2['1997', 1:12], 
     type = "l", lty = 1, col = 'red', axes = FALSE, 
     ylab = '', xlab = '')
# 5. 在右侧画出副坐标轴。
axis(side = 4, col = 'red')
# 6. 为副坐标轴添加名称。
mtext(side = 4, text = '1997', line = 3, col = 'red')

par(mfrow = c(1, 2))
plot(x = 1:12, y = mydata2['1959', 1:12],
     xlab = 'Month', ylab = '1959',
     type = "l", lty = 2, col = 'blue')
plot(x = 1:12, y = mydata2['1997', 1:12],
     xlab = 'Month', ylab = '1997', 
     type = "l", lty = 1, col = 'red')

# 打开一张宽度为8，高度为4的白纸:
pdf('c:/r4r/fig2_13.pdf', width = 8, height = 4)
# 在白纸上画图:
plot(x = mydata2$year, y = mydata2$Jan)
# 画完了，把纸张收起来:
dev.off()

install.packages(c('ggplot2', 'lattice', 'plotrix'))

library(ggplot2)
example(qplot)

library(lattice)
demo(lattice)

library(plotrix)
demo(plotrix)

mydatasub <- t(mydata2[as.character(
  seq(1960, by = 5, length.out = 8)), 1:12])
x <- rep(1:12, 8)
y <- as.vector(mydatasub)
group <- rep(colnames(mydatasub), each = 12)
library(lattice)
xyplot(y ~ x|group, type = c('p', 'l'), 
       xlab = 'Month', ylab = expression(CO[2]))

library(ggplot2)
qplot(x, y, col = group, geom = c("point", "line"), 
      xlab = 'Month', ylab = expression(CO[2]))

vignette('ggplot2-specs')
vignette(all = TRUE)
	 
```

## 第四章 拟合

```
wp <- as.data.frame(WorldPhones)
wp$year <- as.numeric(rownames(wp))
m <- lm(wp$Asia ~ wp$Europe) 

m0 <- lm(wp$Asia ~ wp$Europe + 0) 

m  # 查看模型，显示斜率和截距。
msum <- summary(m)
msum  # 模型的详细总结报告。

msum$r.squared
msum$coefficients

example(lm)

par(mfrow = c(2, 2), mar = c(4, 4.2, 2, 1)) 
plot(m)

plot(x = wp$Europe, y = wp$Asia, pch = 19)
abline(m, col = "blue")
legend("bottomright", pch = c(19, NA), lty = c(NA, 1),
       legend = c("Data", "Linear fit"),
       col = c("black", "blue"), bty = 'n')
	   
text(x = 23000, y = 8500, labels = '(a)', col = 'red')

eqlm1 <- 'y = 0.2915x + 3783'
text(x = 23000, y = 7000, labels = eqlm1, adj = 0)

eqlm2 <- expression(y == 0.2915 * x + 3783)
text(x = 23000, y = 6000, labels = eqlm2, adj = 0)

eqlm3 <- expression(italic(y) == 0.2915 * italic(x) + 3783)
text(x = 23000, y = 5000, labels = eqlm3, adj = 0)

eqr2 <- expression(italic(R) ^ 2 == 0.9752)
text(x = 23000, y = 4000, labels = eqr2, adj = 0)

txt1 <- expression(sqrt(x))
legend('topright', legend = txt1)
legend('right', legend = txt1, lty = 1, col = 'blue', 
       bty = 'n')
	   
txt2 <- expression(integral(f(x) * dx, a, b))
legend('topleft', legend = txt2, col = 'blue', bty = 'n')

set.seed(123)
x <- seq(0, 50, 1)
y <- runif(1, 5, 15) * exp(-runif(1, 0.01, 0.05) * x) + 
  rnorm(51, 0, 0.5)
  
plot(x,y)

a_start <- 8
b_start <- - log(1/a_start) / 50
m <- nls(y ~ a * exp(-b * x), 
         start = list(a = a_start, b = b_start))
m

cor(y,predict(m))

summary(m)

example(lm)
demo(plotmath)
```

## 第五章 循环

```
mydata2 <- as.data.frame(t(matrix(co2, 12,
    dimnames = list(month.abb, unique(floor(time(co2)))))))
mydata2$year <- as.numeric(rownames(mydata2))
x <- mydata2$year
y <- mydata2$Sep
par(mfrow = c(3,3), cex = 1.2, mar = c(3, 2, 0.5, 1))
plot(x = x, y = y, type = 'p')
legend('topleft', legend = 'p', cex = 0.8,
       bty = "n", text.col = 'blue')
plot(x = x, y = y, type = 'l')
legend('topleft', legend = 'l', cex = 0.8,
       bty = "n", text.col = 'blue')
plot(x = x, y = y, type = 'b')
legend('topleft', legend = 'b', cex = 0.8,
       bty = "n", text.col = 'blue')
plot(x = x, y = y, type = 'c')
legend('topleft', legend = 'c', cex = 0.8,
       bty = "n", text.col = 'blue')
plot(x = x, y = y, type = 'o')
legend('topleft', legend = 'o', cex = 0.8,
       bty = "n", text.col = 'blue')
plot(x = x, y = y, type = 'h')
legend('topleft', legend = 'h', cex = 0.8,
       bty = "n", text.col = 'blue')
plot(x = x, y = y, type = 's')
legend('topleft', legend = 's', cex = 0.8,
       bty = "n", text.col = 'blue')
plot(x = x, y = y, type = 'S')
legend('topleft', legend = 'S', cex = 0.8,
       bty = "n", text.col = 'blue')
plot(x = x, y = y, type = 'n')
legend('topleft', legend = 'n', cex = 0.8,
       bty = "n", text.col = 'blue')
       
par(mfrow = c(3, 3), cex = 1.2, mar = c(3, 2, 0.5, 1))
for(i in c('p', 'l', 'b', 'c', 'o', 'h', 's', 'S', 'n')) {
  plot(x = mydata2$year, y = mydata2$Sep, type = i)
  legend('topleft', legend = i, cex = 0.8,
         bty = 'n', text.col = 'blue')
}


for(i in 1:20) print(i)

r <- 0.011
N1 <- 66.8
N2 <- N1 + r * N1
N3 <- N2 + r * N2
# ...... 如此写99行，就可以写到 N100。
N100 <- N99 + r * N99

r <- 0.011
N <- numeric(100)
N[1] <- 66.8
N[2] <- N[1] + r * N[1]
N[3] <- N[2] + r * N[2]
# ...... 如此写99行，一直写到 N[100]。
N[100] <- N[99] + r * N[99]

r <- 0.011
N <- numeric(100)
N[1] <- 66.8
for(t in 1:99) N[t + 1] <- N[t] + r * N[t] 

Y <- seq(2008, length.out = 100)
plot(Y, N)

abline(h = 100)
locator(1)

for(i in 1:360) {
    plot(1, ann = F, type = "n", axes = F)
    text(1, 1, "Ninja, go!", srt = i, col =
        rainbow(360)[i], cex = 7 * i/360)

}

example(image)

install.packages('simecol')
require(simecol)
# 40 * 40的棋盘:
m <- matrix(0, 40, 40)
# 玩家放置细胞的初始条件。0 表示该位置没有细胞，1 表示有细胞：
m[5:35, 19:21] <- 1
# 白色表示没有细胞，绿色有细胞：
image(m, col = c("white", "darkgreen"), axes = FALSE)
for(i in 1:200) {
  nn <- eightneighbours(m)
  m.old <- m
  # 当周围有三个细胞时该位置产生细胞：
  m[m.old == 0 & nn == 3] <- 1
  # 当周围细胞少于 2 个（太孤单）或大于 3 个（太拥挤）时，
  # 该位置细胞死亡。
  m[m.old == 1 & (nn < 2 | nn > 3)] <- 0
  image(m, col = c("white", "darkgreen"), axes = FALSE)
  Sys.sleep(0.1)
}

png(paste("c:/R/data/conway_",
          formatC(i, width = 2, flag = "0"), ".png",
          sep = ""),
    width = 300, height = 300)
image(m, col=c("white", "darkgreen"), axes = FALSE)
dev.off()

install.packages('rgl')
require(rgl)
example(movie3d)

x <- c(61, 45, 55, 46, 56, 79, 86, 57, 56, 56, 57, 71)
x + 100
for(i in 1:12) print(x[i] + 100)

wp <- as.data.frame(WorldPhones) # 转化为数据框类型
wp$year <- as.numeric(rownames(wp)) # 将行名称转化为数值类型
mydata3 <- data.frame( # 生成一个新数据框
  nphone = unlist(wp[, 1:7]), year = rep(wp$year, 7),
  conti = rep(names(wp)[1:7], each = nrow(wp)))
  
summary(mydata3)

str(mydata3)

mydata3$year <- as.factor(mydata3$year)
str(mydata3)

nlevels(mydata3$year)
levels(mydata3$year)

nlevels(mydata3$conti)
levels(mydata3$conti)


for(i in levels(mydata3$year)) {
  print(sum(mydata3$nphone[mydata3$year == i]))
}

tapply(mydata3$nphone, mydata3$year, sum)

mydata2 <- read.csv(file = "c:/r4r/co2.csv")
smr1 <- summary(mydata2)
smr1
smr1[6, 2] - smr1[1, 2]

smr2 <- lapply(mydata2, summary)
smr2[[2]][6] - smr2[[2]][1]

smr3 <- sapply(mydata2, summary)
smr3[6, 2] - smr3[1, 2]

plot(x = mydata3$year, y = mydata3$nphone)
boxplot(mydata3$nphone ~ mydata3$year)

N <- numeric(100)
N[1] <- 66.8
r <- 0.011
for(t in 1:3)
{
  N[t+1] <- N[t] + r * N[t]
  winDialog(type = c("ok"),
            message = paste('population in', t + 2007,
                            'will be', N[t + 1])) #信息提示框
}

n <- winDialogString(
  message = "which year's population would you like to see",
  default = '2050')
winDialog(type = c("ok"), message = paste(
  'population in', n, 'will be', N[as.numeric(n) - 2007]))

winDialog(type = c("ok"), message = paste(
  'population in', winDialogString(
    message = "which year's population would you like to see",
    default = '2050'), 'will be', N[as.numeric(n) - 2007]))
```

## 第六章 分支

```

3 > 2  # 3比2大？是真（true）的。
1 > 2  # 1比2大？是假（false）的。
!(1 > 2)  # 1不比2大？呃......
3 > 2 & 1 > 2  # 3比2大，并且1比2大？假的。
3 > 2 | 1 > 2  # 3比2大，或者1比2大吗？真的。
3 > 2 & !(1 > 2)  # 3比2大，并且1不比2大？好像是真的吧...

x <- 1:3
x == 2

x == 2 | x == 3

y <- c(4, 1, 2)
x > y

x > y & y > 1

TRUE * FALSE
TRUE + TRUE

sum(x > y)

x %in% y
x[x %in% y]
which(x %in% y)
Y[N > 100][1]

x <- 60
if(x < 75) print("x is less than 75")  

if(x < 75) {
	print("x is less than 75")
	y <- x + 10
	print(y)
	}
	
x <- 60
if(x < 75) {
    print("x is less than 75")
} else {
    print("x is larger than 75")
}  # 如果()，那么{}，否则{}。

x <- 60
if(x < 75) {
    print("small")
} else if(x > 90){
    print("large")
} else {
	print("good")
}

ifelse(x < 75, "small", ifelse(x > 90, "large", "good"))


N <- numeric(100)
N[1] <- 66.8
for(t in 1:99) N[t + 1] <- N[t] + r * N[t]
Y <- seq(2008, length.out = 100)
plot(x = Y + 2007, y = N, xlab = "Year", ylab = "Population", 
     cex = ifelse(N >= 100, 2, 1), pch = 16, type = "b", 
     col = ifelse(N >= 100, "red", "darkgreen"))
```

## 第八章 习题

```
x <- c(1, 1, 2, 2, 3)  # 生成一个向量。
is.character(x)  # x 是字符型吗？不是。
is.numeric(x)  # x 是数值型吗？是的。
mode(x)  # 确实是数值型。

y <- c(3, 4, 4, 5, 5)
z <- c(x, y)  # 多个向量并在一起。
z
z[4]  # 向量的下标。

# 生成一个矩阵，指定行数和列数：
m <- matrix(c(2, 3, 1, 5), nrow = 2, ncol = 2)
m
# 生成一个矩阵，指定行数：
m <- matrix(c(2, 3, 1, 5), nrow = 2)
m
# 生成一个矩阵，指定行数，并按行排列：
m <- matrix(seq(1, 20, 1), nrow = 5, byrow = TRUE)
m
# 生成一个矩阵，指定行数，并按列排列：
m <- matrix(seq(1, 20, 1), nrow = 5, byrow = FALSE)
m[2, 2]  # 矩阵的下标。

a <- c(1, 2, 3, 4)
b <- seq(5, 8, by = 1)
d <- data.frame(a, b)  # 生成一个数据框。
d
is.data.frame(d)  # 是数据框吗？
str(d)  # 数据框的结构。
class(d) 
nrow(d) # 数据框的行数。
ncol(d) # 数据框的列数。
e <- c(9, 10)
f <- rbind(d, e)  # 给数据框增加一行。
f
g <- c("one", "two", "three", "four", "five")
class(g)
h <- cbind(f, g)  # 给数据框增加一列。
h
class(h)
ncol(h)
colnames(h) <- c("one", "two", "three")  # 更改列名称。
h

is.numeric(d[, 1])
is.data.frame(d[1, ])
is.numeric(d[1, ])
is.numeric(unlist(d[1, ]))
mylist <- list(x = 1:4, y = letters[3:10])
mylist
mylist[[1]]
mylist[[1]][1]
mylist[[2]]
mylist[[2]][5]
mylist$x
mylist$y[3]
```

## 第九章 函数

```
y <- sd(x = 1:5)  # sd 是函数名, x 是自变量。
y
sd
assign("x", 1:5)

newscore <- function(x) {
  y <- sqrt(x) * 10
  return(y)
}
newscore(x = 40)

x <- 36
y <- 81
newscore(x = y)  # 函数内部的 x 把 81 的值接过来，而不是36。
x # 函数外部的x仍然是36。

news <- function(x, n) {
  sqrt(x) * 10 + n
}
news(x = 36, n = 10)
news(36, 10)
news(n = 10, x = 36)

newscore()
newscore <- function(x = 36) # 将x默认值设为36。
{
  sqrt(x) * 10
}
newscore()

exponentialGrowth <- function(N0, r = 0.01, tmax = 10) 
  # 三个自变量：初始值，增长率（默认为0.01），时间（默认为10）。
{
  N <- N0
  for(t in 1 : (tmax - 1)) {
    N[t + 1] <- N[t] + r * N[t]
  }
  return(N) 
}
plot(exponentialGrowth(80, 0.02, 100))

source('c:/r4r/myf.r')

install.packages("maptools") # 第一次使用某个扩展包时要先安装。
require(maptools)  # 调用包，让R把其中的函数读进R的脑子里。
position <- c(116.39, 39.91)  # 天安门广场的经纬度。
mydate <- "2017-10-01"  # 要计算的日期。
# 日出时刻：
sunriset(matrix(position, nrow = 1), 
         as.POSIXct(mydate, tz = "Asia/Shanghai"), 
         direction = c("sunrise"), POSIXct.out = TRUE)$time
# 日落时刻:
sunriset(matrix(position, nrow = 1), 
         as.POSIXct(mydate, tz = "Asia/Shanghai"), 
         direction = c("sunset"), POSIXct.out = TRUE)$time
# 函数名为flag，默认是计算2017年情人节开始一周内升降国旗时刻。
flag <- function(date.start = "2017-02-14", date.length = 7) 
{
  mydate <- seq(as.POSIXct(date.start, tz="Asia/Shanghai"), 
                by = 3600 * 24, length.out = date.length)
  data.frame(
    sunrise = sunriset(
      matrix(c(116.39, 39.91), nrow = 1), 
      as.POSIXct(mydate, tz="Asia/Shanghai"),
      direction=c("sunrise"), POSIXct.out = TRUE)$time,
    sunset = sunriset(
      matrix(c(116.39, 39.91), nrow = 1), 
      as.POSIXct(mydate, tz="Asia/Shanghai"), 
      direction=c("sunset"), POSIXct.out = TRUE)$time)
}

flag("2017-10-01") # 好了，以后调用这个函数就能很方便计算。


install.packages("beginr")
beginr::plotpch()
beginr::plotlty()
beginr::plottype()
beginr::plotcolors()

set.seed(123)
x <- 1:10
y <- 1:10 + rnorm(10)
beginr::plotlm(x, y, refline = TRUE)

x <- rnorm(10000)
beginr::plothist(x)

df <- data.frame(a = 1:10,
                 b = 1:10 + rnorm(10),
                 c = 1:10 + rnorm(10))
beginr::plotpairs(df)
beginr::plotpairs2(df)

par(mfrow = c(1,2), mar = c(0.1, 0.1, 0.1, 0.1))
x <- seq(0, 2 * pi, length.out = 100) 
y <- data.frame(sin(x), cos(x))
# 假定yerror是y的误差范围
yerror <- data.frame(abs(rnorm(100, sd = 0.3)), 
                     abs(rnorm(100, sd = 0.1)))
beginr::dfplot(x, y, yerror = yerror)
beginr::dfplot2(y, x, xerror = yerror, xlab = '', ylab = '')

x <- seq(0, 2 * pi, length.out = 100)
y <- sin(x)
plot(x, y, type = "l")
beginr::errorbar(x, y, yupper = 0.1, ylower = 0.1)
df <- data.frame(a = 1:10, 
                 b = 1:10 + rnorm(10), 
                 c = 1:10 + rnorm(10))
beginr::lmdf(df)

beginr::bib(pkg = c("mindr", "bookdownplus", "pinyin"))

install.packages("fortunes")
require(fortunes)
fortune('Actually, I see it as part of my job')
citation("bookdown")

length(unique(rownames(available.packages())))

a <- available.packages() # 获取所有扩展包的信息
b <- rownames(a) # 挑出扩展包的名称
c <- unique(b) # 去掉重复的名称
d <- length(c) # 数数有几个

beginr::plotpkg('rmarkdown', from = '2014-01-01')

install.packages(c("devtools", "roxygen2", "knitr", "beginr"))
beginr::rpkg()
newscore <- function(x) {
  y <- sqrt(x) * 10
  return(y)
}

#' Calculate new score
#'
#' @param x old score
#'
#' @return new score
#' @export
#'
#' @examples newscore(49)
newscore <- function(x) {
  y <- sqrt(x) * 10
  return(y)
}

library(mypkg)
newscore(36)

example(newscore)

devtools::install_github("pzhaonet/beginr")
```

## 第十章 字符

```
x <- 'The quick brown fox jumps over the lazy dog'
xlower <- tolower(x)
class(xlower)
length(x)
nchar(x)

myfile2 <- "c:/r4r/co2.csv"

xsingle <- strsplit(xlower, '')[[1]]
nchar(xsingle)
length(xsingle)

grep(xsingle[1], xsingle)
for(i in 1:length(xsingle)) print(grep(xsingle[i], xsingle))
for(i in 1:length(xsingle))
  print(paste(xsingle[i], grep(xsingle[i], xsingle)))
sapply(xsingle, function(x) grep(x, xsingle))
table(xsingle)
duplicated(xsingle)
xsingle[!duplicated(xsingle)]
unique(xsingle)
length(unique(xsingle))



download.file(url =
                "http://dapengde.com/r4rookies/qianziwen.txt",
              destfile = "c:/r4r/qianziwen.txt")
qzw <- readLines('c:/r4r/qianziwen.txt', encoding = 'UTF-8')
class(qzw)
length(qzw) #向量长度
nchar(qzw) #向量里每个元素包含的字符数
qzwmerged <- paste(qzw, collapse = '')
qzwmerged <- gsub(' ', '', qzwmerged)
nchar(qzwmerged)
qzwsingle <- strsplit(qzwmerged, '')[[1]]
chardup <- qzwsingle[duplicated(qzwsingle)]
for(i in chardup) print(paste(i, grep(i, qzw, value = TRUE)))


download.file(url =
                "http://dapengde.com/r4rookies/kdclip.txt",
              destfile = "c:/r4r/kdclip.txt")
aa <- readLines("c:/r4r/kdclip.txt", encoding = "UTF-8")
length.aa <- length(aa)
title <- aa[c(seq(1, length.aa, by = 5))]
title.o <- order(title)
title <- title[title.o]
highlight <- aa[c(seq(4, length.aa, by = 5))][title.o]
kn <- data.frame(Title = title, Highlight = highlight)
write.table(kn, "c:/r4r/kn.txt",
            sep = "\t", row.names = FALSE)
location <- aa[c(seq(2, length.aa, by = 5))][title.o]
location[1]
time.aa <- substr(location,
                  (regexpr(" Added on ", location) + 10) ,
                  nchar(location))[title.o]
loc <- substr(
  location, 13,
  regexpr(" Added on ", location) - 5)[order(title.o)]
kn <- data.frame(Title = title, Highlight = highlight,
                 Loc = loc, Time = time.aa)
write.table(kn, "c:/r4r/kn2.txt",
            sep = "\t", row.names = FALSE)

```

## 第十一章 地图

```
download.file(url = "http://dapengde.com/r4rookies/us.csv",
              destfile = "c:/r4r/us.csv")
us <- read.csv("c:/r4r/us.csv")
summary(us)
nlevels(us$state)
plot(us$lon, us$lat)

plot(us$lon, us$lat)
points(us$lon[us$state == "Texas"],
       us$lat[us$state == "Texas"], col="blue")

cols <- rainbow(nlevels(us$state))
plot(us$lon, us$lat, col = cols[us$state], pch = 20)

lon.median <- tapply(us$lon, us$state, median)
lat.median <- tapply(us$lat, us$state, median)
text(labels = levels(us$state), x = lon.median, y = lat.median, 
     cex = 0.5, col = 'White')
points(-74.02, 40.73, pch = 17, cex = 2)


download.file(url = "http://dapengde.com/r4rookies/cm.zip",
              destfile = "c:/r4r/cm.zip")
unzip(zipfile = "c:/r4r/cm.zip", exdir = "c:/r4r")
install.packages('rgdal')
require(rgdal) 
cm <- readOGR(dsn = "c:/r4r/cm", layer = "bou2_4p") 
plot(cm)

summary(cm)
is.factor(cm$NAME)
levels(cm$NAME)  # 省市名称。

download.file(url =
                "http://dapengde.com/r4rookies/aqi.csv",
              destfile = "c:/r4r/aqi.csv")
aqi <- read.csv("c:/r4r/aqi.csv")
aqi
aqstandard <- c(0, 50, 100, 150, 200, 300, 500, Inf)
aqilevel <- cut(aqi$aqi[match(levels(cm$NAME),aqi$province)], 
                aqstandard)
mycol <- grey(seq(1, 0, 
                  length.out = nlevels(aqilevel)))[aqilevel]
col <- cm$NAME
levels(col) <- mycol
plot(cm, col = as.character(factor(col)), axes = TRUE)

install.packages('plotrix')
library(plotrix)
legendn <- character((length(aqstandard) - 2) * 2 + 1)
legendn[seq(2, length(legendn), by = 2)] <- 
  aqstandard[2:(length(aqstandard)-1) ]
color.legend(
  xl = 135, yb = 10, xr = 137, yt = 30,legend = legendn,
  rect.col = grey(seq(1, 0, length.out = nlevels(aqilevel))),
  align = "lb", gradient = "y")  # 添加图例。
color.legend(
  xl = 135, yb = 10, xr = 137, yt = 30,
  legend = c('Excellent','Good','Lightly', 'Moderately', 
             'Heavily', 'Severely', 'OMG'),
  rect.col = grey(seq(1, 0, length.out = nlevels(aqilevel))),
  align = "rb", gradient = "y")  # 添加图例。

install.packages('leafletCN')
require(leafletCN)
aqi$aqi[aqi$aqi == -1] <- NA
pvs <- regionNames("china")
loc <- match(pvs, aqi$province)
aqi2 <- data.frame(name = pvs, value = aqi$aqi[loc])
geojsonMap(dat = aqi2, mapName = "china",
           popup =  paste(aqi2$name, aqi2$value),
           legendTitle = "AQI")
```

## 第十二章 时间

```
bd <- '1994-09-22 20:30:00'
bdtime <- strptime(x = bd, format = '%Y-%m-%d %H:%M:%S', 
                   tz = "Asia/Shanghai")
bdtime

class(bd)
class(bdtime)
t1 <- Sys.time() # 返回当前时刻
t2 <- date() # 返回当前时刻
t3 <- Sys.Date() # 返回当前日期
t1
t2
t3
class(t1)
class(t2)
class(t3)
bdtime$wday

unlist(unclass(bdtime))
format(bdtime, format = '%d.%m.%Y')

bdtime + 1
bdtime + 60
bdtime + 3600

t3 <- bdtime + 86400
t3

bdtime2 <- strptime(
  '1995-09-01 7:30', format = '%Y-%m-%d %H:%M', 
  tz = 'Asia/Shanghai')
bdtime2 - bdtime

difftime(time1 = bdtime2, time2 = bdtime, units = 'secs')

mean(c(bdtime, bdtime2))

(a <- strptime("2018-03-25 03:00:00", 
              format = "%Y-%m-%d %H:%M:%S", tz = "CET"))
a - 1
(a <- as.POSIXlt("2018-03-25 03:00:00", tz = "CET"))
a - 1
(a <- as.POSIXlt("2018-03-25 02:00:00", tz = "CET"))
(a <- strptime("2018-03-25 02:00:00", 
              format = "%Y-%m-%d %H:%M:%S", tz = "CET"))
a - 1
```

## 第十三章 批量处理文件

```
download.file(url= "http://dapengde.com/r4rookies/figren.zip",
              destfile = "c:/r4r/figren.zip")
unzip(zipfile = "c:/r4r/figren.zip", exdir = "c:/r4r")
fotodir <- 'c:/r4r/figren'
fotofilefull <- dir(fotodir, full.names = TRUE)
fotofile <- dir(fotodir)
fotoinfo <- file.info(fotofilefull)
fotoinfo
fototime <- format(fotoinfo$mtime, '%Y-%m-%d-%H%M%S')
newname <- paste(
  fotodir, '/', fototime, '_', fotofile, sep = '')
file.rename(fotofilefull, newname)

urlink <- 'http://www.biomet.co.at/pictures/'
aa <- readLines(urlink, encoding = 'UTF-8') # 读取网页
linkformat <-
  'src="http://www.biomet.co.at/wp/wp-content/gallery'
bb <- aa[grep(linkformat, aa)]

for(i in 1:length(bb))
  bb[i] <- substring(
    bb[i],
    regexpr("http", bb[i])[1],
    regexpr(".jpg\"", bb[i])[1]+3) # 获取链接
bb <- unique(bb)
length(bb)
writeLines(bb, 'c:/r4r/links.txt')

stname <- substring(bb, 47, 50)
stname <- stname[-which(stname == '')]
for(i in unique(stname))
  dir.create(paste('c:/r4r/', i, sep = ''))

for(i in 1:length(bb)) {
  download.file(
    url = bb[i],
    destfile = paste(
      'c:/r4r/', stname[i],'/', stname[i], i, '.jpg',
      sep = ""),
    method = 'curl', quiet = TRUE)
  print(paste(i, 'of', length(bb), 'downloaded.'))
}
winDialog(type = c("ok"), message = '下载完毕！')

download.file(url = "http://dapengde.com/r4rookies/obs.zip",
              destfile = "c:/r4r/obs.zip")
unzip(zipfile = "c:/r4r/obs.zip", exdir = "c:/r4r")
stn <- 54527
obsdir <- 'c:/r4r/obs'
obsfilefull <- dir(obsdir, full.names = TRUE)
obstime <- as.numeric(dir(obsdir))
output <- NULL
for(k in 1:length(obsfilefull))
{
  input <- read.table(obsfilefull[k], header = FALSE,
                      skip = 2, sep="")
  output_new <- input[which(input[, 1] == stn),]
   if(nrow(output_new) != 0)
     rownames(output_new) <- obstime[k]
  output <- rbind(output, output_new)
}
output$time <- rownames(output)


shell('notepad')
shell('start iexplore http://xuer.pzhao.net')
shell('cmd /c "D:/Program Files/Tencent/QQProtect.exe"')
```

## 第十四章 论文书稿写作

```
install.packages("bookdownplus")
require(bookdownplus)
for(i in template()[1:19])
  bookdownplus(template = i,
               more_output = more_output()[1:3])
for(mf in mail_font()) {
  for(ms in mail_style()) {
    for(mt in mail_theme()) {
      outputname <- paste('mail', ms, mf, mt, sep = '_')
      bookdownplus(template = 'mail',
                   mail_style = ms,
                   mail_font = mf,
                   mail_theme = mt,
                   output_name = outputname)
    }
  }
}

bookdownplus(template = 'article')

bookdownplus(template = template()[1])
template()

bookdownplus(template = 'article',
             author = 'John Smith',
             title = 'My article')

more_output()

bookdownplus(template = 'article',
             more_output = more_output())

bookdown::publish_book()

bookdownplus(template = 'thesis_ubt')

bookdownplus(template = 'thesis_mypku')

install.packages('mindr')
library('mindr')
md2mm()

bookdownplus(template = `nte_zh`)

bookdownplus(template = 'journal')

bookdownplus(template = 'guitar')

```

## 第十五章 搭建小型网站

```
if(!require(devtools)) install.packages('devtools')
devtools::install_github('rstudio/blogdown')
blogdown::install_hugo()
setwd('c:/blogdown_default')
blogdown::new_site()
blogdown::serve_site()
blogdown::build_site()
setwd('c:/blogdown_default')
blogdown::new_site(theme='gcushen/hugo-academic')
```

## 第十六章 在工作中应用

```
rdoc <- readLines('c:/r4r/rdoc.Rmd', encoding = 'UTF-8')
for(k in 1:7) {
  newrmd <- paste('c:/r4r/', k, '.Rmd', sep = '')
  rdoc[13] <- paste('i <-', k)
  writeLines(rdoc, newrmd, useBytes = TRUE)
  rmarkdown::render(newrmd, encoding = 'UTF-8')
}
```

## 第十七章 用 R 进行基础统计（一）：概率分布检验

```
binom.test(x = 27, n = 60, p = 0.5, alternative = "less")
binom.test(x = 203, n = 558, p = 0.4, alternative = "less")
binom.test(x = 203, n = 558, p = 0.4, alternative ="greater")

poisson.test(13,15) 
poisson.test(13,24,alternative="less")

qpois(0.95,lambda =24)
qpois(0.05,lambda =24)

x <- 0:6
y <- c(7, 10, 12, 8, 3, 2, 0)
mean <- mean(rep(x, y))
q <- ppois(x, mean)
n <- length(y)
p <- q
p[1] <- q[1]
p[n] <- 1 - q[n - 1]
for(i in 2:(n - 1))
  p[i] <- 1 - q[i - 1]
chisq.test(y, p = rep(1/length(y), length(y)))

myfreq<-c(30,21,24,35,42,48) # 得到的频数
myprobs<-c(1,1,1,1,1,1)/6 # 指定的概率分布
chisq.test(myfreq,p=myprobs)

par(mfcol=c(1,2),ps=6.5)
hist(AirPassengers,breaks=20)
qqnorm(AirPassengers,pch=1)
shapiro.test(AirPassengers)

par(mfcol=c(1,2),ps=6.5)
hist(lh,breaks=20)
qqnorm(lh,pch=1)
shapiro.test(lh) #人群血样中促黄体浓度属于正态分布吗？

A <- rnorm(100,5,3) 
ks.test(A,5,3) 
ks.test(A,15,1) 
set.seed(1)
mydata <- rexp(950)
ks.test(mydata, "pexp")
set.seed(1)
mydata <- rgamma(1500,1)
ks.test(mydata, "pgamma", 1)
ks.test(mydata, "pgamma", 2)
set.seed(1)
mydata<-rweibull(8500,1)
ks.test(mydata, "pweibull", 1)
ks.test(mydata, "pweibull",2)
ks.test(co2[1:12],co2[97:108],alternative ="two.sided")
qnorm(0.025)
qnorm(0.975)
```

## 第十八章 用 R 进行基础统计（二）：均值比较和方差分析

```
myco2<-co2[1:12]
myco2
t.test(myco2,mu=316.45)
myco2.t1 <- co2[1:12] # 1959年的观测数据
myco2.t2 <- co2[13:24] # 1960年的观测数据
t.test(myco2.t1,myco2.t2)
myco2.t1 <- co2[1:12] # 1959年的观测数据
myco2.t3 <- co2[97:108] # 1965年的观测数据
t.test(myco2.t1,myco2.t3)

require(graphics) # 学生的睡眠数据
with(sleep, t.test(extra[group == 1], extra[group == 2]))
sleep 
t.test(extra ~ group, data = sleep) 
require(graphics)##学生的睡眠数据
with(sleep, t.test(extra[group == 1], extra[group == 2]))
t.test(extra ~ group, data = sleep,paired=TRUE)

attach(airquality)
Month <- factor(Month, labels = month.abb[5:9])
pairwise.t.test(Ozone, Month)
pairwise.t.test(Ozone, Month, p.adj = "bonf")
pairwise.t.test(Ozone, Month, pool.sd = FALSE)
detach()

oneway.test(weight~feed,data=chickwts, var.equal=T)
oneway.test(extra ~ group, data = sleep)
oneway.test(extra ~ group, data = sleep, var.equal = TRUE)
summary(aov(weight~feed,data=chickwts))
library(geepack)
data(dietox)
weight<-aov(Weight~Cu+Evit,data=dietox)
summary(weight)

data(dietox)
weight<-aov(Weight~Cu+Evit+Cu*Evit,data=dietox)
summary(weight)
data(seizure)
seiz.l <- reshape(seizure, 
    varying = list(c("base","y1", "y2", "y3", "y4")),
    v.names="y", times = 0:4, direction = "long")
seiz.l <- seiz.l[order(seiz.l$id, seiz.l$time),]
seiz.l$t <- ifelse(seiz.l$time == 0, 8, 2)
seiz.l$x <- ifelse(seiz.l$time == 0, 0, 1)
result <- aov(y ~ x + trt + x * trt, data=seiz.l)
summary(result)
data(dietox)
weight<-aov(Weight~Cu+Time+Cu*Time,data=dietox)
summary(weight)
wilcox.test(airquality$Ozone, mu = 36, 
    subset = Month %in% c(5, 8), exact = NULL, 
    correct = TRUE,conf.int = FALSE, conf.level = 0.95)
require(graphics)
x <- c(1.83,  0.5,  1.62,  2.48, 1.68, 1.88, 1.55, 3.06, 1.3)
y <- c(0.878, 0.647,0.598, 2.05, 1.06, 1.29, 1.06, 3.14,1.29)
wilcox.test(x, y, paired = TRUE, alternative = "greater")
wilcox.test(y - x, alternative = "less")
wilcox.test(y - x, alternative = "less",
            exact = FALSE, correct = FALSE)
x<-randu$x
y<-randu$y
wilcox.test(x,y,paired=FALSE) # Wilcox秩和检验
wilcox.test(x,y,paired =TRUE) # Mann-Whitney U检验
boxplot(weight~group, data=PlantGrowth)

kruskal.test(weight~group, data=PlantGrowth)
RoundingTimes <-  matrix(c(5.40, 5.50, 5.55,
                           5.85, 5.70, 5.75,
                           5.20, 5.60, 5.50,
                           5.55, 5.50, 5.40,
                           5.90, 5.85, 5.70,
                           5.45, 5.55, 5.60,
                           5.40, 5.40, 5.35,
                           5.45, 5.50, 5.35,
                           5.25, 5.15, 5.00,
                           5.85, 5.80, 5.70,
                           5.25, 5.20, 5.10,
                           5.65, 5.55, 5.45,
                           5.60, 5.35, 5.45,
                           5.05, 5.00, 4.95,
                           5.50, 5.50, 5.40,
                           5.45, 5.55, 5.50,
                           5.55, 5.55, 5.35,
                           5.45, 5.50, 5.55,
                           5.50, 5.45, 5.25,
                           5.65, 5.60, 5.40,
                           5.70, 5.65, 5.55,
                           6.30, 6.30, 6.25),
    nrow = 22,byrow = TRUE,
    dimnames = list(1:22,
        c("Round Out", "Narrow Angle", "Wide Angle")))
friedman.test(RoundingTimes)

data(iris)#鸢尾花数据集
head(iris)#查看下数据集
iris.data<-iris[,-5]#去掉最后一列，非数字变量
cor(iris.data)
head(airquality)
cor.test(airquality$Wind,airquality$Temp)
cor.test(airquality$Wind,airquality$Temp,method = "kendall")
if(!require(psych)) install.packages("psych")
library(psych)
corr.test(iris.data)
corr.test(iris.data)$r
corr.test(iris.data)$p
print(corr.test(iris.data)$r,digits=3)
if(!require(graphics)) install.packages(graphics)
require(graphics)
pairs(iris)
if(!require(corrplot)) install.packages("corrplot")
library(psych)
library(corrplot)
par(cex = 0.5)
corrplot(corr.test(iris.data)$r)

data(mtcars)
M <- cor(mtcars)
# different color series
col1 <- colorRampPalette(c("#7F0000","red","#FF7F00",
    "yellow","white", "cyan", "#007FFF", "blue","#00007F"))
col2 <- colorRampPalette(c("#67001F", "#B2182B", "#D6604D", 
    "#F4A582", "#FDDBC7", "#FFFFFF", "#D1E5F0", "#92C5DE", 
    "#4393C3", "#2166AC", "#053061"))
col3 <- colorRampPalette(c("red", "white", "blue"))
col4 <- colorRampPalette(c("#7F0000","red","#FF7F00",
    "yellow","#7FFF7F", "cyan", "#007FFF", "blue","#00007F"))
wb <- c("white","black")

library(corrplot)
par(mfrow = c(2,1))
corrplot(M, method = "number")
corrplot(M)

corrplot(M, order = "AOE", col = col1(20), cl.length = 21, 
         addCoef.col = "grey")

par(mfrow = c(3,1))
corrplot(M, method = "ellipse", col = col1(200),order ="AOE")
corrplot(M, method = "shade", col = col3(20),order = "AOE")
corrplot(M, method = "pie", order = "AOE")

par(mfrow = c(2,1))
corrplot(M, col = wb, order="AOE", outline=TRUE, cl.pos="n")
corrplot(M, col = wb, bg="gold2",  order="AOE", cl.pos="n")

corrplot(M,order = "AOE", type = "upper", tl.pos = "d")
corrplot(M,add = TRUE, type = "lower", method = "ell", 
    order = "AOE", diag=FALSE, tl.pos= "n", cl.pos = "n")
par(mfrow = c(2,1))

ran <- round(matrix(runif(225, -100,100), 15))
corrplot(ran, is.corr=FALSE)
corrplot(ran, is.corr=FALSE, cl.lim=c(-100, 100))
par(mfrow = c(3,1))

corrplot(M, order="AOE", tl.srt=60)
corrplot(M, order="AOE", diag=FALSE, tl.pos="d")
corrplot(M, order="AOE", type="lower", cl.pos="b")
cor.mtest <- function(mat, conf.level = 0.95){
  mat <- as.matrix(mat)
  n <- ncol(mat)
  p.mat <- lowCI.mat <- uppCI.mat <- matrix(NA, n, n)
  diag(p.mat) <- 0
  diag(lowCI.mat) <- diag(uppCI.mat) <- 1
  for(i in 1:(n-1)){
    for(j in (i+1):n){
      tmp <- cor.test(mat[,i], mat[,j], 
                      conf.level = conf.level)
      p.mat[i,j] <- p.mat[j,i] <- tmp$p.value
      lowCI.mat[i,j] <- lowCI.mat[j,i] <- tmp$conf.int[1]
      uppCI.mat[i,j] <- uppCI.mat[j,i] <- tmp$conf.int[2]
    }
  }
  return(list(p.mat, lowCI.mat, uppCI.mat))
}

res1 <- cor.mtest(mtcars,0.95)
res2 <- cor.mtest(mtcars,0.99)

par(mfrow = c(3,1))
corrplot(M, p.mat = res1[[1]], sig.level = 0.2)
corrplot(M, p.mat = res1[[1]], insig = "p-value",
         sig.level= -1) # add all p-values
corrplot(M, p.mat = res1[[1]], order = "hclust", 
         insig = "pch", addrect = 3)

if(!require(ellipse)) install.packages('ellipse')
library(ellipse)
library(psych)
mycol = colors()[as.vector(apply(corr.test(
  iris.data)$r, 2, rank))]
plotcorr(corr.test(iris.data)$r, 
         col = mycol, mar = rep(0, 4))
x <- c(44.4, 45.9, 41.9, 53.3, 44.7, 44.1, 50.7, 45.2, 60.1)
y <- c( 2.6,  3.1,  2.5,  5.0,  3.6,  4.0,  5.2,  2.8,  3.8)
par(mfrow = c(2, 1), mar = c(2, 4, 0.1, 0.1))
plot(x)
lines(x)
plot(y)
lines(y)
cor.test(x, y, method = "spearm", alternative = "g")
cov(x,y)
cor.test(x, y, method = "spearm", alternative = "g")
x <- as.data.frame(x) # 这个命令要求x是数据框或者矩阵
cov.wt(x, wt = rep(1/nrow(x), nrow(x)), cor = FALSE,
       center = TRUE, method = c("unbiased", "ML"))
xy <- cbind(x = 1:10, y = c(1:3, 8:5, 8:10))
w1 <- c(0,0,0,1,1,1,1,1,0,0)
cov.wt(xy, wt = w1) # i.e. method = "unbiased"
cov.wt(xy, wt = w1, method = "ML", cor = TRUE)
knitr::opts_chunk$set(tidy = FALSE)
```