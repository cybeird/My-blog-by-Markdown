---
title: 软工第一课-概述与软件危机
date: 2021-08-25 10:06:53
tags:
- hexo
- next
- blog
- SWE
categories:
- AfterRead
- Software Engineering
description: 虽然没有好好学习，但是又没有完全在颓废
---

重新来过了，之前的博客因为我实在是太懒了，以致于没有把源文件从阿里云上拷贝下来，现在服务器已经被释出了，心情复杂。旧的文件我全放在`.oldold`项目里了，正如上次一样。

实际上这次课一直在捣鼓捣鼓博客，根本没在好好听，不过第一节课不算很深奥，我就照着ppt和课本大概梳理一下，顺便也把课后作业写咯。

### 软件工程学科发展历史

#### 概念提出
* 1968年NATO会议提出概念
* 1972年IEEE-CS出版学报

#### 学科雏形
* 上世纪70年代末，美国加入研究生教育计划
* 1991年被ACM和IEEE/CS列入计算学科

#### 学科确立
* 2004年8月 被IEEE-CS和ACM给出（SWEBOK[^10个领域]和SEEK）
> 软件工程、计算机科学、计算机工程、信息系统、信息技术 并列

# 软件工程学概述
软件工程是指导计算机软件开发与维护的一门工程学科
> 工程：将科学及数学原理运用于实际用途的应用手段，如：设计、制造、机器操纵、构架等。

## 软件危机
软件工程学自“软件危机”始

### 软件危机介绍

#### 软件的发展

* 程序设计阶段
* 程序系统阶段
* 软件工程阶段

#### 什么？

指在计算机软件的开发和维护过程中，所遇见的一系列严重问题。
* 如何开发软件->以满足日益增长的需求
* 如何维护软件->软件数量不断膨胀

#### 典型表现

1. 开发费用和进度难以估算控制导致超出预算
2. 需求分析不充分导致用户不满意最终产品
3. 质量难以保证；软件质量保证技术没能应用到开发全过程
4. 维护困难(**常常是不可维护的**)
5. 未保留适当的文档资料
> 文档的作用
> **软件开发管理人员**:用于管理和评价软件开发工程的进展状况
> **软件开发人员**:用于开发人员对各个阶段的工作都进行周密思考、全盘权衡、从而减少返工。并且可在开发早期发现错误和不一致性，便于及时加以纠正
> **软件维护人员**:软件维护的依据
6. 软件成本在计算机系统总成本的比例逐年上升
7. 软件开发生产率提高速度不及计算机应用普及速度

#### 产生原因
##### 本身特点
###### 与硬件不同

* 不可见性
* 是设计开发的逻辑产品
* 不会“磨损”，但是回退化(问题的隐蔽性)
* 开发和运行依赖于特点的计算机系统环境
* 具有可复用性

###### 与一般程序不同

* 规模庞大，复杂
* 大型软件开发既有技术问题也有社会问题
##### 开发与维护的方法不正确
* 对需求获取不正确
* 认为软件开发就是写程序并设法使之运行
* 软件开发只要依靠个别编程高手就能完成
* 轻视软件维护
> 维护费用往往占据总费用的55%-75%，提高软件的可维护性是重要目标

##### 其他原因
* 软件开发尚未完全摆脱手工艺的开发方式。
* 软件成本相当昂贵，主要依靠大量复杂的、高强度的脑力劳动
* 软件的开发和运行常常受到计算机系统的限制，对计算机系统有着不同程度的依赖性。

#### 消除途径
1. 对计算机软件有正确的认识，彻底消除“软件就是程序”的错误观念。
> 软件=程序+数据+文档
> 程序是能够完成预定功能和性能的可执行的指令序列；
> 数据是使程序能够适当地处理信息的数据结构；
> 文档是开发、使用和维护程序所需要的图文资料
2. 充分认识到软件开发是一种组织良好、管理严密、各类人员协同配合、共同完成的工程项目，不是个人独立的劳动。
3. 推广和使用在实践中总结出来的软件开发的成功技术和方法。
4. 开发和使用更好的软件工具

### 结论

软件工程正是从**管理**和**技术**两方面研究如何更好地开发和维护计算机软件的。
按工程化的原则和方法组织软件开发工作是有效的，是摆脱软件危机的一个主要出路。


[^10个领域]: 需求 设计 构造 测试 维护 配置管理 工程管理 工程过程 工程工具和方法 质量