---
layout:     post
title:      里面的圆，外面的圆
subtitle:   心脏线，三尖瓣线和它们美丽的近亲
date:       2022-06-25
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
前几天想起来了在维基百科上看到的一个动画：

![cardioids-deltoids-and-its-relatives-fig1](/img/cardioids-deltoids-and-its-relatives-fig1.gif)

这是一个圆沿着另一个和它半径相等的圆的外侧做无滑动滚动，取上面的一个定点画出的曲线（[心脏线](https://www.wikiwand.com/zh/%E5%BF%83%E8%84%8F%E7%BA%BF)）

还有另外一个动图：

![cardioids-deltoids-and-its-relatives-fig2](/img/cardioids-deltoids-and-its-relatives-fig2.gif)

这是一个圆沿着另一个半径是第一个圆半径的三倍的圆的内侧做无滑动滚动，取上面的一个定点画出的曲线（[三尖瓣线](https://www.wikiwand.com/zh-hans/%E4%B8%89%E5%B0%96%E7%93%A3%E7%BA%BF)）

这次我就要
1.定义心脏线和三尖瓣线的近亲
2.推导所有这些线（心脏线，三尖瓣线，还有他们的近亲）的公式（复坐标系），然后给大家我制作的动画
3.探究一些规律

# 1.定义心脏线和三尖瓣线的近亲

**三尖瓣线的近亲**：首先有一圆，半径为$r$，另有一圆，半径为1，在第一个圆的**内侧无滑动滚动**，有一在小圆上的定点，描出的轨迹就是三尖瓣线的一个近亲。

**心脏线的近亲**：首先有一圆，半径为$r$，另有一圆，半径为1，在第一个圆的**外侧无滑动滚动**，有一在小圆上的定点，描出的轨迹就是心脏线的一个近亲。

# 2.推导公式

## 2.1. 推导关于三尖瓣线的近亲的公式

假设这些图形都在复数平面内。

假设一开始小圆的圆心（$点C$）在实数轴上，那个在小圆上的定点（$点B$）也在实数轴上。

在大圆内侧无滑动滚动了一个角度$\omega$后，$点C$到了$点C'$，$点B$到了$点B'$。

由于$点B$是定点，而且是无滑动滚动，所以$\|\mathop{B'E}\limits^{\frown}\|=\|\mathop{BE}\limits^{\frown}\|$

![cardioids-deltoids-and-its-relatives-fig3](/img/cardioids-deltoids-and-its-relatives-fig3.png)

由于$\angle EAB=\omega（弧度）$，并且$AB=r$，所以$\|\mathop{BE}\limits^{\frown}\|=\omega r$，所以$\|\mathop{B'E}\limits^{\frown}\|=\omega r$，又由于$C'B'=1$，所以$\angle EC'B'=\frac{\omega r}{1}=\omega r$。

可以以$点C'$为原点建立另外一个复平面，在这个复平面上计算$点B'$的坐标再转换回以$点A$为原点的坐标。

在**以$点C'$为原点的坐标系上**$点E$的坐标是$1*e^{i\omega}=e^{i\omega}$（$点A$，$点C'$，$点E$三点一线），$点B'$的坐标是$点E$的坐标再顺时针旋转$\omega r$，也就是$点B'$的坐标是$点E$的坐标乘上$e^{-i\omega r}（顺时针，所以加负号）$，也就是$e^{i\omega}e^{-i\omega r}=e^{i(1-r)\omega}$

然后将$点B'$在**以$点C'$为原点的坐标**转换回**以$点A$为原点的坐标**。任何在**以$点C'$为原点的坐标系上**的点转换回**以$点A$为原点的坐标**只需要将原来的坐标加上**以$点A$为原点的$点C'$的坐标**。这些话有点拗口，大家仔细想一想。

所以可以将$点B'$在**以$点C'$为原点的坐标**（$e^{i(1-r)\omega}$）加上**以$点A$为原点的$点C'$的坐标**（$(r-1)e^{i\omega}$），所以$点B'$在**以$点A$为原点的坐标系上的坐标**就是$e^{i(1-r)\omega}+(r-1)e^{i\omega}$。

## 2.2. 推导关于心脏线的近亲的公式

如果上面的推导看懂了的话，下面其实也类似，就直接跳过就行了。

没看懂的话就继续看。

假设一开始小圆的圆心（$点C$）在实数轴上，那个在小圆上的定点（$点B$）也在实数轴上。

在大圆外侧无滑动滚动了一个角度$\omega$后，$点C$到了$点C'$，$点B$到了$点B'$。

由于$点B$是定点，而且是无滑动滚动，所以$\|\mathop{B'E}\limits^{\frown}\|=\|\mathop{BE}\limits^{\frown}\|$

![cardioids-deltoids-and-its-relatives-fig4](/img/cardioids-deltoids-and-its-relatives-fig4.png)

由于$\angle EAB=\omega（弧度）$，并且$AB=r$，所以$\|\mathop{BE}\limits^{\frown}\|=\omega r$，所以$\|\mathop{B'E}\limits^{\frown}\|=\omega r$，又由于$C'B'=1$，所以$\angle EC'B'=\frac{\omega r}{1}=\omega r$。

可以以$点C'$为原点建立另外一个复平面，在这个复平面上计算$点B'$的坐标再转换回以$点A$为原点的坐标。

在**以$点C'$为原点的坐标系上**$点E$的坐标是$1*e^{i(\pi+\omega)}=e^{i(\pi+\omega)}$（$点A$，$点C'$，$点E$三点一线），$点B'$的坐标是$点E$的坐标再逆时针旋转$\omega r$，也就是$点B'$的坐标是$点E$的坐标乘上$e^{i\omega r}（逆时针，所以不加负号）$，也就是$e^{i(\pi+\omega)}e^{i\omega r}=e^{i(\pi+(r+1)\omega)}$

然后将$点B'$在**以$点C'$为原点的坐标**转换回**以$点A$为原点的坐标**。任何在**以$点C'$为原点的坐标系上**的点转换回**以$点A$为原点的坐标**只需要将原来的坐标加上**以$点A$为原点的$点C'$的坐标**。这些话有点拗口，大家仔细想一想。

所以可以将$点B'$在**以$点C'$为原点的坐标**（$e^{i(\pi+(r+1)\omega)}$）加上**以$点A$为原点的$点C'$的坐标**（$(r+1)e^{i\omega}$），所以$点B'$在**以$点A$为原点的坐标系上的坐标**就是$e^{i(\pi+(r+1)\omega)}+(r+1)e^{i\omega}$。

## 2.3.动画

公式推导完了，还不放松一下？

我自己制作的动画在[这里](https://github.com/Coder6886/coder6886.github.io/blob/master/word_files/cardioids-deltoids-and-its-relatives.ggb)下载。

动画里的w就是$\omega$(omega)。

# 3.在动画中的美丽

当$r$是正整数时，图案就是这样的：

![cardioids-deltoids-and-its-relatives-fig5](/img/cardioids-deltoids-and-its-relatives-fig5.png)

可以看出，当小圆在大圆外面滚动时，一共有$r$个凸包；当小圆在大圆里面 滚动时，一共有$r$个凹陷。

当$r$是最简分数时（$\frac{p}{q}$），图案就是这样的：

![cardioids-deltoids-and-its-relatives-fig6](/img/cardioids-deltoids-and-its-relatives-fig6.png)

这里我的例子是$p=5,q=3$。

看一看$5$在这个图里的哪里体现。

中间是一个$5$角星。外面也是$5$重对称。

那$3$在哪里呢？

看里面，如果从五角星的一个角开始沿着蓝色的线再到一个角，就会跨过一个角。再算上起点和终点，就是$3$个角了！

![cardioids-deltoids-and-its-relatives-fig7](/img/cardioids-deltoids-and-its-relatives-fig7.png)

通过这个公式生成的心形线（$r=1$，小圆在外侧滚动，红线）:

![cardioids-deltoids-and-its-relatives-fig8](/img/cardioids-deltoids-and-its-relatives-fig8.png)

三尖瓣线（$r=3$，小圆在内侧滚动，蓝线）：

![cardioids-deltoids-and-its-relatives-fig9](/img/cardioids-deltoids-and-its-relatives-fig9.png)

好了，今天就先到这里了。$\|$