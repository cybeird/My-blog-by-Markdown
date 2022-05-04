---
title: 'Gooooloooowoooocooo！{鱼人语：好水的题啊!}(TOWQs)'
tags:
  - cpp
  - 递推
  - MINE
  - TOWQs
  - Trip Of WaterQuestions
id: 1012
categories:
  - cpp
date: 2016-10-11 21:01:34
---

如果奇迹有颜色，那么一定是“vijos上的橙名！”色；；

没错，为了RP而奋斗的我，又一次的在[训练营](https://vijos.org/training)中发现了一道十分水的[题目](https://vijos.org/p/1130)！<!--more-->

这道题我的第一印象果断是暴力啊！原来还准备专门写个函数，

```c++
    int dfs(int x){
        int half,sum=1;
        if(x%2==0)
            half=x/2;
        else
            half=(x-1)/2;
        for(int i=1;i<=half;i++)
            sum+=dfs(i);
        return sum;
     }
```
   当然，也并非一定要整个函数出来，恩；

```c++
#include <cstdio>
int main() {
    int dp[1001],n;
    dp[1] = 1;
    scanf("%d",&n);
    for (int i = 2;i <= n;i++) {
        dp[i] = dp[i-1];
        if (!(i%2)) dp[i] += dp[i/2];
    }
    printf("%d",dp[n]);
    return 0;
}
```

恩，至于思路么，很简单。
它的左边加上一个自然数，但该自然数不能超过原数的一半;
然后我们就从该自然数左边第一位开始枚举，然后对于每一种可能的第一位，再次进行枚举，然后对于枚举出来的第一位的第一位(也就是第二位)，进行枚举，然后再对枚举出来的。。。

反正就是这么个思路，相信大家不会的看看代码就懂了，毕竟是很水的题目莫；
