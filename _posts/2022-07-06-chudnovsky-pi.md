---
layout:     post
title:      Python算π
subtitle:   楚德诺夫斯基算法
date:       2022-07-06
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
   [ 数学 , python ]
---
算$\pi$，一直是人类心中的一大目标。

今天，我就来用楚德诺夫斯基算法计算$\pi$。

先上公式：

$$

\frac{1}{\pi}=12\sum_{n=0}^{\infty}\frac{(-1)^n(6n)!(13591409+545140134n)}{(3n)!(n!)^3640320^{3n+\frac{3}{2}}}

$$

有点吓人……

没事。

让我们来操作一番。

# 去掉分数幂

先把$640320$的分数幂去掉。

$$

\frac{1}{\pi}=12\sum_{n=0}^{\infty}\frac{(-1)^n(6n)!(13591409+545140134n)}{(3n)!(n!)^3640320^{3n+\frac{3}{2}}}

$$

$$

=\frac{12}{640320\sqrt{640320}}\sum_{n=0}^{\infty}\frac{(-1)^n(6n)!(13591409+545140134n)}{(3n)!(n!)^3640320^{3n}}

$$

$$

=\frac{12}{426880\sqrt{10005}}\sum_{n=0}^{\infty}\frac{(-1)^n(6n)!(13591409+545140134n)}{(3n)!(n!)^3640320^{3n}}

$$

然后再来一通操作（这里的操作就是优化算法用的）：

# S，P，Q，B，T

假如说我们定义一个和S：

$$

S(m,n) = \frac{a_mp_m}{b_mq_m}+\frac{a_{m+1}p_mp_{m+1}}{b_{m+1}q_mq_{m+1}}+\frac{a_{m+2}p_mp_{m+1}p_{m+2}}{b_{m+2}q_mq_{m+1}q_{m+2}}+...+\frac{a_{n-1}p_mp_{m+1}...p_{n-1}}{b_{n-1}q_mq_{m+1}...q_{n-1}}

$$

也就是

$$

S(m,n)=\sum_{k=m}^{n}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})

$$

$a_k,b_k,p_k,q_k$是什么先不用管。

再定义几个函数：

$$

P(m,n)=\prod_{k=a}^{b-1}p_k

$$

$$

Q(m,n)=\prod_{k=a}^{b-1}q_k

$$

$$

B(m,n)=\prod_{k=a}^{b-1}b_k

$$

$$

T(m,n)=B(m,n)Q(m,n)S(m,n)

$$

# 数列性质

然后说一下它们的性质

$$

P(m,n) = P(m,l)P(l,n)\quad(m\leq l\leq n)

$$

$$

Q(m,n) = Q(m,l)Q(l,n)\quad(m\leq l\leq n)

$$

$$

B(m,n) = B(m,l)Q(l,n)\quad(m\leq l\leq n)

$$

这三个性质是显而易见的。

第四个性质需要证明：

$$

T(m,n) = B(l,n)Q(l,n)T(m,l)+B(m,l)Q(m,l)T(l,n)\quad(m\leq l\leq n)

$$

证明如下:

$$

B(l,n)Q(l,n)T(m,l)+B(m,l)Q(m,l)T(l,n)

$$

$$

=B(l,n)Q(l,n)B(m,l)Q(m,l)S(m,l)+B(m,l)Q(m,l)B(l,n)Q(l,n)S(l,n)

$$

$$

=B(m,n)Q(m,n)S(m,l)+B(m,n)P(m,l)Q(l,n)S(l,n)

$$

$$

=B(m,n)(Q(m,n)S(m,l)+P(m,l)Q(l,n)S(l,n))

$$

$$

=B(m,n)(Q(m,n)S(m,l)+\frac{Q(m,n)}{Q(m,l)}P(m,l)S(l,n))

$$

$$

=B(m,n)Q(m,n)\biggl(S(m,l)+\frac{P(m,l)}{Q(m,l)}S(l,n)\biggr)

$$

$$

=B(m,n)Q(m,n)\biggl(\sum_{k=m}^{l-1}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})+\prod_{d=m}^{l-1}\frac{p_d}{q_d}*\sum_{k=l}^{n-1}(\frac{a_k}{b_k}\prod_{d=l}^{k}\frac{p_d}{q_d})\biggr)

$$

$$

=B(m,n)Q(m,n)\biggl(\sum_{k=m}^{l-1}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})+\sum_{k=l}^{n-1}(\frac{a_k}{b_k}\prod_{d=l}^{k}\frac{p_d}{q_d}*\prod_{d=m}^{l-1}\frac{p_d}{q_d})\biggr)

$$

$$

=B(m,n)Q(m,n)\biggl(\sum_{k=m}^{l-1}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})+\sum_{k=l}^{n-1}(\frac{a_k}{b_k}\prod_{d=m}^{k}\frac{p_d}{q_d})\biggr)

$$

$$

=B(m,n)Q(m,n)S(m,n)

$$

$$

=T(m,n)

$$

没看懂的话多看几遍。

# 最终的值

上面证明出了一些很有用的结论。

但它们有什么用呢？

我其实是可以给上面的$a_k,b_k,p_k和q_k$设值的。如果我这样：

$$

p_0=1

$$

$$

p_k = (6k-5)(2k-1)(6k-1)

$$

$$

q_0=1

$$

$$

q_k = k^3*640320^3/24

$$

$$

b_k = 1

$$

$$

a_k = (13591409+545140134k)

$$

用这些值用上面的性质就可以（二分）计算出任意的$T(m,n),P(m,n),Q(m,n),B(m,n)乃至于S(m,n)$。

代码：

```python
import math
from gmpy2 import mpz,iroot
from time import time

def pi_chudnovsky_bs(digits):
    C = 640320
    C3_OVER_24 = C**3 // 24
    def bs(m, n):
        if n - m == 1:
            if m == 0:
                Pmn = Qmn = mpz(1)
            else:
                Pmn = mpz((6*m-5)*(2*m-1)*(6*m-1))
                Qmn = mpz(m*m*m*C3_OVER_24)
            Tmn = Pmn * (13591409 + 545140134*m)
            if m & 1:
                Tmn = -Tmn
        else:
            l = (m + n) // 2
            Pml, Qml, Tml = bs(m, l)
            Pln, Qln, Tln = bs(l, n)
            Pmn = Pml * Pln
            Qmn = Qml * Qln
            Tmn = Qln * Tml + Pml * Tln
        return Pmn, Qmn, Tmn
    DIGITS_PER_TERM = math.log10(C3_OVER_24/6/2/6)
    N = int(digits/DIGITS_PER_TERM + 1)
    P, Q, T = bs(0, N)
    one_squared = mpz(10)**(2*digits)
    sqrtC = iroot(10005*one_squared,2)[0]
    return (Q*426880*sqrtC) // T
if __name__ == "__main__":
    digits=int(input("digits:"))
    start = time()
    f = open("pi.txt","w")
    pi = pi_chudnovsky_bs(digits)
    f.write(str(pi))
    f.close()
    print("time used:{}".format(time()-start))
```
没错，代码就这么短。

来看看时间

|位数|时间（s）|
|  ----  | ----  |
|1 | $\approx 0$ |
|10 | $\approx 0$ |
|100| $\approx 0$|
|1000| 0.001|
|10000|0.002|
|100000|0.03|
|1000000|0.59|
|10000000|11.3|
|100000000|132|

表现还是不错的。

好像比大多数专门计算$\pi$的软件要快。