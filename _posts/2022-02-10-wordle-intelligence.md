---
layout:     post
title:      wordle智能解
subtitle:   
date:       2022-02-10
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    [ 数学 , python ]
---
## [wordle原版游戏地址](https://www.powerlanguage.co.uk/wordle/)

![](/img/2022-02-10-wordle-intelligence/2022-02-11-10-30-07.png)
## 前几天看了这个游戏，觉得想写一个这样的代码。
## 根据第一个版本做出的游戏机和解题机：
### 游戏机：
```python
import sys
import random
last_gets = []
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
ans = possible_words[random.randint(0,len(possible_words)-1)]
def wordle():
    if last_gets[-1] not in all_words:
        print("word not valid")
        last_gets.pop()
        return
    print("<",end = "")
    for i in range(5):
        if last_gets[-1][i] == ans[i]:
            print("O",end="")
        elif last_gets[-1][i] in ans:
            print("o",end="")
        else:
            print(" ",end="")
    print()
    if last_gets[-1] == ans:
        print("Good job! You've got it right in "+str(len(last_gets))+" run/runs! Please press Ctrl+C")
while True:
    try:
        nowin = input(">")
        last_gets.append(nowin)
        wordle()
    except KeyboardInterrupt:
        sys.exit(0)
```
### 解题机：
```python
import os
import math
import sys
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
print("Welcome to the wordle solver! Press Ctrl+C to quit!")
print("For the patterns in the game:")
print("A green square is 0")
print("A yellow square is 1")
print("A grey square is 2")
def wordle(ans):
    global last_result
    if last_gets[-1] not in all_words:
        print("word not valid")
        last_gets.pop()
        return
    last_result = []
    for i in range(5):
        if last_gets[-1][i] == ans[i]:
            last_result.append(0)
        elif last_gets[-1][i] in ans:
            last_result.append(1)
        else:
            last_result.append(2)
while True:
    try:
        print("Now, the current information entropy is "+str(nowentropy)+" bits.")
        entropymax = 0
        best_word = -1
        best_k = -1
        print("Calculating next step...")
        for i in range(len(possible_words)):
            if i % 100 == 0:
                print (i)
            informationEntropy = 0
            last_gets.append(possible_words[i])
            for j in possible_words:
                wordle(j)
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
        print("The best word is:"+possible_words[best_word])
        nowin = input("last input  :")
        pattern = input("last pattern:")
        last_gets.append(nowin)
        statenumber = int(pattern[0])*3**4+int(pattern[1])*3**3+int(pattern[2])*3**2+int(pattern[3])*3**1+int(pattern[4])
        p = len(lstnumbers[possible_words.index(nowin)][statenumber])/len(possible_words)
        nowentropy -= math.log(1/p,2)
        possible_words = lstnumbers[best_word][statenumber]
        lstnumbers = [[[]for i in range(3**5)]for i in range(len(possible_words))]
    except KeyboardInterrupt:
        print("Wordle solver done. Press any key to exit.")
        input()
        sys.exit(0)
```
allowed_words.txt:[allowed_words.txt](/word_files/wordle-intelligence-allowed_words.txt)


possible_words.txt:[possible_words.txt](/word_files/wordle-intelligence-possible_words.txt)

我并没有“加大难度”，而是只采用了那2315个答案数据。这里边，我重写了wordle游戏，答案是随机的，大家可以自己试一试，有什么问题，欢迎提出。