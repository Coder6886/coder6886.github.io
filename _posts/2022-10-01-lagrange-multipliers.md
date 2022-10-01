---
layout:     post
title:      拉格朗日乘数法
subtitle:   
date:       2022-10-01
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
# **🎉🎉首先，祝大家国庆快乐！祝伟大的祖国生日快乐！🎉🎉**

# 今天我们的主题是**拉格朗日乘数法**

这是一个十分厉害的法子。

若有一函数$f(x_1,x_2,...,x_n)$，而且有一约束条件$g(x_1,x_2,...,x_n)=c$，则：

$$

\nabla f=\lambda\nabla g,g=c

$$

的解为$f$在$g$的约束下的极值。

其中的$\lambda$就是为了纪念拉格朗日大叔（$Lagrange$的第一个字母是$l$，在希腊文里是$\lambda$）。

# 证明：
在以下的证明中，我将用3维空间的一些名词来比喻一些形状。“曲面”的意思就是一个$n-1$维的物体。“曲线”的意思就是一个$n-2$维的物体。

假设$f$在$g=c$这个“平面”上的极值点为$P$。

设$\mathbf{r}(t)=\begin{pmatrix} x_1(t) \\ x_2(t) \\...\\ x_n(t) \end{pmatrix}$为$g=c$这个“曲面”上任意一条“曲线”，且$r(0)=P$。再让$h(t)=f(x_1(t),x_2(t),...,x_n(t))$。

可以知道

$$

h'(t)=\nabla f\big|_{\mathbf{r}(t)}\cdot \mathbf{r'}(t)

$$

上边用的是$Chain\,rule$的矢量写法。

知道了上一步，那就知道

$$

h'(0)=\nabla f\big|_{P}\cdot \mathbf{r'}(0)=0

$$

第一个等号是直接将0带入上一个式子，第二个等号是因为点P是极值点，所以$h'(0)$是0。

既然$\nabla f\big|_{P}\cdot \mathbf{r'}(0)=0$,也就意味着$\nabla f\big|_{P}$和$\mathbf{r'}(0)$互相垂直，也就意味着$\nabla f\big|_{P}$与任意一条在$g=c$上的“曲线”垂直。这也就意味着$\nabla f\big|_{P}$与$g=c$这个“曲面”垂直。而我们又知道$\nabla g\big|_{P}$也与$g=c$垂直，所以我们知道$\nabla f\big|_{P}$和$\nabla g\big|_{P}$平行。

根据$\nabla f\big|_{P}$和$\nabla g\big|_{P}$平行，可以列出方程求解点P：

$$

\nabla f=\lambda\nabla g,g=c

$$
证毕。

# 例题（这是一道四川省初中竞赛题）
## 设实数$x,y,z$满足$x^2+y^2+z^2-xy-yz-zx=27$，则$|y-z|$的最大值为？
### 正解：

答：6。

将原等式整理为关于$x$的一元二次方程$x^2-(y+z)x+y^2+z^2-yz-27=0$,$\Delta=(y+z)^2-4(y^2+z^2-yz-27)\geq0$，得$(y-z)^2\leq36$，$|y-z|\leq6$。

**简直了，看着让人眼花缭乱。**

### 我的解释：

答：6。

将原式整理为$(x-y)^2+(y-z)^2+(z-x)^2=54$

设$x-y=a,y-z=b,z-x=-a-b$。

则$a^2+b^2+ab=27$是约束条件，$b$是需要求最大值的那个函数。

列出方程组（我就直接把偏微分算出来了，这个偏微分很容易）：

$$

\begin{cases} 0=\lambda (2a+b)\\ 1=\lambda (2b+a)\\ a^2+b^2+ab=27\end{cases} 

$$

$$

\because0=\lambda(2a+b)

$$

$$

\therefore b=-2a

$$

$$

\therefore a^2+(-2a)^2+a(-2a)=27

$$

$$

\therefore 3a^2=27,a=3,b=6

$$

**我是觉得这个比较简单，思路也挺清晰**

各位可以在评论区投票：

## **赞同方法1简单的打1，赞同方法2简单的打2**