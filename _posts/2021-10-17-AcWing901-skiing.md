---
layout:     post
title:      AcWing901滑雪
subtitle:   
date:       2021-10-17
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing ,  NOIP ]
---

## 题目：

[题目传送门](https://www.acwing.com/problem/content/903/)

## 代码：

```c++
#include<bits/stdc++.h>

using namespace std;
int a[305][305];
int f[305][305];
int dx[4] = {0,1,0,-1}, dy[4] = {1,0,-1,0};
int n, m;
int dp(int x, int y){
    if(f[x][y])return f[x][y];
    f[x][y] = 1;
    for(int i = 0; i < 4; i++){
        int nx = x + dx[i];
        int ny = y + dy[i];
        if(nx >= 0 && nx < n && ny >= 0 && ny < m && a[nx][ny] < a[x][y])
            f[x][y] = max(f[x][y],dp(nx,ny)+1);
    }
    return f[x][y];
}
int main(){
    cin >> n >> m;
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            cin >> a[i][j];
        }
    }
    int res = 0;
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            res = max(res,dp(i,j));
        }
    }
    cout << res << endl;
    return 0;
}

```

