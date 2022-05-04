---
title: 『3』我要入门！让你们见识一下树和二叉树的力量！
date: 2016-10-23 09:50:54
tags: [我要入门,数据结构基础,c++,Binary Tree]
categories: cpp
description:
	恩，从标题就可以略知一二了。 
---
　　二叉树的递归定义如下：二叉树要么为空，要么由根节点(root)、左子树(left subtree)和右子树(right subtree)组成，而左子树和右子树分别是一棵二叉树。

<!--more-->
	
{% blockquote %}
<B>TIPS:</B> 在计算机中，树一般是“倒置”的，即根在上，叶子在下。
{% endblockquote %}
	
　　树(tree)和二叉树类似，区别在于每个节点不一定只有两棵子树。比如说这个神奇网站的categories也可以看做一个树状结构。
　　而不管是二叉树还是树，每一个非根节点都有一个父亲(father),也称父节点。
	
## 二叉树的编号
	
　　对于一个节点k，其左子节点、右子节点的编号分别是2k和2k+1。
	
## 二叉树的层次遍历
	
### 题目简述：
　　输入二叉树的每一个节点的信息，建树完毕后，按照层次顺序遍历这棵树，然后将每一个节点的权值给输出来！
　　注意：如果从根到某个叶节点的路径上有的节点没有在输入中给出或者给出超过一次，应该输出“not complete”.节点数不超过256个！
	
### 样例输入:
{% blockquote %}
	(11,LL) (7,LLL) (8,R) (5,) (4,L) (13,RL) (2,LLR) (1,RRR) (4,RR) () 
	(3,L) (4,R) ()
{% endblockquote %}	
	
### 样例输出:
{% blockquote %}
	5 4 8 11 13 4 7 2 1
	not complete
{% endblockquote %}	
	
### 题目分析：
#### ①
　　由于这道题中已限制结点最多有256个。若各个节点形成一条链，最后一个链的编号将会变得无比巨大！就算用高精度保存编号，数组也开不下。
　　所以说，我们需要采用动态结构，根据需要来建立新的结点，然后将其组织成一棵树。首先，来看一看输入成分和主程序：
	
```cpp
	char s[maxn];									//保存读入结点
	bool read_input(){
		failed = false;
		root = newnode();							//创建根结点
		for(;;){
			if(scanf("%s", s) != 1) return false;	//整个输入结束
			is(!strcmp(s, "()")) break;				//读到结束标志，退出循环(若s == "()"则返回0,s < "()"返回负数)
			int v;
			sscanf(&s[1], "%d", &v);				//读入结点值
			addnode(v, strchr(s, ',')+1);			//查找逗号，然后插入结点
		}
		return ture;
	}
```
	
　　嗯，大意就是:不断读入结点，如果在读到空括号之前文件结束，则返回0(这样，在main函数里就能知道输入结束了)。而且这里两次用到了C语言的灵活性。
1) 在代码第九行的位置里，若读到的结点是(11,LL),则&s[1]所对应的字符串是“11,LL)”。
	
{% blockquote %}
<B>TIPS:</B> 可以把任意“指向字符的指针”看成是字符串，从该位置开始，直到字符“\0”。
{% endblockquote %}
	
2) 函数 strchr(s, ',') 返回字符串 s 中从左往右第一个字符 “,” 的指针，因此 strchr(s, ',')+1 所对应的字符串是 “LL)”。这样，实际调用的是 addnode(11, "LL)")。

#### ②
　　接下来就是最关键的地方了!没错：二叉树的结点定义和操作。首先，需要定义一个称为Node的结构体，并且对应整棵二叉树的树根root:
	
```cpp
	//结点类型
	struct Node{										  //结点值
		bool have_value;
		int v;
		Node *left, *right;
		Node():have_value(false),left(NULL),right(NULL){} //构造函数
	};

	Node* root;											  //二叉树的根节点
```
	
　　由于二叉树是递归定义的，其左右子结点类型都是“指向结点类型的指针”。也就是说，如果结点的类型是Node，则左右子结点的类型都是Node*。
	
{% blockquote %}
<B>TIPS:</B> 如果要定义一颗二叉树，一般都是定义一个“结点”类型的 struct (如叫Node)，然后保存树根的指针(如 Node* root)
{% endblockquote %}

