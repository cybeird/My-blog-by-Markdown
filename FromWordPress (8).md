---
title: 一道水题背后的几把辛酸泪(TOWQs)
tags:
  - cpp
  - MINE
  - TOWQs
  - Trip Of WaterQuestions
  - 动态规划
  - 单调性DP
  - 作死
id: 585
categories:
  - cpp
date: 2016-09-26 09:36:49
---

[<span class="pid">vijos P1292 </span>火车票](https://vijos.org/p/1292)

这道题可以说是一道不是很水的题目，因为毕竟是一道动态规划的题目（当然你也可以用贪心做）。

但是我，即便是使用了动态规划，却也依旧达成了如此强大的战绩。。

下面上图！

![ticket](https://cybirdy.files.wordpress.com/2016/09/ticket.png)

没错，就是这*一样的战绩，下面就来揭晓这道题的真面目！<!--more-->

前三次TLE的原因很简单，![%e6%98%af](https://cybirdy.files.wordpress.com/2016/09/e698af.png)

没错，连续三次忘记了去掉文件操作，而且最重要的是我还以为是其他的错误（比如说把%lld变成%I64d等等）成功刷低了我的AC率，这血一样的教训。。可啪。。

至于后三次RE的原因就有那么几分意思了，为此我还做了个测试（就不在这里展开了，感兴趣的可以下去试试，就是关于memset的坑爹用法）

先上代码
> <pre>#define LOCAL
> #include&lt;cstdio&gt;
> #include&lt;cstring&gt;
> #include&lt;iostream&gt;
> #include&lt;algorithm&gt;
> using namespace std;
> int main()
> {
> 	#ifdef LOCAL
> 		freopen("rail.in","r",stdin);
> 		freopen("rail.out","w",stdout);
>         #endif 
> 	int bird,is,great,c1,c2,c3,n,m,i,j,p,s,t;
> 	long long d[101],dis,f[101];
> 	scanf("%d%d%d%d%d%d",&amp;bird,&amp;is,&amp;great,&amp;c1,&amp;c2,&amp;c3);
> 	scanf("%d",&amp;n);
> 	scanf("%d%d",&amp;s,&amp;t);
> 	if (s&gt;t) swap(s,t);
> 	d[1]=0;
> 	for(i=2;i&lt;=n;i++)
> 	  scanf("%lld",&amp;d[i]);
> 	memset(f,0x3f,sizeof(f));
> 	f[s]=0;
> 	for(i=s+1;i&lt;=t;i++)
> 	  for(j=s;j&lt;=i-1;j++)
> 	  {
> 	   dis=d[i]-d[j];
> 	   if (dis&lt;=bird) 
> 	     if (f[j]+c1&lt;f[i]) f[i]=c1+f[j]; 	   
>            if (dis&gt;bird&amp;&amp;dis&lt;=is) 
> 	     if (f[j]+c2&lt;f[i]) f[i]=c2+f[j]; 	   
>            if (dis&gt;is&amp;&amp;dis&lt;=great) 
> 	     if (f[j]+c3&lt;f[i]) f[i]=c3+f[j];
> 	  }
> 	printf("%lld",f[t]);
> }</pre>
&nbsp;

<span style="font-family:Merriweather, Georgia, 'Times New Roman', Times, serif;line-height:1.7;background-color:#ffffff;">我的想法很简单，就是用memset将f数组中的值定义成非常大。</span>

    <span class="hljs-built_in">memset</span>(f,<span class="hljs-number">127</span>,<span class="hljs-keyword">sizeof</span>(f));`</pre>
    <span style="font-family:Merriweather, Georgia, 'Times New Roman', Times, serif;line-height:1.7;background-color:#ffffff;">但是，我忽视了一个简单而又致命的错误，当我将数组中的值定义的太大之后，如果数据很大的话，它们加在一起就会爆掉，从而在评测集中出现“崩溃：访用无效内存”的错误。</span>
    <pre>`<span class="hljs-built_in">memset</span>(f,0x3f,<span class="hljs-keyword">sizeof</span>(f));

然后我就将其改成了这个样子，心想，这应该不会出错了吧。

但是，依旧出现了RE的坑爹错误，看来是我的代码出现了严重问题！

【尽管我在cogs上提交后只RE了四个点，但是却是开了-O2优化之后的结果（实际上cogs上并不能不开-o2，据吴鸫鸫的神奇小道消息所说：】

![%e6%8d%95%e8%8e%b7](https://cybirdy.files.wordpress.com/2016/09/e68d95e88eb72.png)

我 我我我我我我我我我我是是是是是是是是是 。。火火火火火，车王！

* * *

&nbsp;