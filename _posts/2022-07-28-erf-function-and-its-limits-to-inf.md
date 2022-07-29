---
layout:     post
title:      erf函数再无穷大处的值
subtitle:   还有生活中的一个小鼓包
date:       2022-07-28
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
嗯……这个事从何说起呢？

先说一个函数。

这个函数很普通。

它是：$e^{-x^2}$

再说这篇的主题：$erf$函数

意思就是标准差函数。

定义：

$$

erf(x)=\frac{2}{\sqrt{\pi}}\int_0^xe^{-t^2}dt

$$

中间就出现了$e^{-x^2}$这个函数。其实这个函数非常重要，它和正太分布函数有着千丝万缕的关系。

$erf$函数的定义前面为什么要带一个$\frac{2}{\sqrt{\pi}}$呢？因为人们喜欢1这个数字（比如扔硬币，扔到正面和反面的概率加起来是1，扔骰子扔到1-6的概率和也是1），所以人们设定：

$$

\lim_{x\rightarrow\infty}erf(x)=1（下将简写为erf(\infty)=1）

$$

那就说明

$$

\int_0^xe^{-t^2}dt=\frac{\sqrt{\pi}}{2}

$$

那人们凭什么知道这个是真的呢？

我们今天就来证明它是真的，也就顺带证明了$erf(\infty)=1$。

中间也许你会不明白为什么要做某一部，但是最后我会汇总的。不要急。

# 第一步：预设

首先，

$$

\frac{erf(\infty)}{\frac{2}{\sqrt{\pi}}}=\int_0^{\infty}e^{-t^2}dt

$$

我们定义：

$$

\int_0^{\infty}e^{-t^2}dt=Q

$$

# 第二部：求一个体积

![erf-function-and-its-limits-to-inf-fig1](/img/erf-function-and-its-limits-to-inf-fig1.png)

注意三个轴的方向。

我定义y轴是朝上的，x轴是横纵的，z轴是前后的。

我们现在的当务之急就是求出蓝色曲面在xz平面上方的体积。

方法很简单。

![erf-function-and-its-limits-to-inf-fig2](/img/erf-function-and-its-limits-to-inf-fig2.png)

将这一个面积极小的长方形以y轴为中心旋转成一个“圆筒”：

![erf-function-and-its-limits-to-inf-fig3](/img/erf-function-and-its-limits-to-inf-fig3.png)

当dx趋近于0时，这个圆筒也就相当于一片薄纸。将这个薄纸展开铺平，就可以得到它的体积是$2\pi xe^{-x^2}dx$。前面的$2\pi x$是薄纸的长，$dx$是纸的厚度，$e^{-x^2}$是纸的高。

将上面那个式子积分一下，可以得到：

$$

\int2\pi xe^{-x^2}dx

$$

定义

$$

u=-x^2,du=-2x

$$

原式就变成了

$$

\int-\pi e^udu=-\pi\int e^udu=-\pi e^u=-\pi e^{-x^2}

$$

然后，

$$

\int_0^\infty 2\pi xe^{-x^2}dx=-\pi e^{-x^2}\bigg\vert_0^\infty=0-(-\pi)=\pi

$$

所以，

$$

\int_0^\infty 2\pi xe^{-x^2}dx=\pi

$$

# 第三部分：换种方法求相同的面积

![erf-function-and-its-limits-to-inf-fig4](/img/erf-function-and-its-limits-to-inf-fig4.png)


显而易见，这个小鼓包的方程是$y=e^{-r^2}$，其中$r$是某一个在$xz$平面上的点$(x,z)$到$xz$平面上的原点的距离。

所以，这个小鼓包的方程就是（由勾股定理）：$y=e^{-(x^2+z^2)}$

我首先在$z=b$处将曲面截线（第二根黑线）的方程求出来。

![erf-function-and-its-limits-to-inf-fig5](/img/erf-function-and-its-limits-to-inf-fig5.png)

将b看作一个**常量**，积分$e^{-b^2}e^{-x^2}$:

$$

\int_{-\infty}^\infty e^{-b^2}e^{-x^2}dx=2\int_0^\infty e^{-b^2}e^{-x^2}dx=2e^{-b^2}\int_0^\infty e^{-x^2}dx=2e^{-b^2}Q

$$

这就相当于求出了在$z=b$处的曲面截线（上上图中的第二根黑线）底下的面积。

然后，如果我要求出那个小鼓包底下的体积，再把$2e^{-b^2}Q$积分一下（这时候，Q是那个常数，因为Q里只有定积分一个,b是那个变量，还记得吗？我们把一个$z$值赋值为b，所以b本质上就是z）。

$$

\int_{-\infty}^\infty2e^{-b^2}Qdb=\int_{-\infty}^\infty2e^{-z^2}Qdz=2Q\int_{-\infty}^\infty e^{-z^2}dz

$$

$$

=2*2*Q*\int_0^\infty e^{-z^2}dz=2*2*Q*Q=4Q^2

$$

# 第四部分：汇总

我们知道小鼓包下面的面积是$4Q^2$，也是$\pi$，所以$4Q^2=\pi$，可以推得$Q=\frac{\sqrt{\pi}}{2}$。

$$

erf(\infty)=\frac{\sqrt{\pi}}{2}\frac{2}{\sqrt{\pi}}=1

$$

大功告成！