---
layout:     post
title:      让电脑画字符画
subtitle:   关于卷积Convolution的传奇
date:       2022-12-12
author:     coder6886
header-img: img/post-bg-island.jpg
catalog: true
usemathjax: true
tags:
    [python , 数学]
---

今天我要让我的电脑教我画字符画。


![draw-text-art-with-computer-fig1.png](/img/draw-text-art-with-computer-fig1.png)

这是今天要处理的图像（其实任意搞个漫画之类的东西放这里都可以，就是要稍微根据漫画的线条密度之类的调整一些参数）

先将效果呈上：

![draw-text-art-with-computer-fig2.png](/img/draw-text-art-with-computer-fig2.png)

不怎么样，但也还好吧。这个电脑是Win10的，到Win11上画面会扁一些，就基本跟原图的比例一样。

往里放大就会发现：

![draw-text-art-with-computer-fig3.png](/img/draw-text-art-with-computer-fig3.png)

这果然是字符画！全是由" ",".","*"和"@"组成的！

# 为什么我要选漫画

漫画的优点有：大片颜色，轮廓就能概括整个漫画，没有太多轮廓太过密集的区域和毛发，而且好找

缺点：漫画最出神的是眼睛，而眼睛往往是轮廓线最多的区域，所以控制不好的话眼睛效果很糟糕。

## 过程中一些可调节的参数大家要按照文本编辑器的设定和个人喜好更改

# 卷积Convolution
卷积是Convolution的中文版本，查询时用中文的“卷积”查询，但我再下文将持续使用“Convolution”表示卷积。和卷积一样，“互相关”操作我将使用英文Cross-Correlation来表示。

Convolution是一个十分神奇的东西，在卷积神经网络（Convolutional Neural Networks），图像处理（今天的重点）等各种东西里都会出现。

Convolution的符号是$*$，一个六角星。但要说清楚Convolution，得先从$\star$,五角星，也叫Cross-Correlation（互相关）说起。

## 明细概念（懂的直接跳过）：

### Cross-Correlation
有一小矩阵K(Kernal)

有一大矩阵A

#### 举例：
假如K为

$$
    \left[
    \begin{matrix}
     1 & 2\\
    -1 & 0
    \end{matrix}
    \right]
$$

，并且A为

$$
    \left[
    \begin{matrix}
     1 & 6 & 2\\
     5 & 3 & 1\\
     7 & 0 & 4
    \end{matrix}
    \right]
$$

想象一个和K大小一样的方框划过A:

$$
    \left[
    \begin{matrix}
    \left[\begin{matrix}1 & 6\\ 5& 3\end{matrix}\right]
    \begin{matrix}
     2\\
     1\\
    \end{matrix}\\
    \begin{matrix}
     7 & 0 & 4
    \end{matrix}
    \end{matrix}
    \right]
$$

将这个方框里每个数和K里面对应的每个数相乘，再将所有的乘积相加，也就是这样：

$$

1\times1+6\times2+5\times(-1)+3\times0=8

$$

将这个8填入一个结果矩阵B内：

$$
    \left[
    \begin{matrix}
     8 & \quad\\
     \quad & \quad
    \end{matrix}
    \right]
$$

重复上述操作


$$
    \left[
    \begin{matrix}
    \begin{matrix} 1\\ 5\end{matrix}
    &\left[
    \begin{matrix}
    6&2\\
    3&1
    \end{matrix}
    \right]\\
    7&
    \begin{matrix}
    0&4
    \end{matrix}
    \end{matrix}
    \right]
$$

$$

6\times1+2\times2+3\times(-1)+4\times0=7

$$

$$
    \left[
    \begin{matrix}
     8 & 7\\
     \quad & \quad
    \end{matrix}
    \right]
$$

...（过程不表）...

直到将这个结果B填完：

$$
    \left[
    \begin{matrix}
     8 & 7\\
     4 & 5
    \end{matrix}
    \right]
$$

则我们称

$$

A\star K=B

$$

这也就是Cross-Correlation。

对于一切的A和K也是这个道理：

**<u>1.将和K大小一样的矩阵划过A**

**2.按元素求乘积（Hadamard Product$\odot$）**

**3.将结果放到一个结果矩阵里。</u>**

### Convolution

$$

A*K=A\star rot180(K)

$$

其中rot180会将原来的K

$$
    \left[
    \begin{matrix}
     1 & 2\\
    -1 & 0
    \end{matrix}
    \right]
$$

旋转180度：

$$
    \left[
    \begin{matrix}
     0 &-1\\
     2 & 1
    \end{matrix}
    \right]
