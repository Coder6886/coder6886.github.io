---
layout:     post
title:      hammington code
subtitle:   
date:       2022-02-25
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    [ 数学 , python ]
---
今天我看了大V[3Blue1Brown](https://www.youtube.com/c/3blue1brown)的视频[Hammington codes part 1](https://www.youtube.com/watch?v=X8jsijhllIA&list=PLZHQObOWTQDN52m7Y21ePrTbvXkPaWVSg&index=19)和[Hammington codes part 2](https://www.youtube.com/watch?v=b3NxrZOu_CE&list=PLZHQObOWTQDN52m7Y21ePrTbvXkPaWVSg&index=20)， 看了思路就想写代码：
```python
class information_block:
    def __init__(self):
        self.size = 2
        self.info = [0]
    def write(self,bitarray):
        cnt = 0
        for i in range(1,(2**(self.size))**2):
            if i & (i-1) != 0:
                self.info.append(bitarray[cnt])
                cnt+=1
            else:
                self.info.append(0)
        for i in range(1,(2**(self.size))**2):
            if i & (i-1) != 0 and self.info[i] == 1:
                for j in range(2**(self.size)):
                    self.info[((i >> j) & 1) << j] ^= 1
    def receive(self,bitarray):
        self.info = bitarray
    def mark(self):
        res = 0
        for i in range(len(self.info)):
            if self.info[i] == 1:
               res ^= i
        return res
    def correct(self):
        place = self.mark()
        if place > 0:
            self.info[self.mark()] ^= 1
blk = information_block()
blk.write([1,0,1,0,0,1,0,1,0,0,1])
blk.info[9] ^= 1
print(blk.info)
print(blk.mark())
blk.correct()
print(blk.info)
```
我没有使用那个第0个比特（那样太麻烦），但是剩下的都差不多