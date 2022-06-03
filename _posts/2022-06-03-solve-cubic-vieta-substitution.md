---
layout:     post
title:      求解一元三次方程（韦达替换）
subtitle:   
date:       2022-06-03
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
今天我就来讲一讲一元三次方程我个人最喜欢的解法

# 第一部分——配方

首先有一个一元三次方程：

$$

ax^3+bx^2+cx+d=0

$$

我们可以将这个方程整理为

$$

x^3+\frac{b}{a}x^2+\frac{c}{a}x+\frac{d}{a}=0

$$

还可以将此方程整理为：

$$

x^3+3(\frac{b}{3a})x^2=-\frac{c}{a}x-\frac{d}{a}

$$

将左边和右边同时加上$3(\frac{b}{3a})^2x$和$(\frac{b}{3a})^3$可将左边配成完全立方：

$$

(x+\frac{b}{3a})^3=[3(\frac{b}{3a})^2-\frac{c}{a}]x+[(\frac{b}{3a})^3-\frac{d}{a}]

$$

$$

(x+\frac{b}{3a})^3=[\frac{b^2}{3a^2}-\frac{c}{a}]x+[\frac{b^3}{27a^3}-\frac{d}{a}]

$$

$$

(x+\frac{b}{3a})^3=\frac{b^2-3ac}{3a^2}x+\frac{b^3-27a^2d}{27a^3}

$$

可以化简右边的式子：

$$

(x+\frac{b}{3a})^3=\frac{b^2-3ac}{3a^2}\frac{b}{3a}-\frac{b^2-3ac}{3a^2}\frac{b}{3a}+\frac{b^2-3ac}{3a^2}x+\frac{b^3-27a^2d}{27a^3}

$$

$$

(x+\frac{b}{3a})^3=\frac{b^2-3ac}{3a^2}(x+\frac{b}{3a})+\frac{b^3-27a^2d}{27a^3}-\frac{b^2-3ac}{3a^2}\frac{b}{3a}

$$

$$

(x+\frac{b}{3a})^3=\frac{b^2-3ac}{3a^2}(x+\frac{b}{3a})+\frac{b^3-27a^2d}{27a^3}-\frac{b^3-3abc}{9a^3}

$$

$$

(x+\frac{b}{3a})^3=\frac{b^2-3ac}{3a^2}(x+\frac{b}{3a})+\frac{-2b^3-27a^2d+9abc}{27a^3}

$$

将右边的式子挪回左边，可得

$$

(x+\frac{b}{3a})^3+\frac{3ac-b^2}{3a^2}(x+\frac{b}{3a})+\frac{2b^3+27a^2d-9abc}{27a^3}=0

$$

令$t=x+\frac{b}{3a},p=\frac{3ac-b^2}{3a^2},q=\frac{2b^3+27a^2d-9abc}{27a^3}$，方程可以化简为：

$$

t^3+pt+q=0

$$

# 第二部分——韦达替换

令$t=w-\frac{p}{3w}$，带入$t^3+pt+q=0$可得：

$$

(w-\frac{p}{3w})^3+p(w-\frac{p}{3w})+q=0

$$

展开后可得：

$$

w^3-{p}w+\frac{p^2}{3w}-\frac{p^3}{27w^3}+pw-\frac{p^2}{3w}+q=0

$$

$$

w^3-\frac{p^3}{27w^3}+q=0

$$

此时，只要找到一个$w$，将它分别乘以$\zeta^3=1$的三个解（将$\zeta_1$定义为$-\frac{1}{2}+\frac{\sqrt3}{2}i$，这三个解可以分别表示为$\zeta_1^0,\zeta_1^1,\zeta_1^2$），就可以得到所有的$w^3-\frac{p^3}{27w^3}+q=0$的三个解（不信把$\zeta_1^1w$和$\zeta_1^2w$带入试一试）。

如果我把$w^3-\frac{p^3}{27w^3}+q=0$两边同时乘以$w^3$，可得：

$$

w^6+qw^3-\frac{p^3}{27}=0

$$

将$w^3$作为一个变量求解上面的方程（将$w^3$作为一个变量后上面的方程可以变成一元二次方程）可得：

$$

w^3=-\frac{q}{2}\pm\sqrt{\frac{q^2}{4}+\frac{p^3}{27}},w=\sqrt[3]{-\frac{q}{2}\pm\sqrt{\frac{q^2}{4}+\frac{p^3}{27}}}

$$

取$w$的一个值，分别将其乘$\zeta_1^0,\zeta_1^1,\zeta_1^2$，可以得到$w$的所有解。

将$w$的解带入$t=w+\frac{p}{3w}$可以得到$t$的所有解

再将$t$的解带入$t=x+\frac{b}{3a}$，可以得到$x$的所有解。