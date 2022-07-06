---
layout:     post
title:      Python算π
subtitle:   楚德诺夫斯基算法
date:       2022-07-06
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
   [ 数学 , python ]
---
算$\pi$，一直是人类心中的一大目标。

今天，我就来用楚德诺夫斯基算法计算$\pi$。

先上公式：

$$

\frac{1}{\pi}=12\sum_{n=0}^{\infty}\frac{(-1)^n(6n)!(13591409+545140134n)}{(3n)!(n!)^3640320^{3n+\frac{3}{2}}}

$$

有点吓人……

没事。

让我们来操作一番。

# 去掉分数幂

先把$640320$的分数幂去掉。

$$

\frac{1}{\pi}=12\sum_{n=0}^{\infty}\frac{(-1)^n(6n)!(13591409+545140134n)}{(3n)!(n!)^3640320^{3n+\frac{3}{2}}}

$$

$$

=\frac{12}{640320\sqrt{640320}}\sum_{n=0}^{\infty}\frac{(-1)^n(6n)!(13591409+545140134n)}{(3n)!(n!)^3640320^{3n}}

$$

$$

=\frac{12}{426880\sqrt{10005}}\sum_{n=0}^{\infty}\frac{(-1)^n(6n)!(13591409+545140134n)}{(3n)!(n!)^3640320^{3n}}

$$

然后再来一通操作（这里的操作就是优化算法用的）：

# S，P，Q，B，T

假如说我们定义一个和S：

$$

S(m,n) = \frac{a_mp_m}{b_mq_m}+\frac{a_{m+1}p_mp_{m+1}}{b_{m+1}q_mq_{m+1}}+\frac{a_{m+2}p_mp_{m+1}p_{m+2}}{b_{m+2}q_mq_{m+1}q_{m+2}}+...+\frac{a_{n-1}p_mp_{m+1}...p_{n-1}}{b_{n-1}q_mq_{m+1}...q_{n-1}}

$$

$a_k,b_k,p_k,q_k$是什么先不用管。

再定义几个函数：

$$

P(m,n)=\prod_{k=a}^{b-1}p_k

$$

$$

Q(m,n)=\prod_{k=a}^{b-1}q_k

$$

$$

B(m,n)=\prod_{k=a}^{b-1}b_k

$$

$$

T(m,n)=B(m,n)Q(m,n)S(m,n)

$$

# 数列性质

然后说一下它们的性质

$$

P(m,n) = P(m,l)P(l,n)\quad(m\leq l\leq n)

$$

$$

Q(m,n) = Q(m,l)Q(l,n)\quad(m\leq l\leq n)

$$

$$

B(m,n) = B(m,l)Q(l,n)\quad(m\leq l\leq n)

$$

这三个性质是显而易见的。

第四个性质需要证明：

$$

T(m,n) = B(l,n)Q(l,n)T(m,l)+B(m,l)Q(m,l)T(l,n)\quad(m\leq l\leq n)

$$

证明如下:

$$

B(l,n)Q(l,n)T(m,l)+B(m,l)Q(m,l)T(l,n)

$$

$$

=B(l,n)Q(l,n)B(m,l)Q(m,l)S(m,l)+B(m,l)Q(m,l)B(l,n)Q(l,n)S(l,n)

$$

$$

=B(m,n)Q(m,n)S(m,l)+B(m,n)P(m,l)Q(l,n)S(l,n)

$$

$$

=B(m,n)(Q(m,n)S(m,l)+P(m,l)Q(l,n)S(l,n))

$$

$$

=B(m,n)(Q(m,n)S(m,l)+\frac{Q(m,n)}{Q(m,l)}P(m,l)S(l,n))

$$

$$

=B(m,n)Q(m,n)\biggl(S(m,l)+\frac{P(m,l)}{Q(m,l)}S(l,n)\biggr)

$$

$$

=B(m,n)Q(m,n)\biggl(\sum_{k=m}^{l-1}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})+\prod_{d=m}^{l-1}\frac{p_d}{q_d}*\sum_{k=l}^{n-1}(\frac{a_k}{b_k}\prod_{d=l}^{k}\frac{p_d}{q_d})\biggr)

$$

$$

=B(m,n)Q(m,n)\biggl(\sum_{k=m}^{l-1}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})+\sum_{k=l}^{n-1}(\frac{a_k}{b_k}\prod_{d=l}^{k}\frac{p_d}{q_d}*\prod_{d=m}^{l-1}\frac{p_d}{q_d})\biggr)

$$

$$

=B(m,n)Q(m,n)\biggl(\sum_{k=m}^{l-1}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})+\sum_{k=l}^{n-1}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})\biggr)

$$

$$

=B(m,n)Q(m,n)S(m,n)

$$

$$

=T(m,n)

$$
