---
title: 云服务器初探A-基本操作
date: 2019-10-15 12:51:14
categories:
- TECHNOLOGY
tags:
- 云服务器
- blog
- hexo
keywords:
description: 由于U盘丢失惨案而引起的一系列事件，刚好腾讯云也送了一个15天的云服务器可以拿来试试手
---

### 与云服务器CVM的第一次邂逅

我在一次更新博客的时候突然想起来之前好像给我的博客绑过一个域名(cybird.site)，不过后来好像炸了，我一直以为过期了，然后就上线查看了一番。

结果不仅发现我的域名还没过期（还剩几个月），还"意外"在腾讯云发现了云服务器白给活动

![0元试用.png](https://i.loli.net/2019/10/15/ORmZHtKxUQdVwvl.png)

这就很舒服了，毫不犹豫瞎搞就完事了

当然我大概把几个提供的系统都试了一番，发现我还是用`centos`吧

### 如何优雅的进进出出

 #### 使用`puTTy`登入云服务器

[这里](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)是`puTTy`的下载地址.

然后对其进行配置

![PuTTy](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)

参数举例说明如下：

- Host Name（or IP address）：云服务器的公网IP（登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)，可在列表页及详情页中获取公网 IP）。
- Port：云服务器的端口，必须设置为22。
- Connect type：选择`SSH`。
- Saved Sessions：填写会话名称，例如 test。
  配置 `Host Name`后，再配置 `Saved Sessions` 并保存，则后续使用时您可直接双击 `Saved Sessions` 下保存的会话名称即可登录服务器。

完成操作之后进到这个界面，输入账号密码即可开始快乐

![进入服务器.png](https://i.loli.net/2019/10/15/8tU2s7zHDPYGhVZ.png)

#### 在云服务器上交互文件

这里我们使用一款叫做`WinSCP`的[软件](https://winscp.net/eng/download.php)

![来交互吧.png](https://i.loli.net/2019/10/15/2b8Uol3Sy9eOvu1.png)

这里不必多说，先把各类信息输好就行了

在左边选取要上传的文件，右边选取要放置的目录然后点击`上传`即可，反之亦然

不过直接拖拽也是可以的

![交互.png](https://i.loli.net/2019/10/15/FN9bfqDPaYy6ZBp.png)

这样一来各种意义上来说都方便许多（直接拿来当网盘存存文件也挺好)

不过我太弱了，所以入手的服务器也一样弱，跑`windows`卡顿很严重。而我对于`Linux`如何用手机愉快远程玩耍一窍不通，所以现在这儿立个`Flag`

### 安装各类必要的环境依赖应用

`CentOS`环境安装依赖比较方便

``` 
yum install 软件名称
```

就可以了

#### ``node js ``安装

安装 `Node.js` 的最佳方式是使用` nvm`。`nvm` 的开发者提供了一个自动安装 `nvm `的简单脚本：
cURL:

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | sh
```
Wget:
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | sh
```
安装完成后，重启终端并执行下列命令即可安装 Node.js。
```
nvm install node
```

#### 安装`git`

```
yum -y install git 
```

#### 安装`nginx`

```
yum -y install nginx
```

> `nginx`用于托管静态博客，不过我最后考虑了一番还是没用上

#### 安装`hexo`

我们使用 `Node.js `的包管理器 `npm` 安装 `hexo-cli` 和` hexo-server`

```
npm install hexo-cli hexo-server -g
```

如果这里报错了可以尝试再前面加上`sudo`

这之后就可以快乐布劳格了

至于`hexo`的食用方式这里不再阐述

不过当在云服务器进行`hexo s`操作后，可以通过在浏览器中输入`http://服务器IP:4000/ `进入