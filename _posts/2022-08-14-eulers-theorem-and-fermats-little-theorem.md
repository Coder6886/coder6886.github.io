---
layout:     post
title:      欧拉定理(数论)的证明
subtitle:   附带：费马小定理
date:       2022-08-14
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
# 必备知识

Q：欧拉定理是啥？

A：给你一个公式：

$$

如果gcd(n,a)=1,则a^{\varphi(n)}\equiv1(\bmod\ n)

$$

Q：那$\varphi(n)$是啥？

A：它是欧拉函数。

Q：那欧拉函数的值是多少？

A：$\varphi(n)=小于n并且和n互质的正整数的个数$

Q：有例子吗？

A：$\varphi(10)=4,因为小于10并且和10互质的正整数分别是1,3,7,9，有四个。$

好了，可以开始证明了。

# 开始证明

取所有小于n并且与n互质的正整数，将它们纳入一个集合$C$中。

$$

C = \{c_1,c_2,...,c_{\varphi(n)}\}

$$

显而易见，

$$

\prod_{i=1}^{\varphi(n)}c_i\equiv\prod_{i=1}^{\varphi(n)}ac_i(\bmod\ n)

$$

不那么显而易见？

好吧。

我们可以证明

1.$ac_i$模n的余数一定在集合$C$中，而且

2.没有两个$ac_i$和$ac_j$模n的余数相等。

为啥呢？

对于（1.），$gcd(n,a)=1,gcd(c_i,n)=1,所以gcd(ac_i,n)=1$。

对于（2.），如果有$ac_i\equiv ac_j(\bmod\ n)且i\neq j$，那么因为$gcd(n,a)=1$，所以同余式两边可以同时消去a，就变成了$c_i\equiv c_j(\bmod\ n)且i\neq j$。而这是不可能的，因为集合$C$中没有相同的数。

这样以后，相当于能把$C$和$aC$里面的元素一一对应，每一对元素模n的余数相同。

剩下的证明就好办多了。

$$

\prod_{i=1}^{\varphi(n)}c_i\equiv\prod_{i=1}^{\varphi(n)}ac_i\equiv a^{\varphi(n)}\prod^{\varphi(n)}_{i=1}c_i(\bmod\ n)

$$

又由于$gcd(c_i,n)=1$，所以(从两边消去$\prod_{i=1}^{\varphi(n)}c_i$)

$$

a^{\varphi(n)}\equiv1(\bmod\ n)

$$

这就是欧拉定理的证明。

至于费马小定理……

# 欧拉定理和费马小定理

费马小定理叙述：

$$

若a\nmid p,则a^{p-1}\equiv1(\bmod\ p)

$$

其实这是欧拉定理的一个特殊情况。

当欧拉定理中的n为质数时，$\varphi(n)=n-1$，小于n并且和n互质的正整数所有比n小的正整数。

在那种特殊情况下，欧拉定理就变成了费马小定理。