---
title: 从WP到HEXO
date: 2016-10-20 19:01:24
tags: hexo
categories:
  - Post
---
  <blockquote class="blockquote-center">
  这不该是这样的～ --古尔丹
  时代变了！ </blockquote>

  实际上，很久以前就对wordpress中十分诡异的对中文字体的支持颇有微词了，而同时作为一个穷逼，并没有钱去获得全托管的网站，对于网站的CSS也是表示毫无权限。
  在经历了无穷无尽，水深火热的小白期后，终于成为了一个菜鸟，然后照着谷歌上的[教程](https://http://opiece.me/2015/04/09/hexo-guide/)终于成功的搭建起了自己的网站(想想也是很不容易)。
  <!-- more -->

  然后发一篇博文来试一试 [NexT](https://github.com/iissnan/hexo-theme-next) 的特性(比如说代码高亮之类的东西)；

  ```C++
  #include<stdio.h>
int lowbit(int x)
{
	return x & (-x);
}
int bit[10001];
int a[100001];
int n,l,r;
int built()
{
	for(int i=1;i<=n;i++)
	 {
	 	bit[i]=a[i];
	 	for(int j=i-1;j>i-lowbit(i);j-=lowbit(j))
	 	 bit[i]+=bit[j];
	 }
}
int sum(int k)
{
	int ans=0;
	for(int i=k;i>0;i-=lowbit(i))
	 ans+=bit[i];
	return ans; 
}
int change(int x,int delta)
{
	for(int i=x;i<=n;i+=lowbit(i))
	 bit[i]+=delta;
}
int x,delta;
int main()
{
	scanf("%d",&n);
	for(int i=1;i<=n;i++)
	 scanf("%d",&a[i]);
	built();
	scanf("%d%d",&l,&r); 
	printf("%d\n",sum(r)-sum(l-1));
	scanf("%d%d",&x,&delta);
	change(x,delta);
	scanf("%d%d",&l,&r);
	printf("%d\n",sum(r)-sum(l-1));
}

  ```
