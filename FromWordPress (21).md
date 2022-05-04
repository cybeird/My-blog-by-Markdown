---
title: 惊！原本认为很简单的题目竟然有着不可思议的变种(TOWQs)
tags:
  - cpp
  - TOWQs
  - Trip Of WaterQuestions
  - 强势
  - 作死
id: 647
categories:
  - cpp
date: 2016-09-26 10:43:13
---

[陶陶摘苹果](https://vijos.org/p/1102)这道题相信大家早已了熟于心，但是我今天（也许不是今天，只是我突然想起来了而已）发现了这道题还有一个非官方版本的续集！！<!--more-->
> 话说去年苹果们被陶陶摘下来后都很生气，于是就用最先进的克隆技术把陶陶克隆了好多份&gt;.&lt;然后把他们挂在树上，准备摘取。 摘取的规则是，一个苹果只能摘一个陶陶，且只能在它所能摘到的高度以下的最高的陶陶，如果摘不到的话只能灰溜溜的走开了&gt;.&lt;给出苹果数目及每个苹果可以够到的高度和各个陶陶的高度，求苹果们都摘完后剩下多少个陶陶……
没错，就是[它](https://vijos.org/p/1291)，苹果摘淘淘，先暂且不论版权什么的问题，就是这题目描述，就足以证明出题人的脑洞已经突破天际了！

当然，尽管它的题目描述很令人感到惊奇，但是题目本身还是比较水的（贪心即可）；下面上代码
```c++
#include&lt;cstdio&gt;
#include&lt;cstring&gt;
#include&lt;iostream&gt;
#include&lt;algorithm&gt; 
using namespace std;
int main()
{
	int n,m,t[2001],a[2001];
	scanf("%d%d",&n,&m);
	for(int i=1;i<=n;i++)
		scanf("%d",&t[i]);
	for(int i=1;i<=m;i++)
		scanf("%d",&a[i]);
	int ans=n;
	sort(t+1,t+n+1);
	int j=m;
	for(int i=1;i<=n;i++) 	 	//for(;j<=0;j++)
		if(a[i]<=t[j]&&t[j]!=0)
		{
			t[j]=0;
			j--;
			ans--;
		}
	printf("%d",ans);
	return 0;
}
```
当然，作为蒻稽的我怎能不先WA一下之后再AC呢！没错，如此之水的题目我依旧出现了不可饶恕之错误！

我一开始的思路十分简单，就是定义两个数组，一个放苹果，一个放淘淘，紧接着，我们对苹果的那个数组进行排序，到此为止的思路都很正确，不过我没又想到题目中的这一句话！
> 一个苹果只能摘一个陶陶，且只能在它所能摘到的高度以下的**最高的**陶陶
没错，我这个程序完全是把苹果当成有序的来做了，然而并不是，因为它摘不到之后就会走掉。

所以。。我如果只用一行循环的话就回WA掉，唯一的解决方法就是用两行循环！
```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
using namespace std;

int n,m,a[2010],t[2010];
int main()
{
    scanf("%d%d",&n,&m);
    for(int i=1;i<=n;i++)
    scanf("%d",&a[i]);
    for(int i=1;i<=m;i++)
    scanf("%d",&t[i]);
    int taotao=m;
    sort(t+1,t+m+1);
    for(int i=1;i<=n;i++)
    {
        for(int j=m;j>0;j--)
        {
            if(a[i]>t[j]&&t[j]!=0)
            {
                t[j]=0;
                taotao--;
                break;
            }
        }
    } 
    printf("%d",taotao);
    return 0;
}
```
就是这样，这惨痛的教训告诉我们一定要看清题目再去做题！