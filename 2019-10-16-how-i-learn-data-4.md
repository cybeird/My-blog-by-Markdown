---
title: 数据结构实验课の解题报告-Week4
date: 2019-10-16 21:33:01
categories:
- cpp
tags:
- 学习
- 数据结构
- 二叉树
keywords:
description: 这次的实验相对简单，这算是上半部分，仅仅只是操作界面及其相关，功能还尚未加入
---

## 二叉树遍历基于对话框编程实现

### 创建对话框工程

1. 运行VS，建立对话框工程，工程名为`BTree`

   > 这个名字命名还是很重要的，不然后边代码不好抄了

2. 删除窗体上的提示、“确定”按钮；将“取消”按钮的标题改为“退出”；

3. 更改窗体字体字号，选择“宋体”，“小四号字”。      

4. 在窗体上添加控件，并设置属性，调整布局。如下所示。

![界面文件.png](https://i.loli.net/2019/10/16/Cxdih7ZUwbHV1l9.png)

#### 具体设置：

  a) 放置一个组合框`Combo Box`控件，其属性设置如下：

| Type     | Sort  | ID         |
| -------- | ----- | ---------- |
| 下拉列表 | false | IDC_COMBO1 |

  b) 放置一个`Group Box`、一个`EditControl`、一个`Button`控件，其属性设置如下：
​    ● Group Box”控件属性设置
​                **Caption**修改为**添加结点**
​    ● EditControl控件属性设置

| ID           | Number |
| ------------ | ------ |
| IDC_EDIT_VAL | True   |

​    ● Button控件属性设置

| ID             | Caption  |
| -------------- | -------- |
| IDC_BUTTON_ADD | 确认添加 |

5. 控件绑定变量

​    只设置控制型变量，访问类型均设置为`private`

修改`BTreeDlg.g`

```cpp
private:
	CListBox mc_list;
	CStatic mc_visit;
	CComboBox mc_box;
	CEdit mc_edit;
	BIT_TREE bt
```

### 建立新类NODE、BIT_TREE

在**类视图**中添加类，类名分别为`NODE`,`BIT_TREE`

1. 类`NODE`添加*成员变量*

​    二叉链表结点类型，其元素类型为无符号整型。
​    该类不添加成员函数，其私有成员在二叉树类BIT_TREE的成员函数中直接引用。为此，需要将类BIT_TREE声明为类NODE的友元类。

```cpp
//NODE.h
#pragma once

typedef UINT	ELEM;

class NODE
{
	friend class BIT_TREE;
public:
	NODE(void);
	~NODE(void);
private:
	ELEM	e;
	NODE *lc, *rc;
};
```

2. 类`BIT_TREE`添加*成员变量*

```cpp
private:
    NODE   ht;  //二叉树头结点
```

3. 类`BIT_TREE`添加*成员函数*

```cpp
//BIT_TREE.h
#include "NODE.h"

#pragma once

class BIT_TREE
{
public:
	BIT_TREE(void);
	~BIT_TREE(void);
	void InsertElem(ELEM pe);
	void PreVisit(NODE *t, CListBox &mbox);
	void OrVisit(NODE *t, CListBox &mbox);
	void LastVisit(NODE *t, CListBox &mbox);
	void FreeTree(NODE *t);

	int GetLeafNodeNum(NODE *t);
	int GetTreeHeight(NODE *t);

	NODE* GetTreeBoot() { return ht.lc; }

private:
    NODE   ht;  //二叉树头结点
};
```

4. 在`BIT_TREE.cpp`中对函数定义

