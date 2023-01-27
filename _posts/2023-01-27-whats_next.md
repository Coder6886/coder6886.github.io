---
layout:     post
title:      一劳永逸——找规律
subtitle:   What's Next?
date:       2023-01-27
author:     coder6886
header-img: img/post-bg-island.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---

估计很多人上学时代都被一个问题困扰着：

$$

1,1,2,3,5,8,...

$$

这个数列我们非常熟悉。“兔子数列”，也称Fibonacci数列的规律是$F_n=F_{n-1}+F_{n-2}$

假如有一个人将$1,1,2,3,5,8$给你，然后问你“这个数列中的下一个数是什么？What's next??”

好吧，你知道这个数列的规律。那如果再换一个，你还能知道规律吗？

今天我们就来一劳永逸地解决这个问题。

# 数学部分

## 第一部分：判断
还是拿兔子数列做例子。毕竟今年是兔年😊

我们把这个数列写很多次（要错开写）：

$$

1\quad1\quad2\quad3\quad5\quad8\qquad\qquad\\
\quad1\quad1\quad2\quad3\quad5\quad8\qquad\\
\quad\quad1\quad1\quad2\quad3\quad5\quad8\\
...

$$

我以后就把这一堆错开了的数列叫做“数表”

设置一个计数器k从1开始

在上面的数表中随机选择一个$k\times k$的矩阵，比如

$$

\left[
    \begin{matrix}
    1
    \end{matrix}
\right]

$$

计算它的行列式，发现不是0，所以计数器加一。

再选择一个$k\times k$的矩阵：

$$

\left[
    \begin{matrix}
    1\quad2\\
    1\quad1\\
    \end{matrix}
\right]

$$

再计算行列式，发现还不是零，那计数器再加一。

再选择一个$k\times k$的矩阵：

$$

\left[
    \begin{matrix}
    2\quad3\quad5\\
    1\quad2\quad3\\
    1\quad1\quad2\\
    \end{matrix}
\right]

$$

这回它的行列式是0了。这意味着什么呢？

这其实意味着矩阵的三行中有一行可以表示为其他两行的组合。

想一下我们构造这个数表时这些不同的行都有什么含义。

数表的第一行的第n个数是$F_n$

第一行第n个数正下方的第二行的数是$F_{n-1}$

第一行第n个数下方两个数是$F_{n-2}$

就以n=4为例

$$

1\quad1\quad2\quad F_{n\quad}\quad5\quad8\qquad\qquad\\
\quad1\quad1\quad F_{n-1}\quad3\quad5\quad8\qquad\\
\quad\quad1\quad F_{n-2}\quad2\quad3\quad5\quad8\\
...

$$

那么我们最后的矩阵行列式为零，其实就在对我们传达一个信息：

$$

F_n=x_1F_{n-1}+x_2F_{n-2}+...+x_{k-1}F_{n-k+1}

$$

对于兔子数列来说，它传达的信息就是$F_n=x_1F_{n-1}+x_2F_{n-2}$

其中$x_i$都是下一部分要求的系数。

如果所有这样的$k\times k$矩阵行列式都是0的话，我们就找到了规律。

## 第二部分：计算

上面不是选了一个$k\times k$的矩阵吗？将它的最后一列去掉:

原来的矩阵：
$$

\left[
    \begin{matrix}
    2\quad3\quad5\\
    1\quad2\quad3\\
    1\quad1\quad2\\
    \end{matrix}
\right]

$$

现在的矩阵：

$$

A=\left[
    \begin{matrix}
    2\quad3\\
    1\quad2\\
    1\quad1\\
    \end{matrix}
\right]

$$

设B为A的第一行：

$$

B=\left[\begin{matrix}2\quad3\end{matrix}\right]

$$

再将A的第一行去掉：

$$

A=\left[
    \begin{matrix}
    1\quad2\\
    1\quad1\\
    \end{matrix}
\right]

$$

还记得上面的那些系数$x_i$吗？

设

$$

X=\left[
    \begin{matrix}
    x_1\\
    x_2\\
    ...\\
    x_{k-1}
    \end{matrix}
\right]

$$

那我们可以列出方程$A^TX=B^T$

也就是

$$

F_n=x_1F_{n-1}+x_2F_{n-2}+...+x_{k-1}F_{n-k+1},\\
F_{n+1}=x_1F_n+x_2F_{n-1}+...+x_{k-1}F_{n-k+2}\\
...

$$

解这个方程，就可以得到所有的系数啦！

例如兔子数列：

$$

\left[
    \begin{matrix}
    1\quad1\\
    2\quad1\\
    \end{matrix}
\right]X=
\left[
    \begin{matrix}
    2\\
    3
    \end{matrix}
\right]

$$

就可以解出

$$

X=\left[\begin{matrix}1\\1\end{matrix}\right]

$$

也就是$F_n=F_{n-1}+F_{n-2}$

大功告成！！

# 实操

其实实际操作的时候不需要验证所有$k\times k$的矩阵行列式都为0，只需要验证左上角在第一行上的所有矩阵就可以了。

代码：

```python
```