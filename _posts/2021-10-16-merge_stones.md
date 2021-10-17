---
layout:     post
title:      AcWing282石子合并
subtitle:   
date:       2021-10-16
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing ,  NOIP ]
---

## 题目：

[题目传送门](https://www.acwing.com/problem/content/284/)

## 代码：

```c++
#include<bits/stdc++.h>

using namespace std;
int f[305][305];
int a[305], s[305];
int dp(int st, int ed){
    if(st > ed)return f[st][ed];
    if(st == ed)return f[st][ed] = 0;
    if(f[st][ed] != 0x3f3f3f3f)return f[st][ed];
    int sum = s[ed]-s[st-1];
    for(int i = st; i < ed; i++){
        f[st][ed] = min(f[st][ed],dp(st,i)+dp(i+1,ed)+sum);
    }
    return f[st][ed];
}
int main(){
    memset(f,0x3f,sizeof f);
    int n;
    cin >> n;
    for(int i = 0; i < n; i++)cin >> a[i];
    s[0] = a[0];
    for(int i = 1; i < n; i++)s[i] = s[i-1]+a[i];
    cout << dp(0,n-1) << endl;
    return 0;
}
```

