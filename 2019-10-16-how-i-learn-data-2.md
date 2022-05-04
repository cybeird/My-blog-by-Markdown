---
title: 数据结构实验课の解题报告-Week2
date: 2019-10-10 17:09:36
categories:
- cpp
tags:
- 学习
- 线性表
- 数据结构
keywords:
description: 漫长而又无可奈何
---

### 线性表对话框编程实例方法介绍(上)

1. 运行VS，建立对话框工程，工程名为`STBL`

2. 删除窗体上的提示、`确定`按钮；将`取消`按钮的标题改为`退出`

3. 添加一个按钮，标题设置为`基本操作`，ID设置为`IDC_BUTTON_OPTION`

4. 更改窗体字体大小

   ![1571626064851.png](https://i.loli.net/2019/10/10/9epGbClJQA3UNoV.png)

   鼠标右键点击窗体非控件区域，在弹出页面中点击`属性`项，在弹出属性页中，选择`宋体`，及`小四号字`

5. 插入新对话框

   在“资源视图”选页中，鼠标右键点击`Dialog`项，从弹出菜单中点选`插入 Dialog`项后，即出现对话框新窗体。

   ![1571626039993.png](https://i.loli.net/2019/10/10/OD6TUA5CuHMcbn2.png)

   删除窗体上`确定`按钮；`取消`按钮的标题改为`退出`

6. 设置新对话框属性

   设置ID为：`IDD_DIALOG_LINEAR_LISTS`
   标题改为：`基本操作`
   设置字体为：`小四号字`

7. 新对话框建立新类

   鼠标右键点击窗体非控件区域，点选`添加类`选项，在新页面`类名: `栏输入类名称`DLG_LINEAR_LISTS`，按`确定`按钮

8. 在窗体上添加控件，并设置属性，调整布局

![1571625995790.png](https://i.loli.net/2019/10/10/Y1VwLg5kyQH3rpn.png)

#### 具体设置：

1. 放置三个`Button`控件，和一个`Group Box`控件    
   - 三个`Button`控件，属性设置对应如下：

| Caption | ID                |
| ------- | ----------------- |
| 删除    | IDC_BUTTON_DELETE |
| 插入    | IDC_BUTTON_INSERT |
| 追加    | IDC_BUTTON_ADD    |

- `Group Box`控件属性设置

| Caption      |
| ------------ |
| 选择操作功能 |

- 加上保留的`退出`按钮，构成一个整体
- `Group Box`属性的`Caption`设置为：`输入数据`

2. 放置三个`StaticText`和三个`EditControl`
   - 三个`StaticText`属性设置：

| Caption |
| ------- |
| 位置：  |
| 编号：  |
| 姓名：  |

- 三个`EditControl`属性设置：

| ID                        | Number |
| ------------------------- | ------ |
| 对应位置行  IDC_EDIT_POS  | True   |
| 对应编号行  IDC_EDIT_NUM  | True   |
| 对应姓名行  IDC_EDIT_NAME | False  |

3. 放置两个`StaticText`、两个`RadioButton`、一个`Group Box`
   - 两个`StaticText`属性设置： Caption分别设置为： `男`、`女`
   - 两个`RadioButton`属性设置：
     `Caption`设置为 ，即删除标题内容
     `Group`均设置为`True``
   - ``Group Box`的Caption设置为：`性别`

4. 放置三个`StaticText`、三个`EditControl`和一个`Group Box`

   - 三个`StaticText`属性设置：

     `Caption`分别设置为： `年`、`月`、`日`

   - ###### `Group Box`属性设置
     
     `Caption`设置为：`出生日期`
`Hoirzontal Alignment`设置为： `Center ` 
     
- 三个`EditControl`属性设置
  
     

| ID             | Number |
| -------------- | ------ |
| IDC_EDIT_YEAR  | True   |
| IDC_EDIT_MONTH | True   |
| IDC_EDIT_DAY   | True   |

5. 放置两个`Button`控件，和一个`Group Box`控件
   - 两个`Button`属性设置：
         Caption分别设置为：`确定`、`返回`
         ID分别设置为：`IDC_BUTTON_SET`、`IDC_BUTTON_NOSET`
6. 放置一个`ListBox`，即图中右边白色方框，其属性中的`Sort`设置为`false`

##### 设置完成　



9. 编辑框控件绑定变量

   每个编辑框控件分别设置两类变量, 值变量和控制变量，值变量类型均选择`Cstring`，访问类型均设置为`private`，后面其它绑定变量也是这样

| 控件ID         | 值变量  | 控制变量 |
| -------------- | ------- | -------- |
| IDC_EDIT_POS   | m_pos   | mc_pos   |
| IDC_EDIT_NUM   | m_num   | mc_num   |
| IDC_EDIT_NAME  | m_name  | mc_name  |
| IDC_EDIT_YEAR  | m_year  | mc_year  |
| IDC_EDIT_MONTH | m_month | mc_month |
| IDC_EDIT_DAY   | m_day   | mc_day   |

10. `RadioButton`控件绑定变量

    先设置控制类型变量，设置好后，将`IDC_RADIO2`属性的`group`项改为`false`，再设置值变量

| **控件**ID | **值变量** | **控制变量** |
| ---------- | ---------- | ------------ |
| IDC_RADIO1 | m_radio    | mc_radio1    |
| IDC_RADIO2 |            | mc_radio2    |

11. 其它控件绑定变量

| 控件ID            | **控制变量**   |
| ----------------- | -------------- |
| IDC_LIST1         | mc_list        |
| IDC_BUTTON_DELETE | mc_butt_delete |
| IDC_BUTTON_INSERT | mc_butt_insert |
| IDC_BUTTON_ADD    | mc_butt_add    |
| IDC_BUTTON_NOSET  | mc_butt_noset  |
| IDC_BUTTON_SET    | mc_butt_set    |
| IDCANCEL          | mc_butt_cancel |

12. 为主对话框“基本操作”按钮添加响应函数，用来弹出新对话框

    通过类向导或双击按钮，添加按钮响应函数`OnBnClickedButtonOption()`

    编写代码：

    ```c++
    void CstblDlg::OnBnClickedButtonOption()
    {	// TODO: Add your control notification handler code here
    		DLG_LINEAR_LISTS	a;	//定义对话框类对象
    		a.DoModal();	//调用成员函数激活对话框
    }
    ```

    在函数`OnBnClickedButtonOption()`所在文件的开始处添加类型声明：

    ```c++
    #include "DLG_LINEAR_LISTS.h"
    ```

至此，界面工作已完成。好了，运行程序，若没有问题，备份工程，即整个文件夹，以便后面添加代码，出现大的问题时，可以用备份继续做。

13. 建立三个新类`DATE_B`、`ELEM`、`TBL` 

    在`类视图`对应页面，右键点击最上面一项(右图中蓝色项)，从弹出菜单中选择`添加`、`类`，如右图所示。

![1570713159202.png](https://i.loli.net/2019/10/10/m3hkbFIzaGPY6Nr.png)

在弹出页面中，`类名`栏输入`DATE_B`按确定按钮，建立了新的类——`DATE_B`,`ELEM`,`TBL`两个类构建方法相同

![1570713271593.png](https://i.loli.net/2019/10/10/l3WjnBAEaX8vqrV.png)

14. 添加成员变量

​      在“类视图”对应页面，右键点击最上面一项(右图中蓝色项)，从弹出菜单中选择“添加”、“添加变量”，  如右图所示。

![1570713334218.png](https://i.loli.net/2019/10/10/3JYt7TQkdNxEmH4.png)

​      在新页面中，填写变量的名称、类型并设置访问权限。

![1570713340803.png](https://i.loli.net/2019/10/10/qGc9ZWDMKONtiCa.png)

​       当然，添加变量简单的方法，是在类定义中直接填写。在“类视图”页面，双击类名，即出现对应类的定义文件。

- 类DATE_B添加成员变量

| 名称  | 类型  | 访问权限 |
| ----- | ----- | -------- |
| year  | short | private  |
| month | short | private  |
| day   | short | private  |

- 给类ELEM添加成员变量

```c++
#include "DATE_B.h"

class ELEM
{
    public:
    	ELEM();
    	~ELEM();
    private:
    	char num[9];
    	char name[11];
    	DATE_B date;
    	char sex;
};
```

> 注： 性别成员用一个char类型变量，不用数组。男、女用1和0标识

- 类TBL添加成员变量

```c++
#include "ELEM.h"
#define N 2000

class TBL
{
    public:
    	TBL();
    	~TBL();
    private:
    	ELEM e[N];
    	int cnt;
};
```

15. 向类中添加成员函数

    可以像添加变量一样，通过界面设置添加，也可以直接添加，函数声明填写在对应`.h文件`的类定义中，函数体填写在对应`.cpp文件`中。

![1570713929346.png](https://i.loli.net/2019/10/10/hrGKxXYScPuW9RT.png)