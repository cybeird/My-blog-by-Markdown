---
title: 如何将将类模板中的成员函数在类模板外定义呢
date: 2019-10-11 20:13:41
categories:
- cpp
tags:
- 学习
- 类模板
- 类
keywords:
description: 我之前在这个地方卡了许久，后来后知后觉的发现了错误
---

1. 首先我们知道类模板很重要，而这个声明是在类前进行的

2. 但是每个成员函数在模板外定义的时候都要再声明一边类模板，这就是我所知道但却忘记的

   附上源码：

   ```c++
   #include <iostream>
   using namespace std;
   
   template<class numtype>				//定义类模板
   
   class Compare {
   	public:
   		Compare(numtype a, numtype b)
   		{x=a;y=b;}
   		numtype max();
   		numtype min();
   	private:
   		numtype x,y;
   };
   numtype Compare::max()
   {return (x>y)?x:y;}
   numtype Compare::min()
   {return (x<y)?x:y;}
   
   int main()
   {
   	Compare<int> cmp1(3,7);														//比较整数
   	cout<<cmp1.max()<<" is the Maximum of two interger numbers."<<endl;
   	cout<<cmp1.min()<<" is the Minimum of two interger numbers."<<endl<<endl;
   	Compare<float> cmp2(45.78, 93.6);											//比较浮点数
   	cout<<cmp2.max()<<" is the Maximum of two interger numbers."<<endl;
   	cout<<cmp2.min()<<" is the Minimum of two interger numbers."<<endl<<endl;
   	Compare<char> cmp3('a', 'A');												//比较字符
   	cout<<cmp3.max()<<" is the Maximum of two interger numbers."<<endl;
   	cout<<cmp3.min()<<" is the Minimum of two interger numbers."<<endl<<endl;
   	int sundea;cin>>sundea;
   	return 0;
   }
   ```

   这是错误代码，实际上运行之后的错误报告已经告诉我问题了，许久才意识到

![错误报告](https://i.loli.net/2019/10/11/BMfa9XhHDSIVqd1.png)

