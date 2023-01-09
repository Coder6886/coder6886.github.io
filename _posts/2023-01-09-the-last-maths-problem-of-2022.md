---
layout:     post
title:      2022年我做完的最后一道数学题
subtitle:   这是我的一个小发现
date:       2023-12-12
author:     coder6886
header-img: img/post-bg-island.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---

今天抽空写一下2022年我做完的最后一道数学题。

这道题是我自己编的，如果网上有过这道题并且有更好的做法，那么请谅解。

# 题目：
对于任意的满足$f(0),f(1),f(2),...,f(n)\in\mathbb{Z}$的$n$次多项式$f(x)$，求证：$\forall t\in\mathbb{Z},f(t)\in\mathbb{Z}$
# 解法：
使用数学归纳法。

设命题$P(k)$为"对于任意的满足$f(0),f(1),f(2),...,f(k)\in\mathbb{Z}$的$k$次多项式$f(x)$，$\forall t\in\mathbb{Z},f(t)\in\mathbb{Z}$"

## 证明$P(0)$：
显而易见。（任意一个零次多项式都是平行于$x$轴的，如果有一个y值是整数，那所有的y值就都是整数了）

## 假设$P(k-1)$，证明$P(k)$：
**使用反证法**。若有一个$k$次多项式$f(x)$满足$f(0),f(1),f(2),...,f(k)\in\mathbb{Z}$，但不满足$P(k)$，则考虑函数$g(x)=f(x+1)-f(x)$。

这个函数是一个$k-1$次多项式（展开一下$f(x+1)-f(x)$的$k$次项，发现它被抵消了）。

然后$\because f(0),f(1)\in\mathbb{Z}\therefore g(0)\in\mathbb{Z}$，$\because f(1),f(2)\in\mathbb{Z}\therefore g(1)\in\mathbb{Z}$ …… $\because f(k-1),f(k)\in\mathbb{Z}\therefore g(k-1)\in\mathbb{Z}$。所以$g(0),g(1),...,g(k-1)\in\mathbb{Z}$。而根据$P(k-1)$，则$\forall t\in\mathbb{Z},g(t)\in\mathbb{Z}$。

由$g(x)=f(x+1)-f(x)$，可得$g(x)+f(x)=f(x+1)$。因为$\forall t\in\mathbb{Z},g(t)\in\mathbb{Z}$，所以根据$f(k)\in\mathbb{Z}$递推可得$\forall t\in\mathbb{Z}且t>k,f(t)\in\mathbb{Z}$。

同理，$f(x)-g(x-1)=f(x-1)$。因为$\forall t\in\mathbb{Z},g(t)\in\mathbb{Z}$，所以根据$f(0)\in\mathbb{Z}$递推可得$\forall t\in\mathbb{Z}且t<0,f(t)\in\mathbb{Z}$。

但由$\forall t\in\mathbb{Z}且t<0,f(t)\in\mathbb{Z}$，$\forall t\in\mathbb{Z}且t>k,f(t)\in\mathbb{Z}$，$f(0),f(1),f(2),...,f(k)\in\mathbb{Z}$得$\forall t\in\mathbb{Z},f(t)\in\mathbb{Z}$，与假设矛盾。
