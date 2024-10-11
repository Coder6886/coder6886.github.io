---
layout:     post
title:      碰数游戏——你真的彻底赢过吗？
subtitle:   你真正了解过这个游戏吗？
date:       2023-12-19
author:     coder6886
header-img: img/post-bg-island.jpg
catalog: true
usemathjax: true
tags:
    - c++
---
你小时候玩过碰数吗？我现在也还在上初中，也很爱玩这个游戏。

那应该很多玩过这个游戏的小朋友们都想过，我怎么才能打遍天下无敌手？这可不可能？

# Part 1.规则

碰数游戏本来是用来教小学生加法用的，上了初中就变成了实在没事可干时玩的游戏了。

规则是这样的。

有两个人，甲和乙。

每个人有两只手（~~只有一只手或有三只手的人禁止参加游戏~~），每只手可以表示一个从0到9的数字。

开始时，两个人手上的四个数都是1。甲先进行操作。每一个人每一步可以进行如下操作：

将自己任意一个数字不是零的手去“碰”另一个人任意一个数字不是零的手，并用自己那只手上的数字和自己选择另一个人的那只手上的数字模10的和覆盖自己去碰另一个人的那只手上的数字。

当一方的两个手上的数都为零时，这一方获胜。

这一部分读着有点绕，但网上应该有很多教碰数规则的教程，我就不多赘述了。

# Part 2.原理

先说结论：这个游戏是**有**一个游戏策略保证你不输的。**不管你是先手还是后手**

但“打遍天下无敌手”是**不可能**的，因为最好的策略里都有可能有平局的情况出现。

我现在就来说如何找到这个神奇的不败策略。

其实简略分析一番，会发现做一个不会败的机器人其实不需要像做一个象棋机器人一样那么难。

大家可以看到，整个游戏最多只有$10^4$种状态（四只手，每只手十个数），电脑处理起来都用不了半秒钟。所以我们进行暴力搜索。

然后我们具体考虑一下如何进行搜索。

其实最直观的想法往往就是最正确的想法——DFS，深度优先搜索。

我们只需要从开局的$<1,1;1,1>$状态，将先手可能走的四步挨个枚举一遍，再搜索这四步对应的下一步，……最后一直搜到胜败明了或出现循环。最后回溯就可以知道是否有必胜策略或不败策略。

# Part 3.实现

下面我来根大家说一些细节（看完之后记得看注释）。

首先，这是一个不败的碰数机器人。

![touch-numbers-fig1](/img/touch-numbers-fig1.png)

它的左手边就是你的左手边，它的右手边也是你的右手边。

举个例子，当一个操作是`lr`时，它的意思就是施加操作的那一方的左手(`Left`即`l`)去碰对面的右手(`Right`即`r`)，组合起来就是`lr`。

至于搜索的过程，dfs内显示三个特判（分别是判断输赢和判断是否出现循环），然后是一行记忆化搜索的剪枝，然后是标记正在搜索，最后那一大串就是具体的搜索过程。

具体原理请看代码注释。

