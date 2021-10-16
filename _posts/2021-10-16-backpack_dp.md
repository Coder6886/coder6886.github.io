---
layout:     post
title:      backpack_dp
subtitle:   
date:       2021-10-16
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    [ AcWing ,  NOIP ]
---

## 01背包

```c++
#include<bits/stdc++.h>

using namespace std;
int c[1005], v[1005];
int f[1005];
int main(){
    int n,m;
    cin  >> n >>  m;
    for(int i = 0; i < n; i++){
        cin >> v[i] >> c[i];
    }
    for(int i = 0; i < n; i++){
        for(int j = m; j >= v[i]; j--){
            f[j] = max(f[j],f[j-v[i]]+c[i]);
        }
    }
    cout << f[m] << endl;
    return 0;
}
```

## 完全背包

```c++
#include<bits/stdc++.h>

using namespace std;
int c[1005], v[1005];
int f[1005];
int main(){
    int n,m;
    cin  >> n >>  m;
    for(int i = 0; i < n; i++){
        cin >> v[i] >> c[i];
    }
    for(int i = 0; i < n; i++){
        for(int j = v[i]; j <= m; j++){
            f[j] = max(f[j],f[j-v[i]]+c[i]);
        }
    }
    cout << f[m] << endl;
    return 0;
}
```

## 多重背包（二进制优化）

```c++
#include<bits/stdc++.h>

using namespace std;
int v[25000], c[25000];
int f[25000];
int main(){
    int n,m;
    cin >> n >> m;
    int cnt = 0;
    for(int i = 0; i < n; i++){
        int x,y,z;
        cin >> x >> y >> z;
        int k = 1;
        while(z > k){
            v[cnt] = x*k;
            c[cnt++] = y*k;
            z -= k;
            k <<= 1;
        }
        if(z > 0){
            v[cnt] = x*z;
            c[cnt++] = y*z;
        }
    }
    for(int i = 0; i < cnt; i++){
        for(int j = m; j >= v[i]; j--){
            f[j] = max(f[j],f[j-v[i]]+c[i]);
        }
    }
    cout << f[m] << endl;
    return 0;
}
```

## 分组背包（空间2维）

```c++
#include<bits/stdc++.h>

using namespace std;
int f[105][105];
int main(){
    int n,m;
    cin >> n >> m;
    for(int i = 1; i <= n; i++){
        int s;
        cin >> s;
        for(int j = 0; j < s; j++){
            int v,c;
            cin >> v >> c;
            for(int k = m; k >= 0; k--){
                f[i][k] = max({f[i][k],k>=v?f[i-1][k-v]+c:-1,f[i-1][k]});
            }
        }
    }
    cout << f[n][m] << endl;
    return 0;
}
```

## 分组背包（空间1维）

```c++
#include<bits/stdc++.h>

using namespace std;
int f[105],v[105],c[105];
int main(){
    int n,m;
    cin >> n >> m;
    for(int i = 1; i <= n; i++){
        int s;
        cin >> s;
        for(int j = 0; j < s; j++){
            cin >> v[j] >> c[j];
        }
        for(int k = m; k >= 0; k--){
            for(int j = 0; j < s; j++){
                f[k] = max(f[k],k>=v[j]?f[k-v[j]]+c[j]:-1);
            }
        }
    }
    cout << f[m] << endl;
    return 0;
}
```

