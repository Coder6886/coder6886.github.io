---
layout:     post
title:      AcWing125耍杂技的牛
subtitle:   
date:       2021-10-19
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing ,  NOIP ]
---

## 题目：

[题目传送门](https://www.acwing.com/problem/content/127/)

## 代码：

```c++
#include<bits/stdc++.h>

using namespace std;
pair<int,int> a[50010]; //first:wi+si, second:wi
int main(){
    int n;
    cin >> n;
    for(int i = 0; i < n; i++){
        int x;
        cin >> a[i].second >> x;
        a[i].first = x+a[i].second;
    }
    sort(a,a+n);
    long long res = -0x3f3f3f3f;
    long long tmp = 0;
    for(int i = 0; i < n; i++){
        res = max(res,tmp-a[i].first+a[i].second);
        tmp += a[i].second;
    }
    cout << res << endl;
    return 0;
}
```

