---
title: '『1』我要入门！[UVa 514](TOWQs)'
tags:
  - cpp
  - TOWQs
  - Trip Of WaterQuestions
  - 我要入门
  - 数据结构基础
  - 栈
  - 正常的标题
id: 985
categories:
  - cpp
date: 2016-10-14 10:10:46
---

好的，今天就是要先走一遍这[一道题目](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&amp;Itemid=8&amp;page=show_problem&amp;problem=455)。恩，就是简单的运用一下栈(stack)而已；<!--more-->
> ### 题目描述：
> 
> 某城市有一个火车站，有n节车厢从A方向驶入车站，按进站的顺序编号为1-n.你的任务是判断是否能让它们按照某种特定的顺序进入B方向的铁轨并驶入车站。例如，出栈顺序（5 4 1 2 3）是不可能的，但是（5 4 3 2 1）是可能的。
> 
> 
> ### **题目分析：**
> 
> 为了重组车厢，借助中转站，对于每个车厢，一旦从A移入C就不能回到A了，一旦从C移入B，就不能回到C了，意思就是A-&gt;C和C-&gt;B。而且在中转站C中，车厢符合后进先出的原则。故这里可以看做为一个栈。
> 
> 
> ![](http://img.blog.csdn.net/20140803091134595)
恩，我实在是找不到中文的题目描述了，只好把入门经典的原题目描述给粘过来了。

嗯，相信大家第一眼看到这道题目就是用栈来解决，而我们的c++刚好有一个 stack 的头文件，紧接着，神奇的事情发生了！没错，这道题就写出来了！(嗯，并不是逗比)

好了，废话不多说，看代码！
<pre style="color:#000000;background:#f1f0f0;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">iostream</span><span style="color:#800000;">&gt;</span>
<span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">cstdio</span><span style="color:#800000;">&gt;</span>
<span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">cstring</span><span style="color:#800000;">&gt;</span>
<span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">algorithm</span><span style="color:#800000;">&gt;</span>
<span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">stack</span><span style="color:#800000;">&gt;</span>
<span style="color:#400000;font-weight:bold;">using</span> <span style="color:#400000;font-weight:bold;">namespace</span> <span style="color:#00dddd;">std</span><span style="color:#806030;">;</span>
<span style="color:#400000;font-weight:bold;">const</span> <span style="color:#400000;font-weight:bold;">int</span> MAXN <span style="color:#806030;">=</span> <span style="color:#c00000;">1000</span> <span style="color:#806030;">+</span> <span style="color:#c00000;">10</span><span style="color:#806030;">;</span>
<span style="color:#400000;font-weight:bold;">int</span> n<span style="color:#806030;">,</span> rail<span style="color:#806030;">[</span>MAXN<span style="color:#806030;">]</span><span style="color:#806030;">;</span> 
<span style="color:#400000;font-weight:bold;">int</span> <span style="color:#800000;font-weight:bold;">main</span><span style="color:#806030;">(</span><span style="color:#806030;">)</span>
<span style="color:#806030;">{</span>
	<span style="color:#400000;font-weight:bold;">while</span><span style="color:#806030;">(</span><span style="color:#800040;">scanf</span><span style="color:#806030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#806030;">,</span> <span style="color:#806030;">&amp;</span>n<span style="color:#806030;">)</span> <span style="color:#806030;">=</span><span style="color:#806030;">=</span> <span style="color:#c00000;">1</span> <span style="color:#806030;">&amp;</span><span style="color:#806030;">&amp;</span> n<span style="color:#806030;">)</span><span style="color:#806030;">{</span>
		<span style="color:#800040;">stack</span> s<span style="color:#806030;">;</span>
		<span style="color:#400000;font-weight:bold;">int</span> A <span style="color:#806030;">=</span> <span style="color:#c00000;">1</span><span style="color:#806030;">,</span> B <span style="color:#806030;">=</span> <span style="color:#c00000;">1</span><span style="color:#806030;">;</span>
		<span style="color:#400000;font-weight:bold;">for</span><span style="color:#806030;">(</span><span style="color:#400000;font-weight:bold;">int</span> i <span style="color:#806030;">=</span> <span style="color:#c00000;">1</span><span style="color:#806030;">;</span> i <span style="color:#806030;">&lt;</span><span style="color:#806030;">=</span> n<span style="color:#806030;">;</span> i<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">)</span>
			<span style="color:#800040;">scanf</span><span style="color:#806030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#806030;">,</span> <span style="color:#806030;">&amp;</span>rail<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">)</span><span style="color:#806030;">;</span>	<span style="color:#c34e00;">//读入出站时车厢编号 </span>
		<span style="color:#400000;font-weight:bold;">int</span> ok <span style="color:#806030;">=</span> <span style="color:#c00000;">1</span><span style="color:#806030;">;</span>
		<span style="color:#400000;font-weight:bold;">while</span><span style="color:#806030;">(</span>B <span style="color:#806030;">&lt;</span><span style="color:#806030;">=</span> n<span style="color:#806030;">)</span><span style="color:#806030;">{</span>
			<span style="color:#400000;font-weight:bold;">if</span><span style="color:#806030;">(</span>A <span style="color:#806030;">=</span><span style="color:#806030;">=</span> rail<span style="color:#806030;">[</span>B<span style="color:#806030;">]</span><span style="color:#806030;">)</span> <span style="color:#806030;">{</span> A<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">;</span> B<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">;</span> <span style="color:#806030;">}</span>  <span style="color:#c34e00;">//若A中第一个满足，则出 </span>
			<span style="color:#400000;font-weight:bold;">else</span> <span style="color:#400000;font-weight:bold;">if</span><span style="color:#806030;">(</span><span style="color:#806030;">!</span>s<span style="color:#806030;">.</span>empty<span style="color:#806030;">(</span><span style="color:#806030;">)</span> <span style="color:#806030;">&amp;</span><span style="color:#806030;">&amp;</span> s<span style="color:#806030;">.</span>top<span style="color:#806030;">(</span><span style="color:#806030;">)</span> <span style="color:#806030;">=</span><span style="color:#806030;">=</span> rail<span style="color:#806030;">[</span>B<span style="color:#806030;">]</span><span style="color:#806030;">)</span> 
                             <span style="color:#806030;">{</span> s<span style="color:#806030;">.</span>pop<span style="color:#806030;">(</span><span style="color:#806030;">)</span><span style="color:#806030;">;</span> B<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">;</span> <span style="color:#806030;">}</span>	<span style="color:#c34e00;">//若Station中第一个满足，出 </span>
			<span style="color:#400000;font-weight:bold;">else</span> <span style="color:#400000;font-weight:bold;">if</span><span style="color:#806030;">(</span>A <span style="color:#806030;">&lt;</span><span style="color:#806030;">=</span> n<span style="color:#806030;">)</span> 
                              s<span style="color:#806030;">.</span>push<span style="color:#806030;">(</span>A<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">)</span><span style="color:#806030;">;</span>	<span style="color:#c34e00;">//若不满足，再从A中开一节进Station </span>
			<span style="color:#400000;font-weight:bold;">else</span> <span style="color:#806030;">{</span> ok <span style="color:#806030;">=</span> <span style="color:#c00000;">0</span><span style="color:#806030;">;</span> <span style="color:#400000;font-weight:bold;">break</span><span style="color:#806030;">;</span> <span style="color:#806030;">}</span>    <span style="color:#c34e00;">//要A里没车了，就炸了吧</span>
		<span style="color:#806030;">}</span>
		<span style="color:#800040;">printf</span><span style="color:#806030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%s</span><span style="color:#0f6900;">\n</span><span style="color:#800000;">"</span><span style="color:#806030;">,</span> ok <span style="color:#806030;">?</span> <span style="color:#800000;">"</span><span style="color:#e60000;">Yes</span><span style="color:#800000;">"</span> <span style="color:#806030;">:</span> <span style="color:#800000;">"</span><span style="color:#e60000;">No</span><span style="color:#800000;">"</span><span style="color:#806030;">)</span><span style="color:#806030;">;</span>
	<span style="color:#806030;">}</span>
	<span style="color:#400000;font-weight:bold;">return</span> <span style="color:#c00000;">0</span><span style="color:#806030;">;</span>
<span style="color:#806030;">}</span>
</pre>
是这样没错，就是简单的一层层判断，如果判断到最后发现不行那么就真的不行，相信配合注释应该很好理解；用 if else 就可以做出来的一道水题！