　　每次需要一个新的 Node 时，都要用 new 运算符申请内存，并执行构造函数。下面把申请新结点的操作封装到 newnode 函数中：
	
```cpp
	Node* newnode() { return new Node(); }
```

{% blockquote %}
<B>TIPS:</B> 可以用 new 运算符申请空间并执行构造函数。如果返回值为 NULL，说明空间不足，申请失败。
{% endblockquote %}

#### ③
　　然后就是在 read_input 中调用的 addnode 函数。它按照移动序列行走，目标不存在时调用 newnode 来创建新结点。

```cpp
	
	void addnode(int v, char* s){
		int n = strlen(s);
		Node* u = root;											//从根节点开始往下走
		for(int i = 0; i <= n; i++)
			if(s[i] == 'L'){
				if(u->left == 'L') u->Left = newnode();			//结点不存在，建立新结点
				u = u->left;									//往左走
			} else if(s[i] == 'R'){
				if(u->right == NULL) u -> right = newnode();
				u = u->right;
			}													//忽略其他情况，即最后那个多余的右括号
			if(u->have_value) failed = ture;					//已经赋过值，表明输入有误
			u->v = v;
			u->have_value = ture;								//别忘记做标记
	}
```

#### ④
　　紧接着就是按照层次顺序遍历这棵。此处使用一个队列来完成这个队伍，初始时只有一个根节点，然后每次取出一个结点，就把它的左右子结点(如果存在)放进队列。

```cpp
	bool bfs(vector<int>& ans){
	queue<Node*> q;
	ans.clear();
	q.push(root);								//初始时只有一个根节点
	while(!q.empty()){
		Node* u = q.front(); q.pop();
		if(!u->have_value) return false;		//有结点没有被赋值
		ans.push_back(u->v);					//增加到输出序列尾部
		if(u->left != NULL) q.push(u->left);	//把左子结点(如果有)放进队列
		if(u->right != NULL) q.push(u->right);	//把右子结点(如果有)放进队列
	}
	return true;								//输入正确
}
```

　　这样遍历二叉树的方法称为宽度优先遍历(Breadth-First Search, BFS)。

> **TIPS:**可以用队列实现二叉树的层次遍历。这个方法还有一个名字，叫做宽度优先遍历(Breadth-First Search, BFS)。

　　上面的程序在功能上是正确的，但是有一个小小的技术问题:在输入一组新数据时，没有释放上一棵二叉树所申请的内存空间。一旦执行了 root = newnode() ，就再也无法访问到那些内存了，尽管那些内存物理上仍然存在。当然，从技术上说，还是可以访问到那些内存的，如果能“猜到”那些地址。之所以说“访问不到”，是因为丢失了指向这些内存的指针。
　　有一个专业术语用来描述这样的情况:内存泄漏(memory leak)————它意味着有些内存被白白浪费了。在实际运行的过程中，一般很难看出这个问题:在很多情况下，内存空间都不会很紧张，浪费一些空间后，程序还是可以正常运行；况且在整个程序结束后，该程序占用的空间会被操作系统全部回收，包括泄漏的那些。

> **TIPS:** 如果程序动态申请内存，请注意内存泄漏。程序执行完毕后，操作系统会回收该程序申请的所有内存(包括泄漏的)，所以在算法竞赛中内存泄漏往往不会造成什么影响。但是从专业素养的角度考虑，请从现在养成好习惯，对内存泄漏保持警惕。

#### ⑤
　　下面是释放一棵二叉树的代码，请在“root=newnode()”之前加一行“remove_tree(root)”:
```cpp
	void remove_tree(Node* u){		//提前判断比较稳妥
		if(u == NULL) return;		//递归释放左子树的空间
		remove_tree(u->left);		//递归释放右子树的空间
		remove_tree(u->reght);		//调用u的析构函数并释放u结点本身的内存
		delete u;
	}
```

