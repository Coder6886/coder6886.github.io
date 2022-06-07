---
layout:     post
title:      关于复数的幂运算
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

但是今天，我们要说另一种幂运算：$a^b(a\in\mathbb{I},b\in\mathbb{I})$！

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

## 3.总结
这就证明完了！

其实这个公式好像不太有人知道……

让我们看看这个公式有没有实际用处……

首先，$a,b,\rho$都是正数，所以$ln\rho$不会出来一些定义域的问题，$e^{-b\theta}$也是一个实数，$\rho^a$也是一个正数。

所以这个公式应该还是有用的。
