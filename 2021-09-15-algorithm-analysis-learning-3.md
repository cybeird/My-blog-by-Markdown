---
title: 算法第三课-够快的排序
date: 2021-09-07 08:21:43
tags:
- c艹
- algorithm
- qSort
- STL
categories:
- AfterRead
- Algorithm Analysis
description: 不晓得辣里出料问题
---

```cpp
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <cmath>
#include <ctime>
#define N 10

using namespace std;

bool cmp(int a, int b)
{
    if(a<b) return true;
    else return false;
} //通过调整这个函数的符号来决定函数排序后序列的增减性

int basefinder(int* a, int begin, int end)
{
    int i=begin+1, j=end;
    int mid = a[i-1];
    while(true) {
        while(cmp(a[i], mid) && i < end) {i++;}
        while(cmp(mid, a[j])) {j--;}
        if(i >= j) break;
        swap(a[i], a[j]); //stl库里边应该有swap函数吧， 我确实是懒得写了
//        int tmp = a[i];
//        a[i] = a[j];
//        a[j] = tmp;    //最后还是得自己写一个
//他喵的自己写的是错的
    }
    a[begin] = a[i];
    a[i] = mid;
    return mid;
}//找一个合适的基准点，顺便交换数值

void qSort(int* a,int begin, int end)
{
    if(begin < end) {
        int mid = basefinder(a, begin, end);
        qSort(a, begin, mid-1);
        qSort(a, mid+1, end);
    }//递归啦啦啦
}

int main()
{
    int a[N+2];
    srand(time(0));
    cout<< "before" << endl;
	for(int i = 1; i <= N; i++) {
		a[i]=rand()%100;
        cout << a[i] << ' ';
    }
    cout << endl << endl<< "after" << endl;
    // 在a数组中生成了N个随机数
    qSort(a, 1, N);
	for(int i = 1; i <= N; i++) cout << a[i] << " ";
    return 0;
}
```

有问题，属实有问题

但是因为我们有万能的STL，所以日后再谈，日后再谈

//刚刚给国同学讲时间复杂度的概念，结果拿快排举例子还举错了，我太菜了
