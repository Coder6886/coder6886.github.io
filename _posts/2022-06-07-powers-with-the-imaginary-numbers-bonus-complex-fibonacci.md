---
layout:     post
title:      关于复数的幂运算（还有复数斐波那契数列）
subtitle:   
date:       2022-06-07
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
在普通的教科书里，$a^b$里的底数$a$必须符合条件$a>0$。

但是今天，我们要说另一种幂运算：$a^b(a\in\mathbb{C},b\in\mathbb{C})$！

底数和指数的范围都扩充到了虚数域里。

# 1.一览无余

直接上公式：

当底数$z=\rho e^{i\theta}$,指数$w=a+bi$：

$$

z^w=\rho^ae^{-b\theta}(cos(bln\rho+a\theta)+isin(bln\rho+a\theta))

$$

这就是今天我要证明的公式。

# 2.开始证明

## 2.1.关于$wlnz$

首先我们需要证明$lnz=ln\rho+i\theta$(别忘了$z=\rho e^{i\theta}$)

这个其实很好证。

首先由于$ln(AB)=lnA+lnB$：

$$

ln(\rho *e^{i\theta})=ln\rho+ln(e^{i\theta})

$$

$$

ln\rho+ln(e^{i\theta})=ln\rho+i\theta（提示：ln(e^x)=x）

$$

那我们的第一个结论就证明完毕了。

接下来我们要展开$wlnz$（别忘了$w=a+bi$）。

$$

wlnz=(a+bi)(ln\rho+i\theta)=aln\rho+ia\theta+ibln\rho-b\theta（这一步只是普通展开）

$$

$$

aln\rho+ia\theta+ibln\rho-b\theta=(aln\rho-b\theta)+i(a\theta+bln\rho)（这一步只不过是整理）

$$

那我们2.1的任务就完成了。

## 2.2.这就冲刺了！！

这就是最后一段的证明。

先要知道两个东西：$1.e^{x+y}=e^xe^y,2.e^{ylnx}=x^y$，然后继续：

$$

z^w=e^{wlnz}=e^{(aln\rho-b\theta)+i(a\theta+bln\rho)}

$$

$$

=e^{(aln\rho-b\theta)}e^{i(a\theta+bln\rho)}

$$

$$

=e^{(aln\rho-b\theta)}(cos(bln\rho+a\theta)+isin(bln\rho+a\theta))（这一步的来由是e^{i\theta}=cos\theta+isin\theta）

$$

$$

=e^{aln\rho}e^{-b\theta}(cos(bln\rho+a\theta)+isin(bln\rho+a\theta))

$$

$$

=\rho^ae^{-b\theta}(cos(bln\rho+a\theta)+isin(bln\rho+a\theta))（这一步其实运用了e^{ylnx}=x^y）

$$

# 3.示例（斐波那契数列）
这是一个斐波那契数列的示例。

大家都知道1，1，2，3，5，8……是斐波那契数列，生成斐波那契数列的函数是：

$$

F(n)=\frac{\phi^n-(\frac{1}{-\phi})^n}{\sqrt5}

$$

其中$\phi$是黄金分割比($\frac{1+\sqrt5}{2}\approx1.618$)

这个公式的具体证明请看[这里](https://www.youtube.com/watch?v=e7SnRPubg-g)（这里还有关于另一个数列的故事……）

那如果$F(n)$中$n$不是整数，而是一个任意的实数，那会发生什么？

没错！$F(n)$的输出就是一个复数！

但是这个复数的实部和虚部都是什么？

首先，目光聚焦到带给我们虚部的$(\frac{1}{-\phi})^n$。

我们先要化简这个式子。

对于$\rho,\theta,a$和$b$，这些数在这个情况下的值是：

$$

\rho=\frac{1}{\phi},\theta=\pi,a=n,b=0（为什么呢？因为z=-\frac{1}{\phi}=\frac{1}{\phi}e^{i\pi},w=n=n+0i）

$$

其实使用这个公式有一些“杀鸡用牛刀”的意思，因为这个情况下底数和指数都不是复数。

根据上面这些值，可以计算出：

$$

(\frac{1}{-\phi})^n=(\frac{1}{\phi})^n(cos(\pi n)+isin(\pi n))（这一步就是带入化简）

$$

所以

$$

F(n)=\frac{\phi^n-(\frac{1}{-\phi})^n}{\sqrt5}=\frac{\phi^n-(\frac{1}{\phi})^n(cos(\pi n)+isin(\pi n))}{\sqrt5}

$$

化简后可得：

$$

F(n)=\frac{\phi^n-(\frac{1}{\phi})^ncos(\pi n)}{\sqrt5}-i\frac{(\frac{1}{\phi})^nsin(\pi n)}{\sqrt5}

$$

这就是（复）斐波那契数列。

[这](https://github.com/Coder6886/coder6886.github.io/blob/master/word_files/complex-fibonacci.ggb)是我做的一个（复）斐波那契数列的动画的下载链接。

它使用的就是这个方程。

# 4.总结

其实这个公式好像不太有人知道……

通过上面的“杀鸡用牛刀”可以看出来这个公式的用途。让我们再来看看这个公式有没有可能出一些“岔子”。

首先，$a,b,\rho$都是正数，所以$ln\rho$不会出来一些定义域的问题，$e^{-b\theta}$也是一个实数，$\rho^a$也是一个正数。
