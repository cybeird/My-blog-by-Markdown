---
title: 数据结构实验课の解题报告-Week3
date: 2019-10-12 22:50:10
categories:
- cpp
tags:
- 学习
- 数据结构
- 线性表
keywords:
description: 这个实验课有很多水分，就当我在水贴吧
---

### 线性表对话框编程实例方法介绍(下)

### 类中添加成员函数：

书接上文，继续在类中添加成员函数

#### 添加类`TBL`成员函数

```c++
class TBL   {
	public:
		bool WriteFile(CString fname);
		void DispTbl(CListBox &plist);
		bool DeleteElem(int pos);
		bool InsertElem(int pos, ELEM &a);
		bool AddElem(ELEM &pe);
		void InitTbl(CString path_filename);
		TBL();
		virtual ~TBL();
	private:
		long LoadFile(CString fname);
		ELEM    e[N];
		int	cnt;
};
```

* 初始化表`InitTbl`

```c++
void TBL::InitTbl(CString path_filename) {//初始化表
		cnt=0;	//设置表中元素个数为0，即空表
		CFileFind  x;
		if(x.FindFile(path_filename))	
		//测试文件是否存在，存在装入学生表文件
		cnt=LoadFile(path_filename)/sizeof(ELEM);
}
```

* 装入文件`LoadFile`，该成员函数属性设置为`private`

```c++
long TBL::LoadFile(CString fname) {	//参数: fname为全路径文件名
	//返回值：0=读文件失败，否则，为读取文件的长度
	CFile x_hand;	//定义文件类对象
	long x_size=0;
	if(x_hand.Open((LPCTSTR)fname,CFile::modeRead,NULL))
	{//只读模式打开文件，成功进行读操作
		x_size=x_hand.GetLength();//得到文件长度
		x_hand.Read((char *)t,x_size);
			//读取x_size长度的内容到缓存e数组中
		x_hand.Close();			//关闭文件
	}
	return x_size;
}

```

* 向表中添加元素`AddElem`

即在表尾添加新元素，表长度增1。类`TBL`添加成员函数`AddElem`，属性`public`

```c++
  bool TBL::AddElem(ELEM &pe)
	{//向表中添加元素pe，pe待添加的元素变量引用
	 //返回真，成功。否则，失败
		bool	val=false;
		if(cnt<N)			//表满测试
		{	val=true;		//添加成功标志
			e[cnt++]=pe;
		}
		return	val;
	}
```

* 向表中插入元素`InsertElem`

  表插入，指在表的第i个位置上插入一个值为` x` 的新元素。

  原表长为`n`的表:

  (a1，a2，...，ai-1，ai，ai+1，...，an)
   插入后成为表长为`n+1`的表:
  (a1，a2，...，ai-1，x，ai，ai+1，...，an)
   `i` 的取值范围：`1<=i<=n+1` 。 

+ 类`TBL`添加成员函数`InsertElem` ，属性`public`

```c++
bool TBL::InsertElem(int pos, ELEM &a)
{ //参  数：pos插入位置（从1开始）, a待插入元素变量引用
  //返回值：true插入成功，否则失败
	bool	val=false;	int i;
	if(cnt<N && pos>=1 && pos<=cnt+1)
	{	val=true;	         //插入成功标志
		for(i=cnt;i>=pos;i--)	
			e[i]=e[i-1];    //移位元素
		t[i]=a;	         //插入元素
		cnt++;                 //元素计数增1
	}
	return val;
}   
```

* 删除元素`DeleteElem`

  表删除元素，指将表的第`i`个位置上元素删除。

  原表长为`n`的表:
    (a1，a2，...，ai-1，ai，ai+1，...，an)
  删除后成为表长为`n-1`的表:
    (a1，a2，...，ai-1，ai+1，...，an)
  ` i` 的取值范围：`1<=i<=n` 。

+ 类`TBL`添加成员函数`DeleteElem` ，属性`public`

```c++
bool bool TBL::DeleteElem(int pos)
{ //参  数：pos为删除位置（从1开始）
  //返回值：true插入成功，否则失败
	bool val=false;	int i;
	if(pos<=cnt && pos>0)
	{	val=true;
		for(i=pos-1;i<cnt-1;i++) 
			e[i]=e[i+1]; 	//向前移动元素
		cnt--;			//表中元素-1
	}
	return val;
}
```

* 表中元素输出到列表框`DispTbl` 类`TBL`添加成员函数`DispTbl`，属性`public`

```c++
void TBL::DispTbl(CListBox &plist)
{//参  数： plist列表框控件对象引用；
 //返回值：无
	CString str;
	plist.ResetContent();		//清除列表框内容
	str.Format(“%15s%12s%8s%10s”, “编号”, “姓名”, “性别”, “出生日期”);
	plist.AddString(str);	//组织好表头串，追加到列表框
	for(int i=0;i<cnt;i++)	//逐个元素追加到列表框
	{	str.Format("%15s%12s%8s%18s",e[i].GetNum(),
        e[i].GetName(),e[i].GetSex(),e[i].GetElem().GetDate());
		plist.AddString(str);   //组织好一个串，追加到列表框
	}
}
```

