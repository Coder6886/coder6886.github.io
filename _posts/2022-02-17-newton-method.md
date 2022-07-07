---
layout:     post
title:      牛顿分形
subtitle:   
date:       2022-02-17
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    [ 数学 , python ]
---
今天看了一个很有意思的一个牛顿分形：

![newton-method-1.png](/img/newton-method-1.png)
我看到后，就想编一个代码，实现这个牛顿分形，代码如下（用的matplotlib的点阵）：
```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.pyplot import MultipleLocator
import cmath
def P(z):
    return z**3-1
def Pprime(z):
    return 3*z**2
def Z(lstval):
    if Pprime(lstval) != 0:
        return lstval - P(lstval)/Pprime(lstval)
    else:
        return lstval
def LenBetTP(a,b):
    return ((a.real-b.real)**2+(a.imag-b.imag)**2)**0.5
n_of_iter = 10#迭代次数

s1 = 1+0j
s2 = -0.5-0.866025j
s3 = -0.5+0.866025j
density = 20#点阵密度

for r in range(6*density):
    m = r / density - 3
    for t in range(6*density):
        k = t / density - 3
        ans = m+k*1j
        for h in range(n_of_iter):
            ans = Z(ans)
        l1 = LenBetTP(s1,ans)#r

        l2 = LenBetTP(s2,ans)#g

        l3 = LenBetTP(s3,ans)#b

        if min([l1,l2,l3]) == l1:
            plt.plot(m,k,'o',color = 'r')
            #print(1)
            
        elif min([l1,l2,l3]) == l2:
            plt.plot(m,k,'o',color = 'g')
        else:
            plt.plot(m,k,'o',color = 'b')

plt.plot(s1.real,s1.imag,'o',color='yellow')
plt.plot(s2.real,s2.imag,'o',color='yellow')
plt.plot(s3.real,s3.imag,'o',color='yellow')
plt.show()

```
效果：

![newton-method-2.png](/img/newton-method-2.png)

这个比较粗糙，算的也比较慢。

三个黄点是$P(z)=z^3-1$的三个解，分别是$1+0i$,$-0.5-0.866025i$,$-0.5+0.866025i$。

这三个解的颜色分别是红绿蓝。

这个虽然粗糙了一点，但和最上面的图长得也挺像的。

主体思路，先定义$P$和$P'$两个函数，再定义迭代函数

然后将整个平面分为很多个点，将每一个点的迭代值都算出来，并画出相应的颜色。

