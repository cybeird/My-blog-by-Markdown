---
title: 树状天平(Not so Mobile,UVa 839)(TOWQs)
date: 2016-11-08 17:38:54
categories:
  - cpp
tags:
  - 正常的题目
  - TOWQs
  - Trip Of WaterQuestions
  - Binary Tree
  - 数据结构基础
keywords: 
  - 二叉树
  - Binary Tree
  - UVa
description: 一道非常不错的关于二叉树的题目，从算法竞赛入门经典上搞到的。
---
下面看一道名为天平的题目(Not si Mobile,UVa 839)
### 题目描述
　　输入一个树状天平,根据力矩相等的原则判断是否平衡。如图，所谓力矩相等，就是W<sub>l</sub>D<sub>l</sub>=W<sub>r</sub>D<sub>r</sub>，其中W<sub>l</sub>和W<sub>r</sub>分别为左右两边砝码的重量，D为距离。
　　采用递归(先序)方式输入:每个天平的格式为W<sub>l</sub>,D<sub>l</sub>,W<sub>r</sub>,D<sub>r</sub>，当W<sub>l</sub>或W<sub>r</sub>为0时，表示该“砝码”实际是一个子天平，接下来会描述这个子天平。当W<sub>l</sub>=W<sub>r</sub>=0时，会先描述左子天平，然后是右子天平。
### 样例输入
> 1
> 0 2 0 4
> 0 3 0 1
> 1 1 1 1 
> 2 4 4 2
> 1 6 3 2

![](http://ofshdv83w.bkt.clouddn.com/image/ipg%E5%A4%A9%E5%B9%B3%281%29.JPG)

### 样例输出
> YES

![](http://ofshdv83w.bkt.clouddn.com/image/ipg%E5%A4%A9%E5%B9%B3%282%29.JPG)

### 题目分析
　　这道题目的输入主要采用了递归方式定义，因此可以用一个递归程序来输入，同时在输入的同时完成判断。
```cpp
#include <iostream>
using namespace std;
bool solve(int& W) {
	int Wl, Dl, Wr, Dr;
	bool b1 = true, b2 = true;
	scanf("%d%d%D%D", &Wl, &Dl, &Wr, &Dr);
	if(!Wl) b1 = solve(Wl);
	if(!Wr) b2 = solve(Wr);
	W = Wl + Wr;
	return b1 && b2 && (Wl * Dl == Wr * Dr);
}
int main()
{
	int T, W;
	cin >> T;
	while(T--) {
		if(solve(W)) puts("YES\n");
		else puts("NO\n");
		if(T) puts("\n");
	}
	return 0;
}
```
