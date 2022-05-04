---
title: 真的是很水的题目呢！(TOWQs)
tags:
  - cpp
  - TOWQs
  - Trip Of WaterQuestions
id: 1195
categories:
  - cpp
date: 2016-10-18 16:55:29
---

&nbsp;

恩，[这道题](https://4.vijos.org:8888/p/1316)实在是太水了，你既可以用桶排序也可以用set。反正搞一搞就出来了，我就不废话了；；

<!--more-->
<pre style="color:#000000;background:#f1f0f0;"><span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">set</span><span style="color:#800000;">&gt;</span>
<span style="color:#004a43;">#</span><span style="color:#004a43;">include </span><span style="color:#800000;">&lt;</span><span style="color:#40015a;">cstdio</span><span style="color:#800000;">&gt;</span>
<span style="color:#400000;font-weight:bold;">using</span> <span style="color:#400000;font-weight:bold;">namespace</span> <span style="color:#00dddd;">std</span><span style="color:#806030;">;</span>
<span style="color:#400000;font-weight:bold;">int</span> n<span style="color:#806030;">,</span>tmp<span style="color:#806030;">;</span>
<span style="color:#800040;">set</span><span style="color:#806030;">&lt;</span><span style="color:#400000;font-weight:bold;">int</span><span style="color:#806030;">&gt;</span> S<span style="color:#806030;">;</span>
<span style="color:#800040;">set</span><span style="color:#806030;">&lt;</span><span style="color:#400000;font-weight:bold;">int</span><span style="color:#806030;">&gt;</span><span style="color:#806030;">::</span><span style="color:#800040;">iterator</span> it<span style="color:#806030;">;</span>
<span style="color:#400000;font-weight:bold;">int</span> <span style="color:#800000;font-weight:bold;">main</span><span style="color:#806030;">(</span><span style="color:#806030;">)</span><span style="color:#806030;">{</span>
    <span style="color:#800040;">scanf</span><span style="color:#806030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#806030;">,</span><span style="color:#806030;">&amp;</span>n<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
    <span style="color:#400000;font-weight:bold;">for</span> <span style="color:#806030;">(</span><span style="color:#400000;font-weight:bold;">int</span> i<span style="color:#806030;">=</span><span style="color:#c00000;">1</span><span style="color:#806030;">;</span>i<span style="color:#806030;">&lt;</span><span style="color:#806030;">=</span>n<span style="color:#806030;">;</span>i<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">)</span><span style="color:#806030;">{</span>
        <span style="color:#800040;">scanf</span><span style="color:#806030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#800000;">"</span><span style="color:#806030;">,</span><span style="color:#806030;">&amp;</span>tmp<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
        S<span style="color:#806030;">.</span>insert<span style="color:#806030;">(</span>tmp<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
    <span style="color:#806030;">}</span>
    <span style="color:#800040;">printf</span><span style="color:#806030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span><span style="color:#0f6900;">\n</span><span style="color:#800000;">"</span><span style="color:#806030;">,</span>S<span style="color:#806030;">.</span>size<span style="color:#806030;">(</span><span style="color:#806030;">)</span><span style="color:#806030;">)</span><span style="color:#806030;">;</span>
    <span style="color:#400000;font-weight:bold;">for</span> <span style="color:#806030;">(</span>it<span style="color:#806030;">=</span>S<span style="color:#806030;">.</span>begin<span style="color:#806030;">(</span><span style="color:#806030;">)</span><span style="color:#806030;">;</span>it<span style="color:#806030;">!</span><span style="color:#806030;">=</span>S<span style="color:#806030;">.</span>end<span style="color:#806030;">(</span><span style="color:#806030;">)</span><span style="color:#806030;">;</span>it<span style="color:#806030;">+</span><span style="color:#806030;">+</span><span style="color:#806030;">)</span> 
        <span style="color:#800040;">printf</span><span style="color:#806030;">(</span><span style="color:#800000;">"</span><span style="color:#007997;">%d</span> <span style="color:#800000;">"</span><span style="color:#806030;">,</span><span style="color:#806030;">*</span>it<span style="color:#806030;">)</span><span style="color:#806030;">;</span>
<span style="color:#806030;">}</span>
</pre>
恩，就是这样。