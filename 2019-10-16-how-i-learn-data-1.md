---
title: 数据结构实验课の解题报告-Week1
date: 2019-10-09 12:58:50
categories:
- cpp
tags:
- 学习
- 数据结构
- 顺序表
keywords:
description: 第一章的教程又臭又长也没啥难度，也就是搞个对话框，就直接从线性表开始了
---

#### 顺序表运算控制台编程实例

##### 添加头文件 my.h，定义数据类型

```c++
//my.h
#define N 2000
struct  DATE_B
{
  short  year;  //年
  short  month;  //月
  short  day;  //日
  void Set(char s[]);//根据参数s中的日期“yy-mm-dd”字符串  
  //设置成员变量year,month,day的值

};
struct  ELEM
{
  char  num[9];  //学号, 长度8位
  char  name[11];  //姓名, 最多5个汉字
  char  sex;  //性别，'1'=男，'0'=女
  DATE_B  date;  //出生日期
};
struct  TBL
{	ELEM  e[N];	//表容量
	int	cnt;	//记录表中元素个数
	void  DisplayElem();	//显示表中元素
	void  InitTbl();	//初始化表
	void  AddElemProc();	//添加元素处理
	void	  WFile();       //表中元素写到文件
	bool  DeleteElem(int pos);//删除逻辑序号第pos位置的元素
	void  DeleteElemProc();//删除原素处理
	bool  InsertElem(int pos, ELEM &pe);
  //插入元素，参数pos插入位置的逻辑序号，pe为待插入元素
	void  InsertElemProc();//插入原素处理
	void  AddElem(ELEM &a);//添加元素a
	void  InputElem(ELEM &a);//输入元素a的各个属性值
};
```

##### 添加源文件 my.cpp，编写 my.h 中数据类型的成员函数

```c++
//my.cpp
#include "stdio.h"
#include "conio.h"
#include "my.h"

char   s_fname[] = "e:\\abc.xx";	//保存数据的文件，全路径

void  TBL::AddElem(ELEM &a)
{
    e[cnt++] = a;
}
void  TBL::AddElemProc()
{
	ELEM e;
	printf_s("\n追加元素");
	do {
		if (cnt == N) { printf_s("表已满!!!");break; }
		InputElem(e);
		AddElem(e);
		printf_s("\n是否继续(y/n):");
	} while ((_getch() & 0x5f) == 'Y');
}
bool  TBL::DeleteElem(int pos)
{//删除元素
//参数：pos是被删元素的位置
//返回值: 真=删除成功, 否则，失败
	bool  v = false;
	if (pos <= cnt) {
		v = true;
		for (; pos < cnt; pos++)  e[pos - 1] = e[pos];
		cnt--;
	}
	return v;
}
void  TBL::DeleteElemProc()
{
	int  pos;
	printf_s("\n\n删除操作");
	printf_s("\n\n输入删除元素的位置序号:");
	scanf_s("%d", &pos);
	if (DeleteElem(pos))
		printf_s("\n\n操作成功");
	else
		printf_s("\n\n操作失败");
}
bool  TBL::InsertElem(int pos, ELEM &pe)
{//插入操作
//参数：pos=插入位置，e是待插入元素
//返回值：真=插入成功, 否则，失败
	bool val = false;
	int i;
	if (cnt < N && pos <= cnt + 1)
	{	val = true;
		for (i = cnt; i >= pos; i--)  e[i] = e[i - 1];
		e[i] = pe;
		cnt++;
	}
	return val;
}
void  TBL::InsertElemProc()
{
	ELEM e; int pos;
	printf_s("\n\n插入操作");
	printf_s("\n\n输入插入元素的位置序号:");
	scanf_s("%d", &pos);
	InputElem(e);
	if (InsertElem(pos, e))
		printf_s("\n\n操作成功");
	else
		printf_s("\n\n操作失败");
}
void  TBL::InitTbl()//初始化表
{
	FILE  *h;
	cnt = 0;//设置空表
	h = fopen(s_fname, "rb+");
	if (h != NULL)
	{
		this->cnt = fread(this->e, sizeof(ELEM), N, h);
		fclose(h);
	}
}
void  TBL::InputElem(ELEM &a)
{	  char s[11];
	printf_s("\n输入学号:");
	gets_s(a.num);
	printf_s("\n输入姓名:");
	gets_s(a.name);
	printf_s("\n输入性别('1'=男，'0'=女):");
	a.sex=_getch();
	_putch(a.sex);
	a.sex -= '0';
	printf_s("\n出生日期(年-月-日):");
	gets_s(s,11);
	a.date.Set(s);
}
void  TBL::DisplayElem()
{
	int i;
	char sex[][4] = { "女","男" };
	printf_s("\n%15s%12s%8s%10s", "学号", "姓名", "性别", "出生日期");
	for (i = 0; i < cnt; i++)
		printf_s("\n%15s%12s%8s%6d-%d-%d", e[i].num, e[i].name, sex[e[i].sex], e[i].date.year, e[i].date.month, e[i].date.day);
}
void  DATE_B::Set(char s[])
{
	for (year = 0; s[0] != '-'; s++)
		year = year * 10 + s[0] - '0';
	for (month = 0, s++; s[0] != '-'; s++)
		month = month * 10 + s[0] - '0';
	for (day= 0, s++; s[0]; s++)
		day = day * 10 + s[0] - '0';
}
```

#### 添加主函数源文件　main.cpp

```c++
//main.cpp
#include "stdio.h"
#include "conio.h"
#include "my.h"

#define   COUNT    5

char  s_menu[COUNT][30] = { "\n\n1. 追加操作",
				"\n\n2. 删除操作",
				"\n\n3. 插入操作",
				"\n\n4. 列表操作",
				"\n\n0. 退出" };

void   DisplayMenu(char s[][30]);
int   main()
{      TBL   t;    char s;   t.InitTbl();
	for (DisplayMenu(s_menu);; DisplayMenu(s_menu)){ 
    	s = _getch();
        if (s == '0')break;
        switch (s) {
        	case  '1'://追加操作
            	t.AddElemProc();            break;
        	case  '2'://删除操作
            	t.DeleteElemProc();        break;
        	case '3'://插入操作
            	t.InsertElemProc();         break;
        	case '4'://列表操作
            	t.DisplayElem();
    	}
	}
	t.WFile();
	return 0;
}
void   DisplayMenu(char s[][30])
{
	for (int i = 0; i < COUNT; i++)	printf_s(s[i]);
}
```

生成并运行即可

##### 将 my.h 文件中各结构体换成类

```c++
class	DATE_B
{
public:
	short	year,month,day;
	void Set(char s[]);
};

class ELEM
{
public:
	char	num[9];		//学号, 长度8位
	char	name[11];	//姓名, 最多5个汉字
	char	sex;		//性别，0=男，1=女
	DATE_B	date;		//出生日期
};
class TBL
{
	ELEM	e[N];	//表容量
	int	cnt;	//记录表中元素个数
public:
	void	DisplayElem();
	void	InitTbl();
	void	AddElemProc();
	void	WFile(CString Fname);
	bool	DeleteElem(int pos);
	void	DeleteElemProc();
	bool	InsertElem(int pos, ELEM &pe);
	void	InsertElemProc();
	void 	AddElem(ELEM &a);
	void 	InputElem(ELEM &a);
};

```

