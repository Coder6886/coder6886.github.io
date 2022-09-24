---
layout:     post
title:      AcWing797-差分
subtitle:   
date:       2021-10-21
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing , c++ , NOIP ]
---

## 题目

[题目传送门](https://www.acwing.com/problem/content/799/)

## 代码

```c++
#include<bits/stdc++.h>

using namespace std;
int a[100010];
void insert(int i, int j, int c){
    a[i] += c;
    a[j+1] -= c;
}
int main(){
    int n,m;
    cin >> n >> m;
    for(int i =0; i < n; i++){
        int tmp;
        cin >> tmp;
        insert(i,i,tmp);
    }
    while(m--){
        int a,b,c;
        cin >> a >> b >> c;
        insert(a-1,b-1,c);
    }
    int s = 0;
    for(int i = 0; i < n; i++){
        s += a[i];
        cout << s << ' ';
    }
    cout << endl;
    return 0;
}
```

