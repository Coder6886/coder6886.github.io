---
layout:     post
title:      关于π是无理数的简单证明
subtitle:   
date:       2022-11-12
author:     coder6886
header-img: img/post-bg-island.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
这个证明的pdf版本在[这里](https://github.com/Coder6886/coder6886.github.io/blob/master/word_files/A_Simple_Proof_that_Pi_is_Irrational.pdf)

证明过程：

这个证明使用了反证法。

# 第一步：各种“设”

假设$\pi=\frac{a}{b},a,b\in\mathbb{Z^+}$

定义：

$$

f(x)=\frac{x^n(a-bx)^n}{n!}

$$

$$

F(x)=f(x)-f^{(2)}(x)+f^{(4)}(x)-...+(-1)^nf^{(2n)}(x)

$$

，其中n为任意正整数，且$f^{(i)}(x)$为$f(x)$的$i$阶导数。

# 第二步：取整数值

首先，我们知道f是一个$2n$次多项式，而且次数低于n的所有项的系数为0（前面带一个$x^n$）。

其次，我们知道$f(x)=f(\frac{a}{b}-x)$。

我们现在要证明：

## 对于任意$0\leq i \leq 2n$，$f^{(i)}(0)\in\mathbb{Z}$

### 对于$0\leq i< n$：

$f^{(i)}(0)$就是$f^{(i)}(x)$的常数项，也就是0。
### 对于$n\leq i\leq 2n$：

$f^{(i)}(0)$就是$f^{(i)}(x)$的常数项。但是因为$n!f(x)$的所有项的系数都是整数，并且$f^{(i)}(x)$的常数项就是$f(x)$的i次项系数乘以$i!$，而$n!\big\|i!$，所以$f^{(i)}(0)$为整数。

那知道了上面的事实也就知道了$f(\frac{a}{b})$为整数。

# 第三步：微分和积分

$$

\frac{d}{dx}\{F'(x)sin\,x-F(x)cos\,x\}

$$

$$

=\frac{d}{dx}F'(x)sin\,x-\frac{d}{dx}F(x)cos\,x

$$

$$

=F''(x)sin\,x+F'(x)cos\,x-F'(x)cos\,x+F(x)sin\,x

$$

$$

=sin\,x(F''(x)+F(x))

$$

$$

=sin\,x\,(f(x)-f^{(2)}(x)+f^{(4)}(x)-...+(-1)^nf^{(2n)}(x)+\\\f^{(2)}(x)-f^{(4)}(x)+...-(-1)^nf^{(2n)}(x)+(-1)^nf^{(2n+2)}(x))

$$

$$

\because n是一个2n次多项式\therefore f^{(2n+2)}(x)=0

$$

$$

\therefore 上式=f(x)sin\,x

$$

$$

\int^{\pi}_0f(x)sin\,x\,dx=[F'(x)sin\,x-F(x)cos\,x]\big|^{\pi}_0=F(\pi)+F(0)

$$

# 第四步：推出矛盾

对于任意$0<x<\pi$,

$$

0<f(x)sin\,x\leq f(x)<\frac{\pi^na^n}{n!}

$$

$$

\therefore0<\int^{\pi}_0f(x)sin\,x\,dx=F(\pi)+F(0)<\pi\frac{\pi^na^n}{n!}=\frac{\pi^{n+1}a^n}{n!}

$$

$$

\because 对于任意0\leq i \leq 2n，f^{(i)}(0),f^{(i)}(\frac{a}{b})\in\mathbb{Z}

$$

$$

\therefore F(\pi)+F(0)\in\mathbb{Z^+}

$$

当n趋向于$\infty$时，$\frac{\pi^{n+1}a^n}{n!}$趋向于0，而$F(\pi)+F(0)$是正整数，而且（当n足够大时）任意小，矛盾。

所以$\pi$是无理数。

Quite "Easily" Done.