---
layout:     post
title:      AcWing179-八数码
subtitle:   
date:       2021-10-21
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing , c++ , NOIP ]
---

## 题目

[题目传送门](https://www.acwing.com/problem/content/181/)

## 代码

```c++
#include<bits/stdc++.h>

using namespace std;
map<int,int> m;
int dx[4] = {0,1,-1,0}, dy[4] = {1,0,0,-1};
const int ed = 123456780;
int pow10(int x){
    if(x <= 0)return 1;
    int res = 1;
    while(x--)res *= 10;
    return res;
}
int getat(int n, int x){
    return n%pow10(x+1)/pow10(x);
}
void sswap(int &n, int x, int y){
    if(x > y)swap(x,y);
    int tmp = getat(n,y);
    n -= tmp*pow10(y);
    n += getat(n,x)*pow10(y);
    n -= getat(n,x)*pow10(x);
    n += tmp*pow10(x);
}
int move(int x, int k){
    return (x/3+dx[k])*3+(x%3+dy[k]);
}
int bfs(int beg){
    queue<pair<int,int> > q;
    q.push({beg,0});
    m[beg] = true;
    while(q.size()){
        int ns = q.front().first;
        int stps = q.front().second;
        q.pop();
        if(ns==ed)return stps;
        int x;
        for(int i = 0; i < 9; i++){
            if(getat(ns,i) == 0){
                x=i;
                break;
            }
        }
        for(int i =0; i < 4; i++){
            if(x/3+dx[i]>=0&&x/3+dx[i]<3&&x%3+dy[i]>=0&&x%3+dy[i]<3){
                int newx = move(x,i);
                sswap(ns,x,newx);
                if(!m.count(ns)){
                    m[ns] = 3-i;
                    q.push({ns,stps+1});
                }
                sswap(ns,x,newx);
            }
        }
    }
    return -1;
}
int main(){
    int beg = 0;
    for(int i =0; i < 3; i++){
        for(int j = 0; j < 3; j++){
            char c[2];
            scanf("%s",c);
            if(c[0] == 'x')c[0] = '0';
            beg = beg * 10 + c[0] - '0';
        }
    }
    int k = bfs(beg);
    if(k == -1)cout << "unsolvable" << endl;
    else {
        k=ed;
        stack<int> stk;
        while(k != beg){
            stk.push(m[k]);
            int x;
            for(int i =0; i < 9; i++)
                if(getat(k,i) == 0){
                    x = i;
                    break;
                }
            sswap(k,x,move(x,m[k]));
        }
        while(stk.size()){
            int t = stk.top();
            stk.pop();
            switch (t){
                case 0:
                    cout << 'r';
                    break;
                case 1:
                    cout << 'd';
                    break;
                case 2:
                    cout << 'u';
                    break;
                case 3:
                    cout << 'l';
                    break;
            }
        }
        cout << endl;
    }
    return 0;
}
```