* 将表中数据写入文件中`WriteFile`类`TBL`添加成员函数`WriteFile`，属性`public`

```c++
bool TBL::WriteFile(CString fname)
{	//参数:fname为全路径文件名；返回值：false为写失败，否则写成功
	bool	val=false;
	CFile x_hand;	//文件类对象
	if(!x_hand.Open((LPCTSTR)fname,
                  CFile::modeCreate|CFile::modeWrite,NULL))
		AfxMessageBox("打开或建立文件“"+fname+"”失败!");
	else
	{	//打开或建立文件成功
		x_hand.Write((char *)e,cnt*sizeof(ELEM));//写文件
		x_hand.Close();				//关闭文件
		val=true;
	}
	return val;
}
```

#### 类ELEM和类DATE_B添加内联函数

```c++
class DATE_B  
{public:
	CString GetDate(){ CString s;s.Format("%d-%d-%d",
                      year,month,day);return s;}
	void	SetDate(int y,int m,int d)	{year=y,month=m,day=d;}
	DATE_B();
	virtual ~DATE_B();
};
class ELEM  
{public:
	ELEM();
	virtual ~ELEM();
	char *GetNum()	{	return num;}
	char *GetName()	{	return name;}
	char GetSex()	{	return sex;}
	void SetNum(CString &s)	{	strcpy(num,s);}
	void SetName(CString &s)	{	strcpy(name,s);}
	void SetSex(int a)	{	sex=a;}
	DATE_B &IndexDate()	{	return date;}
};


```

### 为实现表的基本操作，对话框类`DLG_LINEAR_LISTS`的变量、函数设置

#### 添加成员变量

   添加操作状态标识变量`m_flag`、表对象`my_qt`

