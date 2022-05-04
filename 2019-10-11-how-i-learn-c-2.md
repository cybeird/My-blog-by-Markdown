---
title: C艹实验课の解题报告-Week2
date: 2019-10-10 17:09:33
categories:
- cpp
tags:
- 学习
- 友元函数
- 类
keywords:
description: c++实验课的环境是真的舒适（相比于数据结构实验课来说）
---

### 实验9 类和对象（二）

#### 实验 9.1

阅读程序啥的莫得难度，不过修改程序这个要求很玄奇

> 在main函数中调用fun函数，在fun函数中调用change和display函数。在fun函数中使用对象的引用（Student&）作为形参。

```c++
#include <iostream>
using namespace std;
class Student
{
	public:
    	Student(int n, float s):num(n), score(s) {}
    	void change(int n, float s) {num = n; score = s;}
    	void display() {cout<< num << " " << score <<endl;}
    private:
    	int num;
	    float score;
};
Student stud(101,78.5);
void fun(Student &)
{
    stud.display();
    stud.change(101,80.5);
    stud.display(); 
}
int main()
{
    fun(stud);
	//int sundea;cin >> sundea;
    return 0;
}
```

#### 实验 9.2

大概就是给数据算数，模拟就完事了

不过要用静态数据成员和静态数据函数

```c++
#include <iostream>
using namespace std;
class Product
{
	public:
		Product(int m, int q, float p): num(m), quantity(q), price(p){};
		void total();
		static float average();
		static void display();
	private:
		int num;
		int quantity;
		float price;
		static float discount;
		static float sum;
		static int n;
};
//求钱和数量
void Product::total()
{
	float rate = 1.0;
	if (quantity > 10) rate *= 0.98;
	sum += quantity*price*rate*(1-discount);
	n += quantity;
}
//输出
void Product::display()
{
	cout<< sum <<endl;
	cout<< average() <<endl;
}
//求均
float Product::average()
{	return (sum/n);}
//成员初始化
float Product::discount = 0.05;
float Product::sum = 0;
int Product::n = 0;

int main()
{
	Product Prod[3] = {Product(101,5,23.5),Product(102,12,24.56),Product(103,100,21.5)};
	for(int i = 0; i < 3; i++)
		Prod[i].total();
	Product::display();
	//int sundea;cin>>sundea;
	return 0;
}
```

(PS:这个程序好像会有几个warning，不过只要不是error，我们就不必在意)

#### 实验 8.3

分析运行程序然后注意友元函数`Time::display`的作用，然后把他放在类外，再在`Time`,`Date`类中将其声明为友元函数。在主函数中再调用`display`函数，并分别引用`Time`和`Date`两个类的对象的私有数据。

大概就是考察如何使用友元函数，即如何在类外调用类内的`private`数据，这个在我的另一篇[文章](https://cybeird.coding.me/cpp/how-to-use-private-out)里有些哦！

这道题的最终代码如下，实际上改动不是很大：

```c++
#include <iostream>
using namespace std;

class Date;

class Time {
	public:
		Time(int, int, int);
		friend void display(Time &, Date &);
	private:
		int hour, minute, sec;
};

class Date {
	public:
		Date(int, int, int);
		friend void display(Time &, Date &);
	private:
		int month, day, year;
};

Time::Time(int h, int m, int s) {
	hour = h;
	minute = m;
	sec = s;
}

void display(Time &t, Date &d) {
	cout << d.month <<"/"<< d.day << "/" << d.year <<endl;
	cout << t.hour <<":"<< t.minute <<":"<< t.sec <<endl;
}

Date::Date(int m, int d, int y) {
	month = m;
	day = d;
	year = y;
}

int main()
{
	Time t1(10, 13, 56);
	Date d1(12, 25, 2004);
	display(t1,d1);
//	int sundea;cin>>sundea;
	return 0;
}
```

#### 实验 8.4

将函数由类内定义改为类外虽然简单但是繁琐

```c++
#include <iostream>
using namespace std;

template<class numtype>				//定义类模板

class Compare {
public:
	Compare(numtype a, numtype b)
	{
		x = a; y = b;
	}
	numtype max();
	numtype min();
private:
	numtype x, y;
};

template <class numtype>
numtype Compare <numtype>::max()
{
	return (x > y) ? x : y;
};
template <class numtype>
numtype Compare <numtype>::min()
{
	return (x < y) ? x : y;
};

int main()
{
	Compare<int> cmp1(3, 7);														//比较整数
	cout << cmp1.max() << " is the Maximum of two interger numbers." << endl;
	cout << cmp1.min() << " is the Minimum of two interger numbers." << endl << endl;
	Compare<float> cmp2(45.78, 93.6);											//比较浮点数
	cout << cmp2.max() << " is the Maximum of two interger numbers." << endl;
	cout << cmp2.min() << " is the Minimum of two interger numbers." << endl << endl;
	Compare<char> cmp3('a', 'A');												//比较字符
	cout << cmp3.max() << " is the Maximum of two interger numbers." << endl;
	cout << cmp3.min() << " is the Minimum of two interger numbers." << endl << endl;
	int sundea; cin >> sundea;
	return 0;
}
```

（PS：这里我出了一个很想当然的错误，具体可以移步[这里](https://cybeird.coding.me/cpp/how-make-model-out)来查看

