---
layout:     post
title:      关于费马点的位置的证明
subtitle:   
date:       2022-05-23
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
今天我们来看看费马点的位置的证明。

首先，是

# 题目

有一$\triangle ABC$，在三角形内部（包括三个边和三个顶点）有一点$P$。

如果使$PA+PB+PC$最小，$P$应该放在哪里？

# 结论

## 在$\triangle ABC$中最大的角小于$120^\circ$时：

应该使$\angle APB=\angle BPC=\angle CPA=120^\circ$。
## 在$\triangle ABC$中最大的角大于等于$120^\circ$时：

假设那个角是$\angle A$，应该使点$P$与点$A$重合。

# 证明

我有一个geogebra文件，可以在[这里](https://github.com/Coder6886/coder6886.github.io/blob/master/word_files/fermat-point.ggb)下载，大家可以拖动一下点A，拖动一下点P，看看会发生什么。

然后就可以开始证明了

![fermat-point-fig1](/img/fermat-point-fig1.png)

以$AB$为边做等边三角形$\triangle ABD$，再以$AP$为边做等边三角形$\triangle APE$。

$\because \angle PAB+\angle DAB=\angle DAE+\angle EAF$

$\therefore \angle PAB+60^\circ=\angle DAE+60^\circ$

$\therefore \angle PAB=\angle DAE$

$\because AB=AD,AP=AE,\angle PAB=\angle DAE$

$\therefore \triangle ABP \cong \triangle ADE (根据边角边SAS)$

$\because PA=PE,PB=DE$

$\therefore PA+PB+PC=DE+EP+PC$

由于点D和点C是定点，所以最好情况是$DE,EP,PC$共线。

想让他们三条线共线，只需要$\angle DEA=\angle APC = 120^\circ$。

$\because \triangle ABP \cong \triangle ADE$

$\therefore \angle BPA=120^\circ$

$\therefore \angle BPA=\angle APC=\angle BPC=120^\circ$。

如果$\triangle ABC$中最大的角($\angle A$)小于$120^\circ$，这样的在$\triangle ABC$内部的点$P$就存在。

**但是如果$\angle A\geq120^\circ$**：

![fermat-point-fig2](/img/fermat-point-fig2.png)

延长$DA$与$EC$交于点$F$。

对于任意的点$P$来说：

$$

DE+EP+PC\geq DE+EC=DE+EF+FC\geq DF+FC=DA+AF+FC\geq DA+AC

$$

当且仅当点$P$与点$A$重合时，上式的所有等号成立。

证毕。