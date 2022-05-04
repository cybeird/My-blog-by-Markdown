---
title: 算法第四课-DP靠顿悟
date: 2021-09-14 18:38:43
tags:
- DP
- c艹
- algorithm
categories:
- AfterRead
- Algorithm Analysis
description: 今天也算是好好听课了吧，递推的解法可以更好的做到记忆化，但是递归的解法看起来更加优雅，那么我应该选择哪一种呢？

---

## 引入

我感觉我没有必要专门再去写一个引入，因为无论是通俗易懂的金矿模型还是经典的01背包问题（抑或是今天老师讲的超市买东西）都讲的很不错，看这些肯定比我这个半吊子强。

## 算法核心问题及步骤解析

### 核心

往往当我们遇见满足下列条件的问题时，就可以更好地采用动态规划来解决。

* 最优子问题

* 子问题重叠

* 边界

* 子问题独立

这四个问题基本就是整个动态规划能够运作的核心，当然，我们往往还会进行额外的备忘录和时间分析

## 步骤

动态规划本质上依旧使用了分治的思想，同时致力于解决冗余这一方面。

1. 动态转移方程

2. 递归

3. 自下而上

4. 构造最优解

### 状态转移方程

写出状态转移方程可以说是整个动态规划算法运行的核心，我们以01背包为例子

> 这里有一个容积为V的背包，还有一堆占用体积为vi，质量为mi的货物，想出一种装法，使得其最重从而沉死翔孙。

我们设定当前开始的货物编号为begin，最后为end，那么对于每一种货物我们无非就只有装或者不装两种选择（这样递归下去就变成了一棵完全二叉树）

如下所示

```cpp
chensixiangsun(begin, end, V) = max{ chensixiangsun(begin, end-1, V), chensixiangsun(begin, end-1, V-vi) + mi};
```

很完美（01背包不需要做备忘录）

```cpp
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <cmath>
#define N 20
using namespace std;

//01背包实在是太经典啦，怎么都得写个一写
int V, m[N], v[N], n;

int dfs(int V, int end)
{
    if(end > 0)
    return max( dfs(V, end-1), dfs(V-v[end], end-1) + m[end]);
    return 0;
}

int main()
{
    cin >> V >> n;
    for(int i = 1; i <= n; i++)
        cin >> v[i] >> m[i];
    cout << dfs(V, n);
    return 0;
}
```



时间复杂度是O(2^n^)吗，这点我们待会再谈

动态规划主要分为：记忆化搜索（递归+记忆函数），递推

递归由于对于重复的子问题会进行大量的重复计算，所以效率会低于递推

## 递推

时间复杂度是O(n^2^)

```cpp
int i, j;
for(j = 1; j <= n; j++) d[n][j] = a[n][j];
for(i = n-1; i >= 1; i--)
    for(j = 1; j <= i; j++)
        d[i][j] = a[i][j] + max(d[i+1][j], d[i+1][j+1]);
```

## 记忆化搜索

```cpp
int solve(int i, int j) {
    if(d[i][j] >= 0) return d[i][j];
    return d[i][j] = a[i][j] + (i == n ? 0 : max(solve(i+1,j), solve(i+1, j+1)));
}
```

时间复杂度从O(2^n^)升格到O(n^2^)

#### 小秘籍（转载自我也忘了是哪）

##### 思考路线

1. 动规开始
    1. 写出dp状态和方程
    2. 写出dfs函数
    3. 添加记忆化数组
2. 爆搜开始
    1. dfs版爆搜
    2. 去除外部变量
    3. 添加记忆化数组

##### 滚动数组

以斐波那契数列为例，对于求第n个数，我们往往使用递推的方式进行实现，但是我们只需要开一个大小为3的数组就够用了

```cpp
    int f[3] = {1, 1, 2};
    for(int i = 4; i <= n; i++) {
	    f[(i-1)%3] = f[(i-2)%3] + f[i%3];
    }
    cout << f[(n-1)%3];
```

这是因为我们斐波那契数列的递推公式是f[n] = f[n-1] + f[n-2] (n>2),用f[3]足以放下整个公式，空间复杂度是f[3]