$$

顺时针逆时针都一样。

那其实上面的那个公式就代表了一切。

那既生瑜何生亮呢？原因是：Cross-Correlation在图像处理上更直观，而Convolution在函数和多项式乘法还有概率上意义更为明显。所以他们俩各有优劣。

# 大致思路

1.将原图检测边缘（Convolution）

2.加一个滤镜（将小于滤值的过滤掉，并且将剩余的结果分成三档，"."档，"*"档和"@"档）

3.写文件

这里面的大致成型（重工活）都是第一条，精益求精（调节参数）都在第二条，而第三条就是“打酱油的”（呈现结果）

# 具体实施

先上代码（看注释！看注释！看注释！）

```python
import numpy as np
from numpy import pi
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
from scipy import signal
def rgb2gray(rgb):# 顾名思义，将原图转换成灰度图像

    return np.dot(rgb[...,:3], [0.2989, 0.5870, 0.1140])
img = mpimg.imread('image.png')
gray = rgb2gray(img)
kernal1 = np.array([[-1,-1,-1],\
                   [ 0, 0, 0],\
                   [ 1, 1, 1]])
kernal2 = np.array([[-1, 0, 1],\
                   [ -1, 0, 1],\
                   [ -1, 0, 1]])#这两个Kernel的直观解释一会说

result1= signal.convolve2d(gray,kernal1,mode="valid")
result2= signal.convolve2d(gray,kernal2,mode="valid")#这两行就是重工，Convolution

endres = np.maximum(abs(result1)+abs(result2)-0.1,0)#第一个滤镜，0.1以下的都会被过滤掉

#写文件

f = open("drawing.txt",'w')
for i in range(np.shape(endres)[0]):
    for j in range(np.shape(endres)[1]):
        if endres[i][j]>0 and endres[i][j]<=0.3:
            f.write('.')#第二个滤镜，0.3,刨去0.1后坚持不到0.3的都归位"."档

        elif endres[i][j] > 0.3 and endres[i][j] <= 1:
            f.write('*')#第三个滤镜，1,刨去0.1后坚持到0.3的，但是还没有努力到1的都归位"*"档

        elif endres[i][j] > 1:
            f.write('@')#恭喜！坚持到了最后！成为了光荣的"@"档

        else:
            f.write(' ')#好吧，这边都是些空格

    f.write('\n')
f.close()
#底下这两行就是在Matplotlib里画出最终结果（不带滤镜）

plt.imshow(np.amax(endres)-endres, cmap=plt.get_cmap('gray'), vmin=0, vmax=np.amax(endres))
plt.show()

```
至于那两个K，现在我来解释一下。

还是从Convolution回到Cross-Correlation。

那第一个就是

$$
    \left[
    \begin{matrix}
     1 & 1 & 1\\
     0 & 0 & 0\\
    -1 &-1 &-1
    \end{matrix}
    \right]
$$

第二个是

$$
    \left[
    \begin{matrix}
     1 & 0 &-1\\
     1 & 0 &-1\\
     1 & 0 &-1
    \end{matrix}
    \right]
$$

第一个能检测横着的边缘，第二个能检测竖着的。

我就以第一个为例，解释为什么这个能检测边缘。

假如说第一个Kernal就在一个横着的边缘，那两边的颜色会不一样。不妨说下面的颜色数值小，上面的数值大。那当K滑动到边缘上时那三个-1就抵不过三个1的力量，所以Convolution操作后结果里这个边缘上会出现一个较大的正值。如果下面的颜色数值大而上面的数值小，那Convolution操作后结果里这个边缘上就会出现一个较大的负值。

那如果第一个Kernal不在横着的边缘上，那基本上这些1和-1就会互相抵消（差不多抵消），所以Convolution操作后结果里只会剩一个绝对值很小的数。

类似的，第二个Kernal可以检测竖着的边缘。

# 这个程序如何用

搞一个大小差不多为(300~600)x400的图（最好不要有太多毛茸茸的东西，而且有色块，就例如这个漫画），将它保存在程序的目录下，并且改名为"image.png"。

运行这个程序，程序会弹出一个预览框，且程序目录下会出现"drawing.txt"

打开"drawing.txt"

用一个文本编辑器打开drawing.txt，并将大小缩到适当大小（基本上就是最小）。

**<u>切记切记，如果显示异常，不要埋怨程序，需要调整文本编辑器的字体（最好调成“Lucida Console”），再重新打开就好了</u>**

如果觉得线条数量不合适，就调一下各种参数。可以自己摸索一下。