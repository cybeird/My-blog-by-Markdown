---
title: 在类的外面调用类的private数据
date: 2019-10-11 20:13:35
categories:
- cpp
tags:
- 学习
- 类
keywords:
description: 一个简单的知识点
---

## 在类的外面调用类的private数据

### 函数的调用

> 将基类中的虚函数定义为public，在派生类中将该虚函数定义为private，则可以通过基类指针调用派生类的private函数

1. 通过类的`public成员函数`调用`private成员函数`:

   即在类内创建一个接口，这种方法也可以用来在类外修改类内的变量，如

   ```c++
   class Sunsea
   {
   	public:
   		void SetA(int _a)//接口（可以从类外设置a的值） {
   			a = _a;
   		}
   	private:
   		int a ;
   };
   ```

2. 通过类的`友元函数`调用该类的`private成员函数`，但是该成员函数必须设为`static`,这样就可以在`友元函数`内通过类名调用，否则无法调用

   > 友元函数用 friend 定义

   ```c++
   #include<iostream>
   using namespace std;
   class Sunsea{
   	public:
        	friend void fun2(); //fun2()设为类Test的友元函数
   	private:
       	static void fun1() {
           	cout<<"fun1"<<endl;
      		}
   };
   void fun2() {
       Sunsea::fun1();
   }
   int main()
   {
       fun2();
       return 0;
   }
   ```

### 变量的调用

实际上变量的调用和函数无太大区别，不过有一点不同的是，变量可以通过指针直接进行指定，可是这里的地方太小我写不下。