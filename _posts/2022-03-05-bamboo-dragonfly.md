---
layout:     post
title:      支撑竹蜻蜓
subtitle:   
date:       2022-03-05
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学 
---
今天我出去玩的时候买到了一只竹蜻蜓：

![bamboo-dragonfly-fig-1.jpg](/img/bamboo-dragonfly-fig-1.jpg)

这只竹蜻蜓能立在它的嘴巴上

现在，我们就要来试一试算出它的重心

# 初始参数

我们可以先不考虑这只蜻蜓的嘴巴，只考虑翅膀和尾巴

## 蜻蜓的三视图：

侧视图：

![bamboo-dragonfly-fig-2](/img/bamboo-dragonfly-fig-2.jpg)

上视图：

![bamboo-dragonfly-fig-3](/img/bamboo-dragonfly-fig-3.jpg)

正视图：

![bamboo-dragonfly-fig-4](/img/bamboo-dragonfly-fig-4.jpg)

## 其他参数：

**$B$点是三维坐标原点**

将$AB$的长度定义为$1$

$C$的$x$值是$\frac{1}{2}$

$x$轴到$G$的距离是$\frac{\sqrt{3}}{6}$

# 重心

**计算三维重心的关键就在于把三维转换成三个一维**

**计算一维重心：大家必须看[这个](https://zhuanlan.zhihu.com/p/394196284)。不看的后果就是看不懂后面。**

## 计算$y$方向上的重心

这个最好算，根据对称性，重心必定在$x$轴上

## 计算$x$方向上的重心

首先，将蜻蜓投影到$xz$平面

我们可以在$xz$平面上画出蜻蜓在某一点$x$在$xz$投影上对应的长度$f(x)$：

![bamboo-dragonfly-fig-5](/img/bamboo-dragonfly-fig-5.jpg)

其中

$$
f(x) = \{^{k,x\leq0}_{nx+k,x>0}\}
$$

这里面，k是$AB$的宽度，n是**两个翅膀**在$xz$平面上的宽度加起来改变的速率，注意，是**两个翅膀**。

那么就可以计算重心了：

$$
重心的x值=\frac{\int^{\frac{1}{2}}_{-1}xf(x)dx}{\int^{\frac{1}{2}}_{-1}f(x)dx}=\frac{\int^{0}_{-1}kxdx+\int^{\frac{1}{2}}_{0}(nx^2+kx)dx}{\int^{0}_{-1}kdx+\int^{\frac{1}{2}}_{0}(nx+k)dx}
$$

$$
=\frac{[\frac{1}{2}kx^2]^{0}_{-1}+[\frac{1}{3}nx^3+\frac{1}{2}kx^2]^{\frac{1}{2}}_{0}}{[kx]^{0}_{-1}+[\frac{1}{2}nx^2+kx]^{\frac{1}{2}}_{0}}=\frac{-\frac{3}{8}k+\frac{1}{24}n}{\frac{3}{2}k+\frac{1}{8}n}=\frac{n-9k}{3n+36k}
$$

$$
=\frac{1}{3}-\frac{21k}{3n+36k}=\frac{1}{3}-\frac{7k}{n+12k}
$$

前面那个积分分子是质量乘力臂，分母是总质量。我还是建议大家看上面的知乎帖子

这就是阶段性成果

至于那个$n$和那个$k$怎么算，那是留给你们的任务。

## 计算$z$方向上的重心

只用知道$z$方向上的重心比直线$AB$低就可以了

# 总结：
从蜻蜓的嘴到点$B$的距离就是：

$$
\frac{1}{3}-\frac{7k}{n+12k}
$$
