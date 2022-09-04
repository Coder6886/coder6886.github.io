---
layout:     post
title:      二体问题的解
subtitle:   
date:       2022-09-04
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---

# 二体问题：

![two-body-problem-fig1](/img/two-body-problem-fig1.gif)

在宇宙中，有且仅有两个天体，它们都有一定的初速度，初始位置。

现在它们受到引力作用互相吸引，问它们的移动轨迹是什么？

# 结果推导

首先，我们可以把这两个天体看做一个整体，由牛顿第一定律，这个质心不受外力作用，所以可以有两种情况：

1.质心不动

2.质心匀速直线运动

这两种情况我们都可以放心的把坐标系原点设在质心上（我们知道质心的初始速度，而质心匀速直线运动）

**以后的计算坐标原点都在质心上**

由于只有两个天体，所以质心和这两个天体三点一线。

所以

$$

\frac{\|\vec{\colorbox{red}{S}}\|}{\|\vec{\colorbox{orange}{s}}\|}=\frac{\colorbox{orange}{m}}{\colorbox{red}{M}}\ ① 

$$

红色天体对橙色天体施加的力是：

$$

F=G\frac{\colorbox{red}{M}\colorbox{orange}{m}}{\|\vec{\colorbox{red}{S}}-\vec{\colorbox{orange}{s}}\|^2}

$$

假设坐标原点有一个**虚拟天体**。

虚拟天体的质量是：

$$

\colorbox{LightBlue}{M} =\frac{\colorbox{red}{M}}{(1+\frac{\colorbox{orange}{m}}{\colorbox{red}{M}})^2}

$$

使红色天体消失一段时间，让我们来算一算虚拟天体对橙色天体施加的力:

$$

F=G\frac{\colorbox{LightBlue}{M}\colorbox{orange}{m}}{\|\vec{\colorbox{orange}{s}}\|^2}

$$

$$

=G\frac{\frac{\colorbox{red}{M}}{(1+\frac{\colorbox{orange}{m}}{\colorbox{red}{M}})^2}\colorbox{orange}{m}}{\|\vec{\colorbox{orange}{s}}\|^2}

$$

$$

=G\frac{\colorbox{red}{M}\colorbox{orange}{m}}{(1+\frac{\colorbox{orange}{m}}{\colorbox{red}{M}})^2\|\vec{\colorbox{orange}{s}}\|^2}

$$

$$

=G\frac{\colorbox{red}{M}\colorbox{orange}{m}}{(\|\vec{\colorbox{orange}{s}}\|+\frac{\colorbox{orange}{m}}{\colorbox{red}{M}}\|\vec{\colorbox{orange}{s}}\|)^2}

$$

由于 ① 可得：

$$

上式=G\frac{\colorbox{red}{M}\colorbox{orange}{m}}{(\|\vec{\colorbox{orange}{s}}\|+\|\vec{\colorbox{red}{S}}\|)^2}

$$

又由于$\vec{\colorbox{orange}{s}}$与$\vec{\colorbox{red}{S}}$方向相反，可得

$$

上式=G\frac{\colorbox{red}{M}\colorbox{orange}{m}}{\|\vec{\colorbox{red}{S}}-\vec{\colorbox{orange}{s}}\|^2}

$$

我们突然发现虚拟天体对橙色天体的作用力**等于**红色天体对橙色天体的作用力，又由于力的方向一致，所以这可以看做橙色天体围绕质量为$\colorbox{LightBlue}{M} =\frac{\colorbox{red}{M}}{(1+\frac{\colorbox{orange}{m}}{\colorbox{red}{M}})^2}$的一个虚拟天体做[单体运动](https://blog6886.iantzy.online/2022/03/15/orbit/)。

同样的，红色天体也可以看做绕着另一个（也在坐标原点上）的虚拟天体做[单体运动](https://blog6886.iantzy.online/2022/03/15/orbit/)。这个过程我就不推导了，但红色天体对应的那个虚拟天体的质量是$\colorbox{LightGreen}{M} =\frac{\colorbox{orange}{m}}{(1+\frac{\colorbox{red}{M}}{\colorbox{orange}{m}})^2}$

这样，一个二体问题就转化为了两个单体运动。

关于单体运动的我的博客在[这里](https://blog6886.iantzy.online/2022/03/15/orbit/)。