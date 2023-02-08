---
layout:     post
title:      2022年我做完的最后一道数学题
subtitle:   这是我的一个小发现
date:       2023-01-09
author:     coder6886
header-img: img/post-bg-island.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
# 2023.01.09
今天抽空写一下2022年我做完的最后一道数学题。

这道题是我自己编的，如果网上有过这道题并且有更好的做法，那么请谅解。

# 问题：
对于任意的$n$次多项式$f(x)$，若满足$f(0),f(1),f(2),...,f(n)\in\mathbb{Z}$，求证：$\forall t\in\mathbb{Z},f(t)\in\mathbb{Z}$

# 解法：
使用数学归纳法。

设命题$P(k)$为"对于任意的$k$次多项式$f(x)$，若满足$f(0),f(1),f(2),...,f(k)\in\mathbb{Z}$，$\forall t\in\mathbb{Z},f(t)\in\mathbb{Z}$"

## 证明$P(0)$成立：
显而易见。（任意一个零次多项式都是平行于$x$轴的，如果有一个y值是整数，那所有的y值就都是整数了）

## 假设$P(k-1)$成立，证明$P(k)$也成立：
假设$P(k-1)$成立。对于任意一个满足$f(0),f(1),f(2),...,f(k)\in\mathbb{Z}$的$k$次多项式$f(x)$，考虑函数$g(x)=f(x+1)-f(x)$。

这个函数是一个$k-1$次多项式（展开一下$f(x+1)-f(x)$的$k$次项，发现它被抵消了）。

然后$\because f(0),f(1)\in\mathbb{Z}\therefore g(0)\in\mathbb{Z}$，$\because f(1),f(2)\in\mathbb{Z}\therefore g(1)\in\mathbb{Z}$ …… $\because f(k-1),f(k)\in\mathbb{Z}\therefore g(k-1)\in\mathbb{Z}$。所以$g(0),g(1),...,g(k-1)\in\mathbb{Z}$。而根据$P(k-1)$，则$\forall t\in\mathbb{Z},g(t)\in\mathbb{Z}$。

由$g(x)=f(x+1)-f(x)$，可得$g(x)+f(x)=f(x+1)$。因为$\forall t\in\mathbb{Z},g(t)\in\mathbb{Z}$，所以根据$f(k)\in\mathbb{Z}$递推可得$\forall t\in\mathbb{Z}且t>k,f(t)\in\mathbb{Z}$。

同理，$f(x)-g(x-1)=f(x-1)$。因为$\forall t\in\mathbb{Z},g(t)\in\mathbb{Z}$，所以根据$f(0)\in\mathbb{Z}$递推可得$\forall t\in\mathbb{Z}且t<0,f(t)\in\mathbb{Z}$。

由题设，$\forall t\in\mathbb{Z}且0\leq t\leq k,f(t)\in\mathbb{Z}$

综上所述，$\forall t\in\mathbb{Z},f(t)\in\mathbb{Z}$，$P(k)$成立，命题得证。■

# 2023.2.7更新

大家看完上面的证明，有没有想过：如果

$$

f(x)=\frac{p_n}{q_n}x^n+\frac{p_{n-1}}{q_{n-1}}x^{n-1}+...+\frac{p_1}{q_1}x+\frac{p_0}{q_0}\quad(p_k,q_k)=1,p_k,q_k\in\mathbb{Z},k\in\mathbb{Z}

$$

且$f(t)\in\mathbb{Z}(t\in\mathbb{Z})$

那么$q_k$的最大值是多少？

# 问题

对于任意的$n$次多项式$f(x)$，满足$f(t)\in\mathbb{Z}(t\in\mathbb{Z})$，且

$$

f(x)=\frac{p_n}{q_n}x^n+\frac{p_{n-1}}{q_{n-1}}x^{n-1}+...+\frac{p_1}{q_1}x+\frac{p_0}{q_0}\quad(p_k,q_k)=1,p_k,q_k\in\mathbb{Z},(k\in\mathbb{Z})

$$

则$q_k$的最大值为$n!$

# 解法：

一方面，$C_x^n=\frac{x(x-1)(x-2)...(x-n+1)}{n!}$在所有整数$x$上为整数（它在0,1,2,...,n-1上为0，在n上为1，所以根据刚才证明的定理，可以知道$C_x^n$在所有整数$x$上都为整数），且它的$x^n$项为$\frac{1}{n!}$，所以$q_k=n!$可以取到。

另一方面，设$g^k_f(x)=g^{k-1}_f(x+1)-g^{k-1}_f(x)(k>0)$，且$g_f^0(x)=f(x)$，可以知道$g_n$为常函数。



## 引理1

$g^k_{cf}=cg^k_f$，其中c为一常数。这个显而易见。

## 引理2

$g^k_{f+h}=g^k_f+g^k_h$，其中$f$和$h$为任意函数。

## 引理2证明

引理2对于$k=0$时成立。

当$k>0$，用数学归纳法，设引理2对于$k-1$成立。

$$

g^k_{f+h}(x)=g^{k-1}_{f+h}(x+1)-g^{k-1}_{f+h}(x)

$$

$$

=g^{k-1}_f(x+1)+g^{k-1}_h(x+1)-g^{k-1}_f(x)-g^{k-1}_h(x)

$$

$$

=g^{k-1}_f(x+1)-g^{k-1}_f(x)+g^{k-1}_h(x+1)-g^{k-1}_h(x)

$$

$$

=g^k_f+g^k_h

$$

引理2对于k成立。

## 引理3

如果有两个函数$f$和$h$，且$\forall 0\leq k\leq n,g_f^k=g_{h}^k$则$f(x)=h(x)$

## 引理3证明

我们知道所有$g^k_f(0)\,(0\leq k\leq n)$，那我们就知道了$g^n_f$（它是常函数），那我们就可以根据 

$$

g^{k-1}_f(x)=g^k_f(x-1)+g^{k-1}_f(x-1)

$$

递推出所有$g_k$，也就能唯一确定$f$。然而 $\forall 0\leq k\leq n,g_f^k=g_{h}^k$，所以$g_f^k$同样可以确定函数$h$。所以$f(x)$必然等于$h(x)$。

## 最后证明

现在我们设$w(x)=C_x^l$，可知$g^k_w(0)=0(0\leq k<l),g^l_w=1$ （这是一个简单计算，用到了$w(0)=0,w(1)=0,..w(l-1)=0,w(l)=1$ ）

设$h(x)=g_f^0(0)C_x^0+g_f^1(0)C^1_x+...+g^n_f(0)C^n_x$，则因为

$$

g_{h}^k(0)=g^0_f(0)\times 0+g_f^1(0)\times0+..+g_f^{k-1}(0)\times 0+g_f^k(0)\times1+g_f^{k+1}(0)\times0+...+g_f^n(0)\times0\quad(引理1)

$$

$$

=g^k_f（引理2）

$$

所以$h(x)=f(x)$（引理3）

然而$g^k_f$都是整数（显而易见），所以$q_k$最大为$C_x^l$的分母的最大值，也就是$n!$。命题得证■

