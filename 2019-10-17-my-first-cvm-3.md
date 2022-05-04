---
title: 云服务器初探C-私有网盘
date: 2019-10-16 21:33:07
categories:
- TECHNOLOGY
tags:
- 云服务器
- 私有云
keywords:
description: 在使用WinSCP将博客传输上去之后，我在想有没有什么更优雅的文件交互方式呢，这时候就找到了可道云
---

## 部署可道云

`kodexplorer`可道云是目前国内有代表性、美观易用性好的私有云软件。

带着U盘到处跑实在是太麻烦了，既然已经有了云服务器，为什么不物尽其用呢？

### 下载安装`xampp`

#### 下载`xampp`

这里是`xampp`的[下载地址]( https://www.apachefriends.org/zh_cn/download.html )

先探索一番自己所需要的版本，我的云服务器是`Linux`，所以找到了相应最新的下载链接

然后在云服务器输入` wget -c 下载链接 `命令即可，这里是我的选择

```
wget -c https://sourceforge.net/projects/xampp/files/XAMPP%20Linux/7.3.10/xampp-linux-x64-7.3.10-0-installer.run
```

下载完成后对其添加相应的权限

```
chmod +x xampp-linux-x64-7.3.10-0-installer.run
```

#### 安装`xampp`

直接使用安装命令即可

```
sudo ./xampp-linux-x64-7.3.10-0-installer.run
```

如果嫌下载速度太慢可以参考这篇[文章]( https://cybeird.coding.me/TECHNOLOGY/how-keep-running.html)，使其在后台一直保持下载

#### 启动与停止`xampp`

##### 启动`xampp`

```
sudo /opt/lampp/xampp start
```

在启动之后，可以在自己的电脑或手机浏览器上输入你的云服务器IP地址，就可以看到`xampp`的默认页面，代表你的`xampp`正常使用，默认端口为80。

> 运行出现错误，可能是端口冲突，通过查看80端口和443端口（命令为netstat -ap | grep 80）使用情况，可以修改默认的80和443端口，请参考[XAMPP：Another Sever is already running](https://blog.csdn.net/dezhihuang/article/details/53534565)。

> 如果你想访问phpmyadmin页面，可以浏览器访问“IP地址/phpmyadmin”，可能会出现错误，参考https://blog.csdn.net/YellowStar5/article/details/53446676/可解决问题。

##### 停止`xampp`

```
sudo /opt/lampp/xampp stop
```

### 下载安装可道云kodexplorer

### 1.下载最新版可道云

[官方下载页面](https://kodcloud.com/download/)。其中有Linux的[官方文档]( https://kodcloud.com/help/show-1.html )。以及`CentOS`的[官方教程]( http://bbs.kodcloud.com/d/5 )

下载命令：

```
wget http://static.kodcloud.com/update/download/kodexplorer4.40.zip
```

创建一个文件夹，这样把文件解压到这里

```
sudo mkdir kodexplorer
```

解压(注意这里的版本号与下载的要一致)

```
unzip kodexplorer4.40.zip -d ./kodexplorer
```

进入对应文件夹设置权限

```
cd ./kodexplorer
chmod -Rf 777 ./*
```

### 2.拷贝至相应的目录

将整个文件夹拷贝到对应文件夹

```
sudo cp -r kodexplorer/ /opt/lampp/htdocs/
```

进入对应文件夹，设置权限：

```
cd /opt/lampp/htdocs
chmod 777 kodexplorer
chmod -R 777 kodexplorer/data/
```

### 3.测试是否成功

重新启动`xampp`服务，浏览器打开`IP地址/kodexplorer/index.php`，设置管理员密码，开始使用。

![成功进入.png](https://i.loli.net/2019/10/17/WgVmxrqHyCPph6J.png)