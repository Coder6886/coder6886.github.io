---
layout:     post
title:      一个（圆）锥体的体积证明
subtitle:   
date:       2022-02-07
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---

# 锥体体积证明

## 以正方形为底的锥体的面积证明

**首先明确两点：**

**第一.当高不变时，锥体的体积和底成正比**

**第二.当底不变时，椎体的体积和高成正比**

**这两点就是后续证明的必要条件**

现在开始证明

**1.** 首先，创造一个正方体，确定正方体中心点O，并将其连向周围8个顶点。如图一：

![](/img/a-cone's-volume-fig-1.jpg)


点O和在一个面上的四个顶点组成的锥体的体积是正方体体积的$\frac{1}{6}$。

**2.** 拉长这个正方体，将其变为一个长方体，如图二：

![](/img/a-cone's-volume-fig-2.jpg)

锥体OABCD的高从$a$变成$b$，扩大了$\frac{b}{a}$倍。

锥体OABEF的底从$a^2$变成了$ab$，也扩大了$\frac{b}{a}$倍。

所以，$V_{锥体OABCD}=V_{锥体OABEF}$

同理，其他锥体的体积也都相等。

因为一共有六个锥体，

所以


$$

V_{锥体OABCD}=\frac{1}{6}V_{长方形}=\frac{1}{6}a^2b,

$$




$$

V_{锥体EABCD}=2V_{锥体OABCD}=\frac{2}{6}{a^2b}= \frac{1}{3}{a^2b}

$$





## 后续步骤

$a^2$ 是锥体EABCD的底面积$S$，$b$是那个锥体的高$h$，所以

$$

V_{锥体EABCD}=\frac{1}{3}{Sh}

$$

**根据 [祖暅原理](https://baike.baidu.com/item/%E7%A5%96%E6%9A%85%E5%8E%9F%E7%90%86/5165170)，任何底面积等于S的锥体都可以转化为一个底面为正方形的锥体，并用上述公式计算体积，所以：**

$$

V_{任意锥体}=\frac{1}{3}{Sh}

$$

证毕
