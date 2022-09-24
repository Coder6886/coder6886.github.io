---
layout:     post
title:      AcWing143-最大异或对
subtitle:   
date:       2021-10-22
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing , c++ , NOIP ]
---

## 题目

[题目传送门](https://www.acwing.com/problem/content/description/145/)

## 代码

```c++
#include<bits/stdc++.h>

using namespace std;
int a[100010*31][2];
int b[100010];
int tt;
void insert(int n){
    int now = 0;
    for(int i = 30; i >= 0; i--){
        int k = (n >> i) & 1;
        if(!a[now][k])a[now][k] = tt++;
        now = a[now][k];
    }
}
int main(){
    tt++;
    int n;
    cin >> n;
    int ans = 0;
    for(int i = 0; i < n; i++){
        cin >> b[i];
        insert(b[i]);
    }
    for(int i =0; i < n; i++){
        int k = b[i];
        int now = 0;
        int nval = 0;
        for(int j = 30; j >= 0; j--){
            if((k >> j) & 1 && a[now][0] || !a[now][1] && a[now][0]){
                now = a[now][0];
            }
            else if(!((k >> j) & 1) && a[now][1] || !a[now][0] && a[now][1]){
                now = a[now][1];
                nval+=(1 << j);
            }
            else{
                break;
            }
        }
        ans = max(ans,nval^k);
    }
    cout << ans << endl;
    return 0;
}

```