```c++
#include<bits/stdc++.h>

using namespace std;
int vis[10][10][10][11];//保存当前状态的数组
int howmove[10][10][10][11];//保存当前状态下最优步骤的数组
const int LTL = 1,LTR = 2,RTL = 3,RTR = 4;//四种步骤的‘代号’
const int ICANWIN = 1,ICANTIE = 2, IMUSTLOOSE = 3;//三种状态的‘代号’
int dfs(int ml,int mr,int hl,int hr){//my left hand(ml),my right hand(mr),his left hand(hl),his right hand(hr)
    //三个特判
    if(ml == mr && ml == 0){
        vis[ml][mr][hl][hr] = ICANWIN;
        return ICANWIN;//我有必胜策略（我已经赢了）
    }
    if(hl == hr && hl == 0){
        vis[ml][mr][hl][hr] = IMUSTLOOSE;
        return IMUSTLOOSE;//我必输（我已经输了）
    }
    if(vis[ml][mr][hl][hr]==0x3f3f3f3f){
        return ICANTIE;//搜索到了正在搜索的这一支上的点，说明出现了循环
    }
    //注意，特判和搜索的顺序是有讲究的，尤其是判断循环的那一块
    if(vis[ml][mr][hl][hr])return vis[ml][mr][hl][hr];//记忆化搜索
    vis[ml][mr][hl][hr] = 0x3f3f3f3f;//标记为正在搜索
    if(ml != 0){
        if(hl != 0)
            if(4-dfs(hl,hr,(ml+hl)%10,mr)<vis[ml][mr][hl][hr]){
                vis[ml][mr][hl][hr] = 4-dfs(hl,hr,(ml+hl)%10,mr);
                //一部之后敌人的必胜态就是我的必败态
                //敌人的必败态就是我的必胜态
                //敌人可以不败则我也可以保证不败
                //手动实现min函数就是为了选择最优步骤
                //这一段代码可以好好研究一下
                howmove[ml][mr][hl][hr] = LTL;//记录最优步骤
            }
        if(hr != 0)
            if(4-dfs(hl,hr,(ml+hr)%10,mr)<vis[ml][mr][hl][hr]){
                vis[ml][mr][hl][hr] = 4-dfs(hl,hr,(ml+hr)%10,mr);
                howmove[ml][mr][hl][hr] = LTR;
            }
    }
    if(mr != 0){
        if(hl != 0)
            if(4-dfs(hl,hr,ml,(mr+hl)%10)<vis[ml][mr][hl][hr]){
                vis[ml][mr][hl][hr] = 4-dfs(hl,hr,ml,(mr+hl)%10);
                howmove[ml][mr][hl][hr] = RTL;
            }
        if(hr != 0)
            if(4-dfs(hl,hr,ml,(mr+hr)%10)<vis[ml][mr][hl][hr]){
                vis[ml][mr][hl][hr] = 4-dfs(hl,hr,ml,(mr+hr)%10);
                howmove[ml][mr][hl][hr] = RTR;
            }
    }
    return vis[ml][mr][hl][hr];
}
int main(){
    for(int i = 0; i < 10; i++){
        for(int j = 0; j < 10; j++){
            for(int k = 0; k < 10; k++){
                for(int l = 0; l < 10; l++){
                    if(!vis[i][j][k][l])dfs(i,j,k,l);
                }
            }
        }
    }
    int coml = 1,comr = 1,myl = 1,myr = 1;
    while(1){
        cout << "Take your move" << endl;
        cout << coml << comr << endl << myl << myr << endl;
        string s;
        cout << ">";
        cin >> s;
        if(s[0] == 'l' && s[1] == 'l')myl = (myl + coml)%10;
        if(s[0] == 'l' && s[1] == 'r')myl = (myl + comr)%10;
        if(s[0] == 'r' && s[1] == 'l')myr = (myr + coml)%10;
        if(s[0] == 'r' && s[1] == 'r')myr = (myr + comr)%10;
        cout << coml << comr << endl << myl << myr << endl;
        if(howmove[coml][comr][myl][myr] == LTL)coml = (coml + myl)%10,cout << "Computer takes move ll" << endl;
        else if(howmove[coml][comr][myl][myr] == LTR)coml = (coml + myr)%10,cout << "Computer takes move lr" << endl;
        else if(howmove[coml][comr][myl][myr] == RTL)comr = (comr + myl)%10,cout << "Computer takes move rl" << endl;
        else if(howmove[coml][comr][myl][myr] == RTR)comr = (comr + myr)%10,cout << "Computer takes move rr" << endl;
    }
    return 0;
}


```

# Part 4.小结

其实这样的话碰数游戏就已经被我们解决了。

但是碰数机器人显现出的一个策略令我十分惊讶。

这个策略就是“**回头反打**”，也就是先给对面留个破绽，让对面将一个手碰到0，最后再用它灵活的两个手对抗对面的一个手取得胜利。因为我们同学玩这个游戏的时候从来没有用过这种策略，而都是双手对弈，尽可能让自己先出现0。

所以大家伙可以试试这个策略，看看能不能多打败一些小伙伴。

最后，如果真的想置人于死地，可以直接将`howmove`数组输出，并打印成一本小册子，每次碰数只需要翻一番这本“秘籍”，就可以“知己知彼，百战不殆”。