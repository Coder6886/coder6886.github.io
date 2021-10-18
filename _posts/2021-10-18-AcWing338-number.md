---
layout:     post
title:      AcWing338计数问题
subtitle:   
date:       2021-10-18
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing ,  NOIP ]
---

## 题目：

[题目传送门](https://www.acwing.com/problem/content/340/)

## 代码：

```c++
#include<bits/stdc++.h>

using namespace std;
struct numb{
    vector<int> v;
    numb(int x){
        for(int i = x;i; i/=10){
            v.push_back(i%10);
        }
    }
    int len(){
        return v.size();
    }
    int getat(int l, int r){
        int res = 0;
        for(auto i = v.begin()+r; i >= v.begin()+l; i--){
            res = res * 10 + *i;
        }
        return res;
    }
    int toint(){
        return getat(0,v.size()-1);
    }
};
int pow10(int b){
    if(b < 0)return 0;
    if(b == 0)return 1;
    if(b == 1)return 10;
    int ans = pow10(b/2);
    ans *= ans;
    if(b%2)ans *= 10;
    return ans;
}
int count(int n, int x){
    if(n == 0)return 0;
    numb num(n);
    n = num.len();
    int res = 0;
    for(int i = n-1-!x; i >= 0; i--){
        if(i < n-1){
            res += num.getat(i+1,n-1) * pow10(i);
            if(!x)res -= pow10(i);
        }
        if(num.getat(i,i)==x)res += num.getat(0,i-1)+1;
        else if(num.getat(i,i)>x)res += pow10(i);
    }
    return res;
}
int main(){
    int n,m;
    while(cin >> n >> m && n && m){
        if(n > m)swap(n,m);
        for(int i = 0; i < 10; i++){
            cout << count(m,i)-count(n-1,i) << ' ';
        }
        cout << endl;
    }
    return 0;
}

```