#### ⑥
　　<!--在学习了新的语法后可以干更多的事情了O(∩_∩)O-->
　　二叉树并不一定要用指针实现。接下来，把指针完全去掉。首先还是按每个节点编号但不是按照从上到下的顺序，而是按照结点的生成顺序。用计数器`cnt`表示已存在的结点编号的最大值yinci因此`newnode`的函数需要改成这样:
```cpp
const int root = 1;
void newnode(){
    left[root] = right[root] = 0;
    have_value[root] = false;
    cnt = root;
}
```
　　上面的`newnode()`是用来替代前面的`remove_tree(root)`和`root = newnode()`两条语句 的:由于没有了动态内存的申请和释放，只需要重置结点计数器和根结点的左右子树了。
　　接下来，就仅仅只需要把所有Node*类型改成int类型，然后把结点结构中的成员变量改成全局数组(例如，u->left和u->right分别改成right[u]和left[u]就行了)
　　<!--完结撒花！φ(≥ω≤*)♪ -->
## 二叉树的递归遍历
　　对于二叉树T，可以递归定义它的先序遍历、中序遍历和后序遍历，如下所示:
　　   - PreOrder(T)=T的根结点+PreOrder(T的左子树)+PreOrder(T的右子树)
　　   - InOrder(T)=InOrder(T的左子树)+T的根结点+InOrder(T的右子树)
　　   - PostOrder(T)=T的根结点+PostOrder(T的左子树)+PostOrder(T的右子树)
　　其中加号表示字符串连接运算。而这三种遍历都属于递归遍历，或者说深度优先搜索遍历(`Depth-First Search`,`DFS`)，因为它总是优先往深度访问。

> **TIPS:**二叉树有三种深度优先遍历:先序遍历、中序遍历和后序遍历

### 题目简述
　　给一棵点带权(权值各不相同，就是小于 `10000` 的正整数)的二叉树中序和后序遍历，找一个叶子使得它到根的路径上的权和最小。如果有多解，该叶子本身的权应尽量小。输入中每两行表示一棵树，其中第一行为中序遍历，第二行为后序遍历。

### 样例输入
> 3 2 1 4 5 7 6
> 3 1 2 5 6 7 4
> 7 8 11 3 5 16 12 18
> 8 3 11 7 16 18 12 5
> 255
> 255

### 样例输出
> 1
> 3
> 255

### 题目分析
　　后序遍历的最后一个字符就是根，因此只需在中序遍历中找到它(因为树中权值各不相同)，就可以知道左右字数的中序遍历和后序遍历了。这样可以先把二叉树构造出来，然后再执行一次递归遍历，找到最优解。

> **TIPS:**给定二叉树的中序遍历和后序遍历，可以构造出这棵二叉树。方法是根据后序遍历找到树根，然后在中序遍历中找到树根，从而找出左右子树的结点列表，然后递归构造左右子树。

代码如下:(另外，也可以在递归的同时统计最优解，不过程序稍微复杂一点)
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <sstream>
using namespace std;

//因为各个结点的权值不同，从而可以直接用权值来当做结点编号
const int maxv = 10000 + 10;
int in_order[maxv], post_order[maxv], lch[maxv], rch[maxv], n;

bool read_list(int* a){
	string line;
	if(!getline(cin, line)) return false;
	getline(cin, line)
	n = 0;
	int x;
	while(ss >> x) a[n++] = x;
	return n > 0;
}

//把in_order[L1..R1]和post_order[L2..R2]建成一棵二叉树，返回树根
int build(int L1, int R1, int L2, int R2){
	if(L1 > R1) return 0; //空树
	int root = post_order[R2];
	int p = L1;
	while(in_order[p] != root) p++;
	int cnt = p - L1; //左子树的结点个数
	lch[root] = build(L1,  p-1, L2,     L2+cnt-1);
	lch[root] = build(p+1, R1,  L2+cnt, R2-1);
	return root;
}

int best, best_sum; //目前为止的最优解和对应的权和

void dfs(int u, int sum) {
	sum += u;
	if(!lch[u] && !rch[u]) { //叶子
		if(sum < best_sum || (sum == best_sum && u < best)) {
			best = u;
			best_sum = sum;
		}
	}
	if(lch[u]) dfs(lch[u], sum);
	if(rch[u]) dfs(rch[u], sum);
}

int main()
{
	while(read_list(in_order)) {
		read_list(post_order);
		build(0, n-1, 0, n-1);
		best_num = 1234567890;
		dfs(post_order[n-1], 0);
		cout << best << "\n";
	}
	return 0;
}
```