---
title: 这和说好的不一样啊！(TOWQs)
tags:
  - cpp
  - TOWQs
  - Trip Of WaterQuestions
  - 并查集
  - 二分答案
id: 1066
categories:
  - cpp
date: 2016-10-18 09:48:49
---

嗯，记得假期的时候马老师专门跟我们说过[关押罪犯](https://vijos.org/p/1776)这道题，他认为这道题可以说是二分答案的典型例题了~~然而。。。<!--more-->

为毛大家看到这道题的时候都是用的并查集呢(⊙o⊙)?（嗯，高老师用的爆搜我们就不必在意了）

虽然不知到为什么就连标签上都打上 “图结构 二分图” ，然而我依旧去用并查集去做。嗯，没有任何原因，就是要用并查集！(好吧，实际上就是单纯的不会二分图而已)

开一个两倍的并查集表示犯人的集合及其补集，排序按怨念从大到小往集合里放，发现冲突直接输出就可以了。

排序直接调用的中的 sort(a, a+n)。并查集是标准的一行式路径压缩，每次查找确认不冲突后分别放到对方的补集中。空间 O(2n)，时间 O(m lg*n)，其中 lg*n 最大为 5 效率很高，90分。

最后注意没有冲突要输出 0，这样才能 100 分。(高老师就是被这个坑了，但是我最开始就是为了骗分直接输出了零，拿了十分，所以最后写正解的时候没有被坑)
下面上代码：
<pre style="color:#000000;background:#f1f0f0;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">algorithm</span><span style="color:#800000;">&gt;</span>
<span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">iostream</span><span style="color:#800000;">&gt;</span>
<span style="color:#400000;font-weight:bold;">using</span> <span style="color:#400000;font-weight:bold;">namespace</span> <span style="color:#00dddd;">std</span><span style="color:#806030;">;</span>
<span style="color:#400000;font-weight:bold;">int</span> n<span style="color:#806030;">,</span>m<span style="color:#806030;">,</span>f<span style="color:#806030;">[</span><span style="color:#c00000;">40001</span><span style="color:#806030;">]</span><span style="color:#806030;">,</span>x<span style="color:#806030;">,</span>y<span style="color:#806030;">;</span>
<span style="color:#400000;font-weight:bold;">struct</span> data
<span style="color:#806030;">{</span>
	<span style="color:#400000;font-weight:bold;">int</span> a<span style="color:#806030;">,</span>b<span style="color:#806030;">,</span>c<span style="color:#806030;">;</span>
<span style="color:#806030;">}</span>e<span style="color:#806030;">[</span><span style="color:#c00000;">100001</span><span style="color:#806030;">]</span><span style="color:#806030;">;</span> 	<span style="color:#c34e00;">//定义一个结构体来数据</span>
<span style="color:#400000;font-weight:bold;">bool</span> cmp<span style="color:#806030;">(</span><span style="color:#400000;font-weight:bold;">const</span> data <span style="color:#806030;">&amp;</span>a<span style="color:#806030;">,</span><span style="color:#400000;font-weight:bold;">const</span> data <span style="color:#806030;">&amp;</span>b<span style="color:#806030;">)</span>
<span style="color:#806030;">{</span>
	<span style="color:#400000;font-weight:bold;">return</span> a<span style="color:#806030;">.</span>c<span style="color:#806030;">&gt;</span>b<span style="color:#806030;">.</span>c<span style="color:#806030;">;</span>
<span style="color:#806030;">}</span><span style="color:#c34e00;">//这样就可以按照怨气值进行从大到小的排序</span>
<span style="color:#c34e00;">//这么写和重载的做法，在速度上没什么区别，只不过尽量用默认的吧</span>
<span style="color:#c34e00;">//可读性嘛，不写得越多越好。</span>
<span style="color:#c34e00;">//如果能确定只可能有一种严格弱序，或者要求默认一种，那就应该用&lt;。</span>
<span style="color:#c34e00;">//如果在多种严格弱序，其中没一种比其它更值得当成默认的，那么就不应该用&lt;。</span>
<span style="color:#400000;font-weight:bold;">int</span> <span style="color:#800040;">find</span><span style="color:#806030;">(</span><span style="color:#400000;font-weight:bold;">int</span> x<span style="color:#806030;">)</span>
<span style="color:#806030;">{</span>
    <span style="color:#400000;font-weight:bold;">return</span> f<span style="color:#806030;">[</span>x<span style="color:#806030;">]</span><span style="color:#806030;">=</span><span style="color:#806030;">=</span>x<span style="color:#806030;">?</span>x<span style="color:#806030;">:</span>f<span style="color:#806030;">[</span>x<span style="color:#806030;">]</span><span style="color:#806030;">=</span><span style="color:#800040;">find</span><span style="color:#806030;">(</span>f<span style="color:#806030;">[</span>x<span style="color:#806030;">]</span><span style="color:#806030;">)</span><span style="color:#806030;">;</span>
<span style="color:#806030;">}</span>		<span style="color:#c34e00;">//最简单的并查集运用</span>
<span style="color:#400000;font-weight:bold;">int</span> <span style="color:#800000;font-weight:bold;">main</span><span style="color:#806030;">(</span><span style="color:#806030;">)</span>
<span style="color:#806030;">{</span>
	<span style="color:#800040;">cin</span><span style="color:#806030;">&gt;</span><span style="color:#806030;">&gt;</span>n<span style="color:#806030;">&gt;</span><span style="color:#806030;">&gt;</span>m<span style="color:#806030;">;</span>
    <span style="color:#400000;font-weight:bold;">for</span><span style="color:#806030;">(</span><span style="color:#400000;font-weight:bold;">int</span> i<span style="color:#806030;">=</span><span style="color:#c00000;">1</span><span style="color:#806030;">;</span>i<span style="color:#806030;">&lt;</span><span style="color:#806030;">=</span>m<span style="color:#806030;">;</span>i<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">)</span>
        <span style="color:#800040;">cin</span><span style="color:#806030;">&gt;</span><span style="color:#806030;">&gt;</span>e<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">.</span>a<span style="color:#806030;">&gt;</span><span style="color:#806030;">&gt;</span>e<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">.</span>b<span style="color:#806030;">&gt;</span><span style="color:#806030;">&gt;</span>e<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">.</span>c<span style="color:#806030;">;</span>
    <span style="color:#400000;font-weight:bold;">for</span><span style="color:#806030;">(</span><span style="color:#400000;font-weight:bold;">int</span> i<span style="color:#806030;">=</span><span style="color:#c00000;">1</span><span style="color:#806030;">;</span>i<span style="color:#806030;">&lt;</span><span style="color:#806030;">=</span>n<span style="color:#806030;">*</span><span style="color:#c00000;">2</span><span style="color:#806030;">;</span>i<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">)</span>
        f<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">=</span>i<span style="color:#806030;">;</span>
    <span style="color:#800040;">sort</span><span style="color:#806030;">(</span>e<span style="color:#806030;">+</span><span style="color:#c00000;">1</span><span style="color:#806030;">,</span>e<span style="color:#806030;">+</span>m<span style="color:#806030;">+</span><span style="color:#c00000;">1</span><span style="color:#806030;">,</span>cmp<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
    <span style="color:#400000;font-weight:bold;">for</span><span style="color:#806030;">(</span><span style="color:#400000;font-weight:bold;">int</span> i<span style="color:#806030;">=</span><span style="color:#c00000;">1</span><span style="color:#806030;">;</span>i<span style="color:#806030;">&lt;</span><span style="color:#806030;">=</span>m<span style="color:#806030;">;</span>i<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">)</span>
	<span style="color:#806030;">{</span>
        x<span style="color:#806030;">=</span><span style="color:#800040;">find</span><span style="color:#806030;">(</span>e<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">.</span>a<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
        y<span style="color:#806030;">=</span><span style="color:#800040;">find</span><span style="color:#806030;">(</span>e<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">.</span>b<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
        <span style="color:#400000;font-weight:bold;">if</span><span style="color:#806030;">(</span>x<span style="color:#806030;">=</span><span style="color:#806030;">=</span>y<span style="color:#806030;">)</span>
		<span style="color:#806030;">{</span>
            <span style="color:#800040;">cout</span><span style="color:#806030;">&lt;</span><span style="color:#806030;">&lt;</span>e<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">.</span>c<span style="color:#806030;">;</span>
            <span style="color:#400000;font-weight:bold;">return</span> <span style="color:#c00000;">0</span><span style="color:#806030;">;</span>
        <span style="color:#806030;">}</span>
        f<span style="color:#806030;">[</span>y<span style="color:#806030;">]</span> <span style="color:#806030;">=</span> <span style="color:#800040;">find</span><span style="color:#806030;">(</span>e<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">.</span>a <span style="color:#806030;">+</span> n<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
        f<span style="color:#806030;">[</span>x<span style="color:#806030;">]</span> <span style="color:#806030;">=</span> <span style="color:#800040;">find</span><span style="color:#806030;">(</span>e<span style="color:#806030;">[</span>i<span style="color:#806030;">]</span><span style="color:#806030;">.</span>b <span style="color:#806030;">+</span> n<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
    <span style="color:#806030;">} //因为已经对罪犯的仇恨值排过序了，所以直接尽可能的把仇恨值高的分开</span>
    <span style="color:#800040;">cout</span><span style="color:#806030;">&lt;</span><span style="color:#806030;">&lt;</span><span style="color:#c00000;">0</span><span style="color:#806030;">;
</span>    <span style="color:#400000;font-weight:bold;">return</span> <span style="color:#c00000;">0</span><span style="color:#806030;">;</span>
<span style="color:#806030;">}</span>
</pre>
考虑到并查集的本职工作是维护某两点在一个集合，不能很好地处理不在一个集合的情况，所以我们要曲线救国，通过保存某个点的“敌人”集合来代表和他不在一个监狱的罪犯，间接地实现维护某两点不在一个集合的情况。在加入关系的时候进行判断，如果某两点已经在一个集合，说明他们无论如何也安排不到不同的两个监狱了，输出仇恨值即可。

（P.s 用并查集保存两点不在一个集合还可以使用对立点的方式，即给每一个实点都建立一个与之对立的虚点。当读取到A与B不在同一集合的信息时，将A与B'，B与A'分别连边，这样也可以表示A与B不在同一集合。判断过程与上面的方法相同，实现起来也很简单，大家不妨试一下）『犯罪团伙这道题可以说是这个思路，可以一做』