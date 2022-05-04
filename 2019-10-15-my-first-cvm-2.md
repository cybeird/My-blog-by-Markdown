---
title: 云服务器初探B-转移博客
date: 2019-10-15 22:41:43
categories:
- TECHNOLOGY
tags:
- 云服务器
keywords:
description: 将我的布劳格转移一下，这样就可以在服务器上进行更新了！update everywhere！
---

### 将博客文件传输到服务器

很简单，[之前](https://cybeird.coding.me/TECHNOLOGY/my-first-cvm)说过，使用`WinSCP`即可，不过全上传是实在是太多太慢太累了

1. 讨论下哪些文件是必须拷贝的：首先是之前自己修改的文件，像站点配置config.yml，theme文件夹里面的题，以及source里面自己写的博客文件，这些肯定要拷贝的。除此之外，还有三个文件需要有，就是scaffolds文件夹（文章的模板）、package.json（说明使用哪些包）和.gitignore（限定在提交的时候哪些文件可以忽略）。其实，这三个文件不是我们修改的，所以即使丢失了，也没有关系，我们可以建立一个新的文件夹，然后在里面执行hexo init，就会生成这三个文件，我们只需要将它们拷贝过来使用即可。总结：_config.yml，theme/，source/，scaffolds/，package.json，.gitignore，是需要拷贝的。

2. 再讨论下哪些文件是不必拷贝的，或者说可以删除的：首先是.git文件，无论是在站点根目录下，还是主题目录下的.git文件，都可以删掉。然后是文件夹node_modules（在用npm install会重新生成），public（这个在用hexo g时会重新生成），.deploy_git文件夹（在使用hexo d时也会重新生成），db.json文件。其实上面这些文件也就是是.gitignore文件里面记载的可以忽略的内容。总结：.git/，node_modules/，public/，.deploy_git/，db.json文件需要删除。

* 为了使用hexo d来部署到git上，需要安装 
```
npm install hexo-deployer-git --save 
```
* 为了建立RSS订阅，需要安装 
```
npm install hexo-generator-feed --save 
```
* 为了建立站点地图，需要安装 
```
npm install hexo-generator-sitemap --save
```

### 上传到Coding和GitHub

#### 配置ssh

打开终端输入 `ssh-keygen -t rsa -C "your_email@example.com"`( 你的邮箱)，连续点击 Enter 键即可。

```
cd ~/.ssh
ls
//显示authorized_keys  id_rsa  id_rsa.pub即可
cat id_rsa.pub
//复制下来就好了
```

然后添加到`github`和`coding`的SSH公钥

之后就是直接`hexo g -d`就完事了，当然也可以直接在服务器上进行部署，但是意义不大。

