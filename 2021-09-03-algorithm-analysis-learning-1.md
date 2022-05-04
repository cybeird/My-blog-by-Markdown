---
title: 算法第一课-分治下的归并
date: 2021-09-02 17:00:49
tags:
- Divide and Conquer
- mergeSort
- c艹
- algorithm
categories:
- AfterRead
- Algorithm Analysis
description: 老师留了一道简单的排序题，要求使用分治的思想实现，那么就借此机会复习一下归并排序的写法吧。

---

## 核心思想

归并排序的核心操作是归并（一般是二路归并），首先将待排序数列分割成若干个小子序列，在对最小的子序列进行完合并操作后，再将这些有序表逐步合并成为最终的有序序列。这个算法在老师的PPT上好像是叫做合并排序，本质上是一样的。

## 具体分析

### 题目要求

随机生成n（例如100）个数，利用分治的思想设计算法进行排序，并分析算法的复杂度

### 代码实现及思路

初步代码思路为下

```c++
#include <cstdio>
#include <iostream>
#include <ctime>
#define N 100
using namespace std;

int a[10005], b[10005] = {0};

void mergesort(int *ar, int begin, int end)
{
    if(begin < end) {  //保证数组还有的分
        int i = (end + begin)/2;
        mergesort(ar, begin, i);
        mergesort(ar, i+1, end);
        //找中点，然后分治
        for(int l = begin; l <= end; l++)  b[l] = a[l]; //将合并后的数列放到原数列
        int j = begin, k = i+1;
        for(int  n = begin; n <= end; n++) {
            if(j > i) a[n] = b[k++];
            else if(k > end) a[n] = b[j++];
            else if(b[j] < b[k]) a[n] = b[j++];
            else a[n] = b[k++];
        } //将两个有序数列合并成一个有序数列
    }
}

int main()
{
    srand(time(0));
    cout<< "before" << endl ;
	for(int i = 1; i <= N; i++) {
		a[i]=rand()%100;
        cout << a[i] << ' ';
    }
    cout << endl << endl<< "after" << endl;
    // 在a数组中生成了100个随机数
    // 分治的思想中，由于c++的STL库中自有快速排序，所以我选择写一个简单的合并排序
    mergesort(a, 1, N);
	for(int i = 1; i <= N; i++) cout << a[i] << " ";
    return 0;
}
```

先利用`ctime`库里的`rand()`函数生成100个随机数。

再写一个归并排序，首先判断是否是最小数列，否则便通过递归调用本身继续分治，然后再将分治后的两个有序数列进行合并，最终完成排序

### 算法空间复杂度和时间复杂度分析

#### 空间复杂度

使用了两个相当于数据量大小的一维数组，因此是O(n)

#### 时间复杂度

在归并的过程中，每次进行一个层级的归并操作的时间复杂度都是O(n)，而由于是二分的思想，所以归并的层级总共有log~2~n层，也就是执行了log~2~n次归并操作，最终的时间复杂度便是O(nlog~2~n)

​									
