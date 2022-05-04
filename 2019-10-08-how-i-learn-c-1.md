---
title: C艹实验课の解题报告-Week1
date: 2019-10-08 21:26:19
categories:
- cpp
tags: 
- 学习
- c++
keywords:
description: 实验课闲的无聊，决定写写博客顺便写写报告
---

C艹实验课の解题报告-Week1

### 实验8 类和对象（一）

#### 实验8.1

将数据成员改为私有，用成员函数来输入输出然后把成员函数放类里，依葫芦画瓢而已，没什么难度

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
using namespace std;

class Time
{
	private:
		int hour;
		int minute;
		int sec;
	public:
		void getin(void)
		{
			cin >> hour;
			cin >> minute;
			cin >> sec;
		}
		void out(void)
		{
			cout << hour << ":" << minute << ":" << sec <<endl;
		}
};
int main()
{
	Time t1;
	t1.getin();
	t1.out();
	//int sundea;cin>>sundea;
	return 0;
}
```

#### 实验 8.2

查错，程序的错误显而易见。即便看不出来也没有关系，直接全打到`IDE`里边运行一下看一下报的错就知道了

##### 含类定义的头文件 student.h

增加一个给成员赋值的函数set_value()

```c++
//student.h
class Student
{
	public:
		void display();
		void set_value();
	private:
		int num;
		char name[20];
		char sex;
};
```

##### 包含成员函数定义的源文件 student.cpp

这块书上的代码忘记使用标准的命名空间了，添上就可以了，然后顺手把赋值函数set_value定义一下即可

```c++
//student.cpp
#include <iostream>
#include "student.h"
using namespace std;   //不然cin cout 会变成未声明的标识符
void Student::display()
{
	cout << "num:" << num << endl;
	cout << "name:" << name << endl;
	cout << "sex:" << sex << endl;
	//printf("num:%d/n",num);
	//printf("name:%s/n",name);
	//printf("sex:%c/n",sex);
}
/*void Student::set_value(int first_num,string first_name,char first_sex)
{
	num = first_num;
	name = first_name;
	sex = first_sex;
}*/
void Student::set_value()
{
	cin >> num;
	cin >> name;
	cin >> sex;
}
```

##### 包含主函数的源文件 main.cpp

这里也要使用标准的命名空间

```c++
//main.cpp
#include <iostream>
#include "student.h"
using namespace std;
int main()
{
	Student stud;
	stud.set_value();
	stud.display();
	//int sundea;cin>>sundea;
	return 0;
}
```

#### 实验 8.3

实验要求写个算长方柱体积的程序，还是算三个的，题目要求的很宽松，随便写写即可

（实际上一个主函数里边for循环就完事了，不过还是照着前边的做法依葫芦画瓢吧）

##### 含类定义的头文件 volume.h

```c++
//volume.h
class Volume
{
	private:
		float height;
		float width;
		float length;
	public:
		void getnum();
		void calculate();
};					//这里的;一定要记得写哦  
```

##### 包含成员函数定义的源文件 volume.cpp

```c++
//volume.cpp
#include <iostream>
#include "volume.h"
using namespace std;
void Volume::getnum()
{
		cin >> length;
		cin >> width;
		cin >> height;
}
void Volume::calculate()
{
	int ans = length * width * height;
	cout << ans <<endl;
}
```

#### 包含主函数的源文件 main.cpp

```c++
//main.cpp
#include <iostream>
#include "volume.h"
using namespace std;
void Volume::getnum()
{
		cin >> length;
		cin >> width;
		cin >> height;
}
void Volume::calculate()
{
	int ans = length * width * height;
	cout << ans <<endl;
}
```