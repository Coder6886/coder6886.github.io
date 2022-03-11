---
layout:     post
title:      fourier变换（分析函数）
subtitle:   
date:       2022-03-06
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - python 
---
我现在可以用我的程序分析一个函数$g(x)$
代码：
```python
## https://kaizhao.net/blog/fourier 
## 相位就是arctan(-bn/an)
import numpy as np
from numpy import pi
import matplotlib.pyplot as plt
delta = 0.01
greaterZeroPlace = 0.1
def g(t):
    return 1.0*np.cos(2*pi*t*1+2)-2*np.sin(2*pi*t*2)-3*np.cos(2*pi*t*3)+5*np.sin(2*pi*t*5)
def compute_center(t1,t2,freq):
    t = t1
    integ = 0.0
    while t<t2:
        integ += 2*delta*g(t)*np.e**(-2*pi*freq*t*1j)
        t+=delta
    return integ/(t2-t1)
def plot_graph(t1,t2,freq1,freq2):
    fig,ax = plt.subplots(2)
    fig.suptitle("fourier transform of g")
    x1 = []
    y1 = []
    x2 = []
    y2 = []
    x3 = []
    y3 = []
    freq = freq1;
    while freq <= freq2:
        z = compute_center(t1,t2,freq)
        x1.append(freq)
        y1.append(z.real)
        x2.append(freq)
        y2.append(-z.imag)
        x3.append(freq)
        if abs(z.real - 0) > greaterZeroPlace and abs(-z.imag) > greaterZeroPlace:
            y3.append(np.arctan(-z.imag/z.real))
        elif abs(z.real - 0) < greaterZeroPlace and abs(-z.imag) > greaterZeroPlace:
            if -z.imag > 0:
                y3.append(pi/2)
            else:
                y3.append(-pi/2)
        else:
            y3.append(0)
        freq += 0.1
    ax[0].plot(x1,y1,color = 'orange')
    ax[0].plot(x2,y2,color = 'r')
    ax[1].plot(x3,y3,color = 'b')
    plt.show()
plot_graph(0,20,0.1,6)

```
函数$g(x)$可以是任何函数，这个程序是将这个函数分解为几个$sin$和$cos$函数。
效果：

![fourier-transformation.jpg](/img/fourier-transformation.jpg)

其中橙线是$cos$波、红线是$sin$波、蓝线是相位。

大家可以试着改一下$g(x)$，看看这个函数会发生什么。