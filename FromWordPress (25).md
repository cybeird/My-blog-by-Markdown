---
title: 真~水题 一元三次方程！(TOWQs)
tags:
  - cpp
  - TOWQs
  - Trip Of WaterQuestions
  - 搜索
  - 枚举
id: 931
categories:
  - cpp
date: 2016-10-08 14:40:48
---

这是我第一次写如此正常的题解，心情感到十分激动；

没错，我遵循我的[誓言](https://cybirdy.wordpress.com/2016/10/05/%e9%87%8c%e7%a8%8b%e7%a2%91%ef%bc%81%e5%b1%85%e7%84%b6%e8%a6%81%e5%bc%80%e5%a7%8b%e7%96%af%e7%8b%82%e6%90%9c%e7%b4%a2%e6%b0%b4%e9%a2%98%ef%bc%81/)来刷水题，而最近的水题则是关于灰常简单的！没错，就是非常简单的枚举而已。恩，而今天写的就是[这道题目](https://vijos.org/p/1116)；<!--more-->

当然，这道题据说也是可以直接用公式来做，但是我们说好了要用枚举当然不能用如此无脑的方式了(当然枚举也很无脑，而且我也担心用公式的话会出现关于精度的问题）

主要还是二分，然后端点进行特殊处理
> 提示：记函数f(x)，若存在2个实数x1和x2，且x1&lt;x2，使f(x1)*(x2)&lt;0，则在(x1, x2)之间一定存在实数x0使得f(x0)=0。
而且相信大家也都在提示里面看到了，就基于这个原理来二分，不断枚举直到找到符合条件的值

下面上代码
```c++
#include <iostream>
#include <cstdio>
#define TINY 0.000000001
double a,b,c,d,l,r,p;
double f(double x){      //返回式子的值 
    return ((a*x+b)*x+c)*x+d;
}
inline int equal(double a,double b){
    return fabs(a-b)&lt;TINY;
}
int main(){
    scanf("%lf%lf%lf%lf",&amp;a,&amp;b,&amp;c,&amp;d);
    l=-100;
    for(l=-100.0;l&lt;=99.0;l+=1.0){  //从-100开始枚举                   
    r=l+1;                 
    double M=f(l)*f(r);                 
    if(M&gt;0)
            continue;		//如果f(l)*f(r)&gt;0，那么跳出本次循环 
        double pl=l,pr=r,pm;
        if(equal(f(l),0)){
            printf("%.2lf ",l);
            continue;
        }
        if(equal(f(r),0)){
            l++;
            printf("%.2lf ",r);
            continue;
        }      //左右两边不断缩小寻找范围，直到找到那个值（结果） 
        while(1){
            pm=(pl+pr)/2;
            if(f(pl)*f(pm)&lt;=0)
                pr=pm;
            else
                pl=pm;
            if(equal(f(pm),0)){
                printf("%.2lf ",pm);
                break;  //还是二分 
            }
        }
    }
    return 0;
}
```