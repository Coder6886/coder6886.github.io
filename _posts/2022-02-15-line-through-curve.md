---
layout:     post
title:      直杆+曲线孔幻觉
subtitle:   
date:       2022-02-15
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学 
---
**我看了一个[知乎专栏](https://zhuanlan.zhihu.com/p/60033934)，里面有一些视觉错觉，我看到第四条“直杆+曲线孔幻觉”时，发现它是用数学计算算出来的，所以来了兴趣。那我就开始说一说这个曲线的公式是什么吧。**
## 题目

![line-through-curve-0](/img/line-through-curve-0.gif)

求白色板子上的线的公式
# 解
## 我们要求的就是点$A$在$xOy$平面上的轨迹。
### 首先，我们先分析第一种种情况：
![line-through-curve-1](/img/line-through-curve-1.png)

**假设$OF$为1，$OC$为$m$，$\frac{AB}{BC}$也就是直线$CE$的斜率为$k$**
假设$\angle BOF=\omega$。
$\angle OFB=90^\circ$
那么我们现在要用$\omega$表示出$OB$和$AB$
$$

OB=\frac{1}{\cos(\omega)}

$$
$$

AB=k\times BC=k\times (CF+FB)=k\times (\sqrt{m^2-1}+\tan(\omega))

$$
那么，点$O$就是坐标轴原点，$OB$就是$x$。
$$

\tan(\omega)=\frac{\sin(\omega)}{\cos(\omega)}=\frac{\frac{\sqrt{x^2-1}}{x}}{\frac{1}{x}}=\sqrt{x^2-1}

$$
所以，
$$

f(x)=k(\sqrt{m^2-1}+\sqrt{x^2-1})

$$
这是一个双曲线
没想到吧？
如果看懂了的话，并能联想到另一种情况的话，可以直接[跳到文末](#end)
没联想出来的话……
### 其次，我们再分析第二种情况：
![line-through-curve-2](/img/line-through-curve-2.png)

**假设$OF$为1，$OC$为$m$，$\frac{AB}{BC}$也就是直线$CE$的斜率为$k$**
假设$\angle BOF=\omega$。
$\angle OFB=90^\circ$
那么我们现在要用$\omega$表示出$OB$和$AB$
$$

OB=\frac{1}{\cos(\omega)}

$$
$$

AB=k\times BC=k\times (CF-FB)=k\times (\sqrt{m^2-1}-\tan(\omega))

$$
那么，点$O$就是坐标轴原点，$OB$就是$x$。
$$

\tan(\omega)=\frac{\sin(\omega)}{\cos(\omega)}=\frac{\frac{\sqrt{x^2-1}}{x}}{\frac{1}{x}}=\sqrt{x^2-1}

$$
所以，
$$

g(x)=k(\sqrt{m^2-1}-\sqrt{x^2-1})

$$
这还是一个双曲线
# 文末
<div id="end"></div>
我们已经得到了两个式子，分别是：
$$

f(x)=k(\sqrt{m^2-1}+\sqrt{x^2-1})

$$
和
$$

g(x)=k(\sqrt{m^2-1}-\sqrt{x^2-1})

$$
将这两个式子画出来，范围是$0\le x \le m$，得到的就是：

![line-through-curve-3](/img/line-through-curve-3.png)
这是当$m=5$,$k=1$时的曲线

大家可以试着3D打印一个模型

完工