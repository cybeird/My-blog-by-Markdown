---
title: '『2』我要入门！矩阵？辣鸡！[Uva 442](TOWQs)'
tags:
  - cpp
  - stack
  - TOWQs
  - Trip Of WaterQuestions
  - 我要入门
  - 正常的标题
id: 1002
categories:
  - cpp
date: 2016-10-16 19:12:27
---

嗯，今天要刷的水题是一道[看起来很难的题目](https://uva.onlinejudge.org/index.php?option=onlinejudge&amp;page=show_problem&amp;problem=383)，因为当我们看到矩阵的时候难免会有‘一阵阵的恶心’，但是再仔细读了题意之后就会发现，这是一道很辣鸡的水题。<!--more-->

#### 仔细瞅瞅

发现本题的关键就是解析表达式，而比较简单的解析表达式可以借助栈来完成。
代码如下：
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cstdio>
#include <stack>
using namespace std;

struct Matrix{
	int a,b;
	Matrix(int a=0, int b=0):a(a),b(b) {}   //定义一个结构体，这一步是构造函数
}m[26];

stack<Matrix> s;

int main()
{
	int n;
	cin >> n;
	for(int i = 0; i < n; i++){
		string name;
		cin >> name;
		int k = name[0] - 'A';
		cin >> m[k].a >> m[k].b;
	}  //嗯，这样就读入了数据
	string expr;
	while(cin >> expr) {
		int len = expr.length();		//用len来保存长度
		bool error = false;		
		int ans = 0;
		for(int i = 0; i < len; i++){
			if( isalpha(expr[i]) ) s.push(m[expr[i] - 'A']);  
			else if(expr[i] == ')') {
				Matrix m2 = s.top(); s.pop();
				Matrix m1 = s.top(); s.pop();
				if (m1.b != m2.a){ error = true; break; }		
                                        //若A的行数不等于B的列数，则乘法无法运行
				ans += m1.a * m1.b * m2.b;
				s.push(Matrix(m1.a, m2.b));
			}	       //当我们遇到右括号时出栈并计算，然后结果入栈
		}
		if(error) printf("error\n");
		else printf("%d\n", ans);
	}
	return 0;
}
```
注意到底下的算式中每两个需要相乘的矩阵都会放在一个括号中，不会出现(ABC)这样的算式。因此，每遇到一个右括号就代表要将括号之前的两个矩阵进行矩阵乘法。我们可以使用一个栈来模拟这个过程：

*   右括号 : 不用搭理它
*   矩阵名称 : 压栈
*   右括号 : 弹出栈中的前两个，进行乘法运算，将结果压栈
由此便可以模拟整个表达式的计算过程。我们可以用一个 pair 来表示矩阵的行数和列数，矩阵乘法的过程请参考《线性代数》。在前面的 res 函数中计算结果，如果遇到了没法相乘的矩阵就输出 error。这个函数可以计算结果矩阵的行数和列数并返回相乘的总次数。我们只需要将结果加起来就可以得到结果了。另外，如果表达式只有一个矩阵的话，表达式长度必为 1，直接输出结果 0。