![添加操作状态.png](https://i.loli.net/2019/10/16/XUORjnqPM7E5NWc.png)

>  注：为了能够识别类型`TBL`，添加`“include TBL.h`

![头文件.png](https://i.loli.net/2019/10/16/OXw5Bjqm96CG2fk.png)

#### 添加成员函数

* 添加成员函数`x_SetAttrItem()`

  函数功能：
      对追加、插入、删除和无操作状态这几个模式，设置编辑框、按钮的属性，即编辑框是否允许输入，按钮点击是否有效及按钮是否可见。
  访问类型： `private`
      说明函数为类的私有成员函数

```c++
void DLG_LINEAR_LISTS::x_SetAttrItem()
{//设置编辑框、按钮操作状态
	m_year="";m_month=""; m_day="";
	m_radio=0;
  m_num="";	m_name="";	m_pos="";
	this->UpdateData(false);		//变量交换到控件
	switch(m_flag)
	{	case 0:
		SET_EDIT_OPTION_MODE(false)//使变灰色不能操作
		mc_pos.EnableWindow(false);
		mc_butt_set.ShowWindow(false);//隐藏控件
		mc_butt_noset.ShowWindow(false);
		SET_BUTTON_OPTION_MODE(true)
		break;
	case 2:				//插入功能状态设置
		SET_EDIT_OPTION_MODE(true)	//设置可操作
		mc_pos.EnableWindow(true);
		mc_butt_set.ShowWindow(true);
		mc_butt_noset.ShowWindow(true);
		SET_BUTTON_OPTION_MODE(false)
		break;
	case 1:				//追加功能状态设置
		SET_EDIT_OPTION_MODE(true)	//设置可操作
		mc_pos.EnableWindow(false);	
                      //追加位置号设置为不可操作
		mc_butt_set.ShowWindow(true);
		mc_butt_noset.ShowWindow(true);
		SET_BUTTON_OPTION_MODE(false)
		break;
	case 3:			//删除功能状态设置
		SET_EDIT_OPTION_MODE(false)
                  //使变灰色，不能操作
		mc_pos.EnableWindow(true); //可操作
		mc_butt_set.ShowWindow(true);
		mc_butt_noset.ShowWindow(true);
		SET_BUTTON_OPTION_MODE(false)
		break;
	}
}

```

上面函数里使用了宏，将下面宏代码添加到DLG_LINEAR_LISTS.cpp文件中，放在
      “// DLG_LINEAR_LISTS 对话框” 的前面

``` c++
#define SET_EDIT_OPTION_MODE(x)	\
		mc_year.EnableWindow(x);\
		mc_month.EnableWindow(x);\
		mc_day.EnableWindow(x);\
		mc_radio1.EnableWindow(x);\
		mc_radio2.EnableWindow(x);\
		mc_num.EnableWindow(x);\
		mc_name.EnableWindow(x);
#define SET_BUTTON_OPTION_MODE(x)	\
		mc_butt_add.EnableWindow(x);\
		mc_butt_delete.EnableWindow(x);\
		mc_butt_insert.EnableWindow(x);\
		mc_butt_cancel.EnableWindow(x);

```

![宏代码](https://i.loli.net/2019/10/16/MovOs9gXHnyCcmF.png)

* 添加成员函数`x_CheckValidity`

  功能：输入数据合法性检测，并将数据存入元素中
  参数：ELEM &pe，为存放数据的元素
  返回值：返回真合法，否则不合法
  访问类型：private

```c++
bool DLG_LINEAR_LISTS::x_CheckValidity(ELEM &pe)
{//输入数据合法性检测
	bool	val=true; 	int m,d;
	switch(m_flag)
	{	case 3:
	case 2:
		if(m_pos=="")
		{	val=false;	break;}
		if(m_flag==3)	break;
	case 1:
	 m=atoi(m_month);	d=atoi(m_day);
	 if(m_num=="" || m_name=="" || m<1 || m>12 || d<1 || d>31)
	 {	val=false;	break;}
		pe.SetNum(m_num);
		pe.SetName(m_name);
		pe.SetSex(m_radio);
	   pe.IndexDate().SetDate(atoi(m_year),m,d);	break;
	}
	return val;
}

```

#### 添加按钮点击消息影射函数

* “追加”按钮点击响应函数`OnBnClickedButtonAdd()`
      功能：使成为追加元素操作模式

```c++
void DLG_LINEAR_LISTS::OnBnClickedButtonAdd()
{// TODO: 在此添加控件通知处理程序代码
	m_flag=1;		//设置为追加元素操作模式
	x_SetAttrItem();//设置编辑框、按钮属性
}

```

* “插入”按钮点击响应函数`OnBnClickedButtonInsert()`
      功能：使成为插入元素操作模式

```c++
void DLG_LINEAR_LISTS::OnBnClickedButtonInsert()
{// TODO: 在此添加控件通知处理程序代码
	m_flag=2;		//设置为插入元素操作模式
	x_SetAttrItem();//设置编辑框、按钮属性
}


```

* “删除”按钮点击响应函数`OnBnClickedButtonDelete()`
      功能：使成为删除元素操作模式

```c++
void DLG_LINEAR_LISTS::OnBnClickedButtonDelete()
{// TODO: 在此添加控件通知处理程序代码
	m_flag=3;		//设置为删除元素操作模式
	x_SetAttrItem();//设置编辑框、按钮属性
}


```

* “返回”按钮点击响应函数`OnBnClickedButtonNoset()`
      功能：使成为无操作模式状态

```c++
void DLG_LINEAR_LISTS::OnBnClickedButtonNoset()
{// TODO: 在此添加控件通知处理程序代码
	m_flag=0;		//设置为无操作模式
	x_SetAttrItem();//设置编辑框、按钮属性
}

```

* “确定”按钮点击响应函数`OnBnClickedButtonSet()`
  功能：输入数据合法性检测。合法，则按对应操作模式，更新表中数据

```c++
void DLG_LINEAR_LISTS:: OnBnClickedButtonSet() 
{	// TODO: 在此添加控件通知处理程序代码
  bool	val=false;//状态，true=成功，false=失败
	ELEM	 e;
	this->UpdateData(TRUE);	//从控件到变量
	if(!x_CheckValidity(e))
	{
		this->MessageBox("数据不正确!!!");
		return;
	}
   	switch(m_flag)
	{case 1:
		if(my_qt.AddElem(e))	val=true;
		else	MessageBox("表已满，追加失败!!!");
		break;                
	case 2:
		if(my_qt.InsertElem(atoi(m_pos),e)) val=true;
		else
	MessageBox("插入位置不合法或表已满，插入失败!!!");
		break;
	case 3:
		if(my_qt.DeleteElem(atoi(m_pos))) val=true;
		else  MessageBox("删除位置不合法，删除失败!!!");
		break;
	}
	if(val) //操作成功
	{	my_qt.DispTbl(mc_list);	this->x_SetAttrItem();}
}

```

* 添加对话框初始化消息影射函数`OnInitDialog()`

      在“类视图”页面，点击“DLG_LINEAR_LISTS”项(左上图所示)后，在出
      

  现如下图页面中，点击重写函数的盒子，图中红色箭头指的小方块， 弹出右图页面，找到`OnInitDialog`项，添加即可。

![添加初始化函数.png](https://i.loli.net/2019/10/16/tsWSB2LPpXfM5Gn.png)

在函数中添加初始化代码:

```c++
m_flag = 0; //设置为无操作状态
my_qt.InitTbl(path_filename);
my_qt.DispTbl(mc_list);    //表的信息从my_qt送到列表框中
this->x_SetAttrItem();//设置操作状态

```

![初始化代码.png](https://i.loli.net/2019/10/16/IQ9AoFsgE7NY3lV.png)

* 通过“类向导”页面，添加`WM_DESTROY`消息映射函数`OnDestroy() `

![消息映射函数.png](https://i.loli.net/2019/10/16/ZlAiMkJIYmdN7sv.png)

在函数中添加代码：

```c++
	my_qt.WriteFile(path_filename);

```

![添加代码1.png](https://i.loli.net/2019/10/16/dZgs6Fpbk2HWlwe.png)

在`DLG_LINEAR_LISTS.cpp`文件开始处，添加

```c++
char path_filename[]="d:\\abc.xx";

```

![添加代码.png](https://i.loli.net/2019/10/16/ErNoHJ357DWd6Kk.png)好了，生成，没有问题，运行程序