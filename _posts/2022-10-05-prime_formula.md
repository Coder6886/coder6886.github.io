---
layout:     post
title:      必读！素数生成公式
subtitle:   虽然这个公式复杂度极高
date:       2022-10-05
author:     coder6886
header-img: img/post-bg-island.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
# 这篇文章参考的论文是由C.P.Willans写的。

# 如果想要论文PDF版本[=>请戳我<=](https://github.com/Coder6886/coder6886.github.io/blob/master/word_files/On_Formulae_for_the_Nth_Prime_Number.pdf)（这篇文章只解释它推导的第一个公式，不对第二个进行解释，希望读者自行查看）

好了，话入正题。

这个公式是什么呢？

$$

p_n=1+\sum^{2^n}_{i=1}\bigg\lfloor\bigg(\frac{n}{\sum^i_{j=1}\big\lfloor cos^2\,\pi\frac{(j-1)!+1}{j}\big\rfloor}\bigg)^{\frac{1}{n}}\bigg\rfloor

$$

额……稍微长了一点点……但是也还行。

那（希望）大部分人都要问“这东西是真的吗？咋证出来的？”

# 证明

好吧。从里往外说。

## 核心部分
先说最中间的那个式子：

$$

\frac{(j-1)!+1}{j}

$$

这个式子有什么可以说的呢？

这个式子当且仅当$j=质数或1$时才是整数。

如何证明？这就要留给[威尔逊定理](https://www.wikiwand.com/zh-hans/%E5%A8%81%E5%B0%94%E9%80%8A%E5%AE%9A%E7%90%86)了。

## 判断整数

然后外面有一圈

$$

\big\lfloor cos^2\,\pi x\big\rfloor

$$

其中$x$就是一个输入。

外面这一圈的输入是：

$$

\begin{cases} 1\ 当输入为整数 \\ 0\ 当输入不是整数\end{cases}

$$

为什么呢？

看一下函数图像就行了：

![prime_formula_fig1.png](/img/prime_formula_fig1.png)

这是$cos^2\pi x$的函数图像。五彩缤纷的竖线分别是$x=0,x=1,...$可以看到当且仅当输入为整数时这个函数的值会是1。其他值都$\in[0,1)$。所以只要下取整，这个函数就会在整数上值为1，其他地方值为0。

所以

$$

\big\lfloor cos^2\,\pi\frac{(j-1)!+1}{j}\big\rfloor

$$

就构成了一个函数，使得函数的值是：

$$

\begin{cases} 1\ 当j为质数或1 \\ 0\ 当j是合数\end{cases}

$$

## $\pi(i)$

然后外面套一个

$$

\sum^i_{j=1}

$$

意思就是小于i的质数个数+1。

举例：

当i=10时，这个和就是：

$$

1+1+1+0+1+0+1+0+0+0=5

$$

第一个1代表的是$j=1$，剩下的1代表的是$j=$小于10的所有质数。

现在引入一种新写法。我们定义$\pi(n)$为不大于n的质数的个数。

则

$$

\pi(i)+1=\sum^i_{j=1}\big\lfloor cos^2\,\pi\frac{(j-1)!+1}{j}\big\rfloor

$$

## 使用数学构造不等式

那

$$

\bigg\lfloor\bigg(\frac{n}{\sum^i_{j=1}\big\lfloor cos^2\,\pi\frac{(j-1)!+1}{j}\big\rfloor}\bigg)^{\frac{1}{n}}\bigg\rfloor=\bigg\lfloor\bigg(\frac{n}{\pi(i)+1}\bigg)^{\frac{1}{n}}\bigg\rfloor

$$

是什么意思呢？

![prime_formula_fig2.png](/img/prime_formula_fig2.png)

这是

$$

\big(\frac{x}{4+1}\big)^\frac{1}{x}

$$

的函数图像。当输入x为**整数**时，这个函数的输出是：

$$

\begin{cases} \in[1,2)的某个数 \ 当x>4 \\ \in[0,1)的某个数\ 当x\leq4\end{cases}

$$

注意，**输入x为整数！！**

将上面的函数下取整，可得

$$

\begin{cases} 1 \ 当x>4 \\ 0\ 当x\leq4\end{cases}

$$

将x替换为n，4替换为$\pi(i)$可以知道这个函数的输出是：

$$

\begin{cases} 1 \ 当n>\pi(i) \\ 0\ 当n\leq\pi(i)\end{cases}

$$

而当且仅当第n个质数大于i时$n>\pi(i)$;当且仅当第n个质数不大于i时$n\leq\pi(i)$。**（多思考一下）**

所以上面的那个式子可以改成

$$

\begin{cases} 1 \ 当第n个质数>i \\ 0\ 当第n个质数\leq i\end{cases}

$$

也就是

$$

\begin{cases} 1 \ 当i<第n个质数 \\ 0\ 当i\geq第n个质数\end{cases}

$$

## 最终求和

在外面再套一圈

$$

\sum^{2^n}_{i=1}

$$

我们一定知道$2^n$之内至少有n个质数（不知道？[看这里：伯特兰-切比雪夫定理](https://www.wikiwand.com/zh-hans/%E4%BC%AF%E7%89%B9%E8%98%AD-%E5%88%87%E6%AF%94%E9%9B%AA%E5%A4%AB%E5%AE%9A%E7%90%86)）。

举例：

n=4

这个和就是：

$$

1+1+1+1+1+1+0+0+0+0+0+0+0+0+0+0

$$

也就是6。为什么呢？因为第n=4个质数是7，所以从1到6所有的数都小于7，也就全是1。剩下的数（包括7）都是0。而6个1+10个0就是6，也就是第n=4个质数减去1。将最终结果加回一个1就可以。

# 再看一看这个公式是不是觉得懂了呢？

$$

p_n=1+\sum^{2^n}_{i=1}\bigg\lfloor\bigg(\frac{n}{\sum^i_{j=1}\big\lfloor cos^2\,\pi\frac{(j-1)!+1}{j}\big\rfloor}\bigg)^{\frac{1}{n}}\bigg\rfloor

$$

