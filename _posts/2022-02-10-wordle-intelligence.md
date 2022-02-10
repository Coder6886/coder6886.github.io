---
layout:     post
title:      wordle 智能解
subtitle:   
date:       2022-02-10
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学 - python
---

前几天看了[这个微信链接](https://mp.weixin.qq.com/s/iddHGL4IaibPq_A59efuyg)，看到了大V[3Blue1Brown](https://www.youtube.com/channel/UCYO_jab_esuFRV4b17AJtAw)的视频，觉得想写一个这样的代码。
## 第一个版本：
```python
import os
import math
last_gets = []
last_result = []
possible_words = []
all_words = []
p_file = open("possible_words.txt",'r')
line = p_file.readline()
while line:
    possible_words.append(line[:5])
    line = p_file.readline()
p_file.close()
a_file = open("allowed_words.txt",'r')
line1 = a_file.readline()
while line1:
    all_words.append(line1[:5])
    line1 = a_file.readline()
a_file.close()
lstnumbers = [[[]for i in range(3**5)]for i in range(len(possible_words))]
nowentropy = math.log(len(possible_words),2)
answer = "pause"
def wordle(p,ans):
    global last_result
    if last_gets[-1] not in all_words:
        print("word not valid")
        last_gets.pop()
        return
    if not p:
        last_result = []
    for i in range(5):
        if last_gets[-1][i] == ans[i]:
            if p:
                print("0",end="")
            else:
                last_result.append(0)
        elif last_gets[-1][i] in ans:
            if p:
                print("1",end="")
            else:
                last_result.append(1)
        else:
            if p:
                print("2",end="")
            else:
                last_result.append(2)
    if p:
        print()
    if last_gets[-1] == ans:
        if p:
            print("Good job! You've got it right in "+str(len(last_gets))+" run/runs! Please press Ctrl+C")
while True:
    print(nowentropy)
    entropymax = 0
    best_word = -1
    best_k = -1
    for i in range(len(possible_words)):
        if i % 100 == 0:
            print (i)
        informationEntropy = 0
        last_gets.append(possible_words[i])
        for j in possible_words:
            wordle(False,j)
            lstnumbers[i][last_result[0]*3**4+last_result[1]*3**3+last_result[2]*3**2+last_result[3]*3**1+last_result[4]].append(j)
        last_gets.pop()
        for k in range(3**5):
            p = len(lstnumbers[i][k])/len(possible_words)
            if p > 0:
                informationEntropy += p*math.log(1/p,2)
        if entropymax < informationEntropy:
            entropymax = informationEntropy
            best_word = i
            best_k = k
    print(possible_words[best_word])
    nowin = input(">")
    last_gets.append(nowin)
    wordle(True,answer)
    wordle(False,answer)
    statenumber = last_result[0]*3**4+last_result[1]*3**3+last_result[2]*3**2+last_result[3]*3**1+last_result[4]
    p = len(lstnumbers[possible_words.index(nowin)][statenumber])/len(possible_words)
    nowentropy -= math.log(1/p,2)
    possible_words = lstnumbers[best_word][statenumber]
    lstnumbers = [[[]for i in range(3**5)]for i in range(len(possible_words))]
```
我并没有像3Blue1Brown那样“加大难度”，而是只采用了那2315个答案数据。这里边，我重写了wordle游戏，答案就是那个`answer="pause"`,大家可以自己试一试，有什么问题，欢迎提出。