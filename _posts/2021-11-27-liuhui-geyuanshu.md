---
layout:     post
title:      割圆术
subtitle:   
date:       2021-11-27
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - 数学
---
## 割圆术

```python
n = int(input("input the number of iterations:"))
k = 6*(3**0.5)/4
l = 1
for i in range(n):
    k = l * 3*(2**(i+1))/2
    l = ((1-(1-(l/2)**2)**0.5)**2+(l/2)**2)**0.5
print(k)
```

原理请看[维基百科](https://zh.wikipedia.org/wiki/%E5%89%B2%E5%9C%86%E6%9C%AF_(%E5%88%98%E5%BE%BD))

