---
layout:     post
title:      关于圆锥曲线上向量轨迹的一个小结论
subtitle:   2024年唯一也是最后一篇文章
date:       2024-12-31
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
这篇文章是我在2024年写的唯一一篇文章。开始写于2024年12月31日 23:23。

# 圆

大家在做和圆有关的几何最值时一定遇到过这样一个类型的题：

![fig1](/img/on-locus-of-same-angle-vectors-on-conic-sections-fig1.png)

已知两个定圆，这两个圆各有一条半径在绕着圆心旋转，且这两条半径同步旋转（夹角不变）。请问半径外端两个点距离的最值是多少？

这道题如果想用初中方法想还不太容易，但是用向量来看就会简单太多。

![fig2](/img/on-locus-of-same-angle-vectors-on-conic-sections-fig2.png)

其实$\overrightarrow{D'D''}=\overrightarrow{DA'}+\overrightarrow{A'A''}+\overrightarrow{A''D''}=\overrightarrow{DA'}+\overrightarrow{A''D''}+\overrightarrow{A'A''}=\overrightarrow{DD'}+\overrightarrow{A'A''}$

然后$\overrightarrow{A'A''}$是定向量，$\overrightarrow{DD'}$是一个绕着定点动的向量，所以向量$\overrightarrow{D'D''}$的轨迹是个圆。

然后就好算了。

但是……
$\overrightarrow{DD'}$是一个绕着定点动的向量是不是有些蹊跷呢？

为啥呢？

对于圆来说，原因很简单，就是圆心角不变，向量长不变。

但是有圆，就一定有……

# 椭圆
椭圆有这个性质吗？

其实是有的，但得借助离心角的概念。

众所周知，椭圆的参数方程是$(acos\theta,bsin\theta)$。这个参数方程中的$\theta$就是所谓的离心角。那现在我们就提出一个猜测。

如果一个椭圆上有一个向量在滑动，且这个向量两端点离心角之差为定值，那此向量平移到原点后的轨迹也为一椭圆。

证明：设两个端点为$(acos(\theta+\phi),bsin(\theta+\phi))$,$(acos(\theta-\phi),bsin(\theta-\phi))$。则

$$

\vec v= (acos(\theta+\phi)-acos(\theta-\phi),bsin(\theta+\phi)-bsin(\theta-\phi))

$$

$$

=(-2asin\theta sin\phi,2bcos\theta sin\phi)

$$

这显然就是个椭圆（就是把上面的标准方程扩了倍并翻了一下）

想一想从几何直观上这也是正确的。

椭圆其实就是圆进行了拉伸。

我们其实是把原来在圆上转的那个向量硬拉到了椭圆上。

那它的轨迹本来是一个圆，后面被拉了一下不也变成了一个椭圆？

那圆完了，就该

# 双曲线
以上的命题对双曲线也是对的，但奇怪的是我只能通过强算平方差为1来验证它的轨迹真的是双曲线。

也就是说，得出的双曲线和原来的双曲线没有特别明显的几何变换的联系。

这是为什么我暂时也不清楚。也许从圆到双曲线的变换还没被我搞清楚。它也许是在复平面内的一个拉伸？

那今天先写到这里了。祝大家2025年快乐！