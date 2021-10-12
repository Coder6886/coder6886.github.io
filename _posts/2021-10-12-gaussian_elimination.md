---
layout:     post
title:      Gaussian_elimination
subtitle:   
date:       2021-10-12
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing , 洛谷 ,  NOIP ]
---

## 题目

[题目传送门](https://www.luogu.com.cn/problem/P3389)

## 代码

```c++
#include<bits/stdc++.h>
using namespace std;
typedef double db;
const db err = 1e-6;
db a[105][105];
db ans[105];
int getans(int n){
    const int has_only_solution = 0;
    const int no_solution = 1;
    const int infinite_solutions = 2;
    int r, c;
    for(r = 0, c = 0; c < n; c++){
        int t = r;
        for(int i = r; i < n; i++){
            if(abs(abs(a[i][c])-abs(a[t][c]))>err)
                t = i;
        }
        if(abs(a[t][c])<err)continue;
        for(int i = c; i <= n; i++)swap(a[t][i],a[r][i]);
        for(int i = n; i >= c; i--)a[r][i] /= a[r][c];
        for(int i = r+1; i < n; i++){
            if(abs(a[i][c]) > err){
                for(int j = n; j >= c; j--){
                    a[i][j] -= a[r][j]*a[i][c];
                }
            }
        }
        r++;
    }
    if(r < n){
        for(int i = r; i < n; i++)
            if(abs(a[i][n]) > err)
                return no_solution;
        return infinite_solutions;
    }
    for(int i = n-1; i >= 0; i--){
        for(int j = i+1; j < n; j++){
            a[i][n]-=a[i][j]*a[j][n];
        }
    }
    return has_only_solution;
}
int main(){
    freopen("yl.in","r",stdin);
    int n;
    scanf("%d",&n);
    for(int i = 0; i < n; i++){
        for(int j = 0; j <= n; j++){
            scanf("%lf",&a[i][j]);
        }
    }
    int t = getans(n);
    if(t == 0){
        for(int i = 0; i < n; i++){
            printf("%.2lf\n",a[i][n]);
        }
    }
    else printf("No Solution");
    return 0;
}

```

