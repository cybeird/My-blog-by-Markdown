---
title: 算法第二课-二分后查找
date: 2021-09-07 08:21:43
tags:
- c艹
- algorithm
- binarySearch
categories:
- AfterRead
- Algorithm Analysis
description: 今天算是在机房上的第一节课，刚好学学二分，就从基础题目开始做起吧

---

## 吐槽

老师见我们有的人买了实验报告书而有的人没买略微有些惊奇，我还在想代码的事情，结果老师告诉我们她填这本书完全是为了自己看看的，哈哈哈哈哈哈哈我是伞兵。不过老师随即表示这书买了也不亏，如果你想练练算法题不也方便许多吗。我觉得老师说的很有道理，然后打开了PTA

现在是上课一个小时后，看见长青大佬在疯狂刷题，我的心情十分复杂，根本无法沉下心来做题了T。T

## 算法核心与分析

二分搜索，就是通过不断二分然后比较的方式来进行序列内元素的查找：

首先找到数组内的中间元素`mid`开始比较，然后向左从`begin`到`mid`，向右从`mid+1`到`end`逐步分治下去。最终比较到第一个所需的数字并返回其位置（如果数组内有多个相似的值就没办法了，我个人觉得可以写个优先队列来存储位置，但是我实在是太懒啦）

 ## 算法代码

```cpp
#include <ctime>
#include <cstdio>
#include <iostream>
#include <algorithm>

#define N 10

using namespace std;

int binarySearch(int *a, int begin, int end, int x)
{
    if(end - begin >= 0)
        while(begin < end) {
            int mid = (begin + 1 + end)/2;
            if (x != a[begin]) {
            if(binarySearch(a, begin, mid, x) != -1)return binarySearch(a, begin, mid, x);
            else return binarySearch(a, mid+1, end, x);
            }
            else return begin;
        }
    else return -1;
}

int main()
{
    int a[N];
    srand(time(0));
    cout<< "before" << endl ;
	for(int i = 1; i <= N; i++) {
		a[i]=rand()%100;
        cout << a[i] << ' ';
    }
    // 在a数组中生成了100个随机数
    // 归并排序我们已经写过一个可以运行的了，这次就按照老师的要求写一个二分查找吧
    cout << endl << "which number do you like?" << endl;
    int num;cin >> num;
    cout << binarySearch(a, 1, N, num);
    return 0;
}
```

报错的原因是因为第一个函数被程序判断为没有写返回值（如果实在看不顺眼可以写个`return 0;`不过这个永远也不会被用到罢了）

原本我是打算每次分治之后先检查第一个值然后再去接着二分的，但是仔细想想若如此做反而是浪费了更多的时间去进行重复的比较，所以最后还是按照这种方式来写。

## 时间复杂度和空间复杂度

对于n长的序列进行二分搜索最差的情况也就进行了logn次查找，所以时间复杂度应该是O(logn)吧

空间复杂度基本就用了一个用来存数列的数组，也就是O(n)
