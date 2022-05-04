---
title: Linux系统SSH客户端断开后保持进程继续运行配置方法
date: 2019-10-16 23:30:19
categories:
- TECHNOLOGY
tags:
- 云服务器
keywords:
description: 断开SSH客户端就没进程了，很不爽，毕竟服务器一直开着机，那么如何将其充分利用起来呢
---

[参考链接]( https://help.aliyun.com/knowledge_detail/42523.html?spm=5176.2000002.0.0.616d7b0fuIjmqa )

### 概述

 在Linux系统中，通常我们在执行一些运行时间比较长的任务时，必须等待执行完毕才能断开SSH连接或关闭客户端软件，否则可能会导致执行中断。 

### 使用screen执行

#### 安装screen工具

Linux系统默认没有screen工具，需要先进行安装。

- CentOS系列系统安装命令如下所示。

  ```
  yum install screen
  ```

- Ubuntu 系列系统安装命令如下所示。

  ```
  sudo  apt-get  install screen
  ```

 

#### 使用简介

1. 执行如下命令，创建screen窗口。

   ```
   screen -S [$Name]
   ```

   > 注：[$Name]用来标注screen窗口用途。

2. 执行如下命令，列出screen窗口。

   ```
   screen -ls
   ```

   系统显示类似如下。

   ![img](https://onekb.oss-cn-zhangjiakou.aliyuncs.com/1264805/a34dc1bf-9e0a-4b41-a7f1-14d8c29df360.png)

3. 当需要运行脚本、执行程序时，在命令前添加screen即可。

4. 然后使用 **Ctrl** 和 **a** 键，再按下 **d** 键，就可以退出SSH登录，但不会影响screen程序的运行。

5. 若需要继续工作时，登录实例，然后执行如下命令，恢复会话即可。

   ```
   screen -r -d
   ```