---
layout:     post
title:      AcWing104货仓选址
subtitle:   
date:       2021-10-19
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing , c++ , NOIP ]
---

## 题目：

[题目传送门](https://www.acwing.com/problem/content/106/)

## 代码：

```c++
#include<bits/stdc++.h>

using namespace std;
int a[100010];
int main(){
    int n;
    cin >>  n ;
    for(int i = 0;i < n; i++){
        cin >> a[i];
    }
    sort(a,a+n);
    int pos = a[n/2];
    long long res = 0;
    for(int i =  0; i < n; i++)res += abs(pos - a[i]);
    cout << res << endl;
    return 0;
}
```

