---
layout:     post
title:      turtle-谢尔宾斯基三角
subtitle:   
date:       2022-05-12
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - python
---
前几天看见了谢尔宾斯基三角能由一个L-系统生成。

那个L-系统是什么我就不详细说了，只说意思。

1.首先，有一个指令串`s="A"`

2.把`s`中所有的`A`都替换成`B-A-B`,**同时**把`s`中所有的`B`都替换成`A+B+A` **注意，这是同时替换。不存在先后顺序。这里的+和-不是加减号，这两个都是字符。**

3.重复执行`2.`n次。

4.最后解析`s`

是如何解析的呢？

`A`和`B`都是`前进`的意思

`+`和`-`分别是`右转60°`和`左转60°`的意思

然后最后就是

5.执行解析后的指令

代码：
```python
from turtle import *
#这就是步骤2

def iterate_triangle(s):
    ans = ""
    for i in s:
        if i == "A":
            ans += "B-A-B"
        elif i == "B":
            ans += "A+B+A"
        else:
            ans += i
    return ans
#这是s

instructions = "A"
#这是迭代次数

iterations = 8
for i in range(iterations):
    instructions=iterate_triangle(instructions)
penup()
shape("turtle")
#这是初始位置（不知道为什么谢尔宾斯基三角形总是颠倒过来）

setpos(-300,300*((-1)**iterations))
#这是走一步的步长

steplen = 2**(9-iterations)
setheading(0)
pendown()
#这是步骤3和步骤4

for i in instructions:
    if i == "A" or i == "B":
        forward(steplen)
    elif i == "+":
        right(60)
    else:
        left(60)

```
效果：

5次迭代：

![sierpinski-triangle-turtle-5-iter.png](/img/sierpinski-triangle-turtle-5-iter.png)

6次迭代：

![sierpinski-triangle-turtle-6-iter.png](/img/sierpinski-triangle-turtle-6-iter.png)

最多是九次迭代

这个turtle是有动画的，大家可以自己欣赏（其实挺好看的）