```cpp
#include "StdAfx.h"
#include "BIT_TREE.h"
#include "STACK_OR_QUENE.h"

#define VISIT_NODE(x,y) CString str;str.Format("%10d",x->e);y.AddString(str);


BIT_TREE::BIT_TREE()
{//在构造函数里初始化二叉树
	ht.lc = NULL;	//设置空树
	ht.e = -1;		//元素域存入无符号最大值
}

BIT_TREE::~BIT_TREE(void)
{
}

void BIT_TREE::InsertElem(ELEM pe)
{//向树中插入结点，pe为待插入元素
	NODE *p, *s;	s = new(NODE);	s->e = pe;
	s->lc = s->rc = NULL;//插入结点总是叶结点
	for (p = &ht;;)//寻找待插入结点双亲结点指针p
	{	if (p->e < pe)
		{//待插入结点元素值大于p指向结点元素值时，插入在p结点为根的右子树上
		    if (p->rc)p = p->rc;//p的右子女存在，以p的右子女为根
		    else
		   {  p->rc = s; break;  }//待插入结点作为p的右子女，插入完成
		}
		else
      {//待插入结点元素值小于等于p指向结点元素值时，插入在p结点为根的左子树上
		   if (p->lc)p = p->lc;//p的左子女存在，以p的左子女为根
          else  { p->lc = s; break;}//待插入结点作为p的左子女，插入完成
      }
   }
}

void BIT_TREE::PreVisit(NODE *t, CListBox &mbox)
{//先序遍历
	if (t)
	{	VISIT_NODE(t, mbox)//访问结点t
		PreVisit(t->lc, mbox);//先序遍历左子树
		PreVisit(t->rc, mbox);//先序遍历右子树
	}
}

void BIT_TREE::OrVisit(NODE *t, CListBox &mbox)
{//中序遍历
	if (t)
	{	OrVisit(t->lc, mbox);//中序遍历左子树
		VISIT_NODE(t, mbox)//访问结点t
		OrVisit(t->rc, mbox);//中序遍历右子树
	}
}

void BIT_TREE::LastVisit(NODE *t, CListBox &mbox)
{//后序遍历
	if (t)
	{	LastVisit(t->lc, mbox);//后序遍历左子树
		LastVisit(t->rc, mbox);//后序遍历右子树
		VISIT_NODE(t, mbox)//访问结点t
	}
}
void BIT_TREE::FreeTree(NODE *t)
{//释放二叉链表，按后序遍历编写
	if (t)
	{	FreeTree(t->lc);//释放左子树
		FreeTree(t->rc);//释放右子树
		free(t);//释放根结点
	}
}

int BIT_TREE::GetLeafNodeNum(NODE *t)
{	int n = 0;
	if (t)
	{	n = GetLeafNodeNum(t->lc);	n += GetLeafNodeNum(t->rc);
		if (t->lc == NULL && t->rc == NULL) n++;
	}
	return n;
}

int BIT_TREE::GetTreeHeight(NODE *t)
{	int lth=0, rth;
	if (t)
	{	lth = GetTreeHeight(t->lc);	rth = GetTreeHeight(t->rc);
		if (lth < rth) lth = rth;
		lth++;
	}
	return lth;
}
```

### 添加操作使用的常量数据定义

在`BTreeDlg.cpp`文件中添加以下定义

```cpp
#define		LEN	7
char  sss[][31] = { "先序遍历","中序遍历","后序遍历",
		"广度遍历",
		"非递归先序遍历","非递归中序遍历","非递归后序遍历" };
#define		NUM	18
ELEM	as[] = { 76,42,32,17, 3,98,105,89,73,54,48,20,
			  18,10, 7, 4,38,26 };
```

需要在`BTreeDlg.cpp`文件中开始处添加

``` cpp
#include "NODE.h"
```

### 类`CBTreeDlg`添加成员变量

```cpp
private:
	BIT_TREE	bt;
```

需要在`BTreeDlg.h`文件中添加

```cpp
#include "bit_tree.h"

```

### 对话框初始化

 在`BOOL CBTreeDlg::OnInitDialog()`函数中添加代码(`BTreeDlg.cpp`)

```cpp
// TODO: 在此添加额外的初始化代码
int i;
for (i = 0; i < LEN; i++)
    mc_box.AddString(sss[i]);
mc_box.SetCurSel(1);

for (i = 0; i < NUM; i++)
    bt.InsertElem(as[i]);
OnSelchangeCombo1();

```

> 设置工程“字符集”属性，通过解决方案资源管理器，设置为多字符集
>
> 到此，先看看工程由没有问题，生成工程，没有问题，则运行之.
