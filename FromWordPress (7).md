---
title: '一道十分经典的基础题背后竟然隐藏天大秘密！[TOWQs]'
tags:
  - cpp
  - MINE
  - TOWQs
  - Trip Of WaterQuestions
  - 强势
  - 作死
id: 517
categories:
  - cpp
date: 2016-09-23 10:16:23
---

<!--more-->
### <span style="color:#008080;">题目描述</span>

<pre>输入两个整数a,b，输出它们的和(|a|,|b|&lt;=10^9)。
注意
1、pascal使用integer会爆掉哦！
2、有负数哦！
3、c/c++的main函数必须是int类型，而且最后要return 0。这不仅对洛谷其他题目有效，而且也是noip/noi比赛的要求！

好吧，同志们，我们就从这一题开始，向着大牛的路进发。
“任何一个伟大的思想，都有一个微不足道的开始。”</pre>

### <span style="color:#008080;">格式</span>

#### **输入格式**

<pre>两个整数以空格分开</pre>

#### **输出格式**
<pre>一个数</pre>

### <span style="color:#008080;">样例</span>

#### **输入样例#1**
<pre>20 30</pre>

#### **输出样例#1**
<pre>50</pre>

* * *

这道题可以说是入门的经典题目了（当然还有Hello World），相信大家第一眼看到这道题的时候应该是这样的<!--more-->
```
Free Pascal Code

var a,b:longint;
begin
    readln(a,b);
    writeln(a+b);
end.
C Code

#include <stdio.h>
int main()
{
    int a, b;
    scanf("%d%d", &a, &b);
    printf("%d\n", a + b);
    return 0;
}
C++ Code

#include <iostream>
using namespace std;
int main()
{
    int a, b;
    cin >> a >> b;
    cout << a + b << endl;
    return 0;
}
Python Code

print(sum(map(int, raw_input().split())))
Java Code

import java.io.*;
import java.util.Scanner;

public class Main {

    /**
     * @param args
     * @throws IOException 
     */
    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        System.out.println(a + b);
    }
}
```

    但是，经过我的认真读题，详细研究之后，发现题目远远不止这么简单

    我是很清纯的一个人，本来真以为是这样子的，看了一下难度就惊呆了……
    难度⑨，不可能这么简单

    用了九牛二虎之力，我才发现，这道题目需要用类定义
    代码如下：
```cpp    
#include <iostream>
using namespace std;
class A
{
    public :
    inline void func(int,int);
    inline void print();
    private :
    int i,j;
};
int main()
{
    A a;
    int q,w;
    cin >> q >> w;
    a.func(q,w);
    a.print();
    return 0;
}
void A::func(int x,int y)
{
    i=x;  j=y;
}
void A::print()
{
cout << i+j << endl;
}
```
又想了想，用这种最简单的类定义，friend和virtual都没有用到怎么可能是正解呢？

后来，我发现这道题的真谛是这样的
```cpp
#include <iostream>;
#define bird using
#define is namespace
#define great std
#define 1 ;
#define whatever int
#define doesnot main
#define kill (
#define you )
#define simply {
#define end }
#define kil cin
#define what &gt;&gt;
#define hucha return
#define eh ,
#define shit cout
#define en &lt;&lt;
#define ao endl
#define echo +
#define stenger 0
#define makes ios_base
#define you ::
#define more sync_with_stdio 
bird is great 1
whatever doesnot kill you simply makes you more kill stenger
you 1 e SJ eh NB 1
kil what SJ what NB 1
shit en SJ echo NB en ao 1 hucha stenger
1 end
```
所以在我们做题的时候一定要挖掘所有的可能性！
