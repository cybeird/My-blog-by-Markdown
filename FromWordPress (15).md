---
title: 好奇~真相难道是...数据太水？(TOWQs)
tags:
  - cpp
  - 逆序对
  - TOWQs
  - Trip Of WaterQuestions
  - 归并排序
id: 792
categories:
  - cpp
date: 2016-10-03 16:58:35
---

[原题链接](http://www.rqnoj.cn/problem/509) (这道题原本是第三天集训时的第二题，但是我竟然在网上一个不知名的oj上找到了这道题目)<!--more-->

其实这道题就是逆序对的变种，变成正序对而已。最朴素的方法就是枚举，不过时间太长了。我们先看一下朴素做法。
<pre>for(int i=2;i&lt;=n;i++){      
    int shazam=score[i];      
    for(int j=i-1;j&gt;=1;j--){
          if(score[j]&lt;(--shazam)) ans++;
    }
}
</pre>
很简洁，但如果稍加改动，就能形成标准的顺序对。
这样，a[i]就可以表示为第i次开始得分减去序号，若a[i]&lt;a[j]，那么第j次考试就鄙视了第i次考试。
之后，就是将求逆序对的程序改为求顺序对的程序就行了。

我们首先来复习一下归并排序为何物。

* * *

### 归并排序

假设当前求的是子数列A[low..high]的逆序数，记为d(low，high)。

#### 分治

将子数列A[low..high]分成数的个数尽量相等的两个部分，A[low..mid]和A[mid+1，high](mid=(low+high)div 2)。如果逆序对中的两个数分别取自子数列A[low..mid]和A[mid+1..high]的话，则该类逆序对的个数记入f(low，mid，high)。显然:
d(low,high)=d(low,mid)+d(mid+1,high)+f(low,mid,high)
假设当前求的是子数列A[low..high]的逆序数，记为d(low，high)。

#### 合并

显然，计算f(low，mid，high)的快慢是算法时效的瓶颈，如果依然用两重循环来计算的话，其时效不会提高。
我们要求计算出d(low，high)后，数列A[low..high]已排序。这样一来，当求出d(low，mid)和d(mid+1，high)后，A[low，mid]和A[mid+1，high]已排序。
设指针i，j分别指向A[low，mid]和A[mid+1，high]中的某个数，且A[mid+1]，..，A[j-1]均小于A[i]，但A[j]&gt;=A[i]，那么A[mid+1..high]中比A[i]小的数共有j-mid-1个，如下图，将j-mid-1计入f(low，mid，high)。

由于A[low..mid]和A[mid+1..high]已经排序，因此只要顺序移动i，j就能保持以上条件，这是合并时间复杂度为线性时间的根本原因。例如从上图到下图的状态只需要将i顺序移动一个位置，将j顺序移动一个位置。

![%e6%97%a0%e6%a0%87%e9%a2%98](https://cybirdy.files.wordpress.com/2016/10/e697a0e6a087e9a298.png)

下面上代码！
```c++
#include&lt;cstdio&gt;
#include&lt;cstring&gt;
#include&lt;iostream&gt;
#include&lt;algorithm&gt;
using namespace std;
long i,ans,n,a[100001],b[100001];
int shazam(int left,int right)
{
        int mid,q,w,e;
        if(left!=right){
                mid=(left+right)/2;
                shazam(left,mid);
                shazam(mid+1,right);
                q=left;
                w=mid+1;
                for(e=left;e&lt;=right;e++){                         
                     if(q==mid+1) {                                 
                           b[e]=a[w];w++;continue;                         
                     }                         
                     if(w==right+1) {                                 
                           b[e]=a[q];q++;continue;                         
                     }                         
                     if (a[q]&gt;=a[w]) {
                           b[e]=a[q];q++;
                     }else {
                           b[e]=a[w];w++; ans=(ans+mid-q+1)%12345;
                     }
                }
                for(e=left;e&lt;=right;e++)
                       a[e]=b[e];
        }
}

int main()
{
        #ifdef LOCAL
        freopen("bis.in","r",stdin);
        freopen("bis.out","w",stdout);
        #endif // LOCAL
        scanf("%d",&amp;n);
        for(i=1;i&lt;=n;i++){
                scanf("%d",&amp;a[i]);
                a[i]=a[i]-i;
        }
        if(n==1){printf("0");return 0;}
        shazam(1,n);
        printf("%d",ans);
        return 0;
}
```