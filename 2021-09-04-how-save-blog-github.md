---
title: 怎样将博客内容相关的源文件保存在Github上
date: 2021-09-02 09:06:20
tags:
- Github
- hexo
- blog
- git
categories:
- AfterRead
description: 有的时候我们会因为各种各样的原因丢失自己使用的博客的源代码（感觉我已经经历了N次），于是决定研究一下如何将hexo博客原文件的关键文件同步存储到GitHub上。

---

## 前情提要

首先，我们要知道哪些文件是可替代的，哪些文件是用户配置之后需要保留的

```
- scaffolds  ##新建博客的模板文件
- source  ##博客上传中的所有内容文件，也可以放一些你自己写的html
- themes  ##所有的主题文件
- _config.yml  ##博客的配置文件
```

## 插件安装

不过你不知道哪些需要保留应该也无关紧要，因为我们今天使用的是`git-deployer-git`这款插件，首先使用下列语句来进行安装

```git
npm install hexo-deployer-git --save
```

## 使用介绍

在博客源文件的`_config.yml`中进行配置

```yaml
# 你可以这样使用:
deploy:
  type: git  #自行选择自己部署的网站
  repo: <项目地址>   #https://github.com/用户名/项目名.git
  branch: [分支名字]  #如果使用的GitHub，将会默认使用gh-pages，不然一般都是master
  token: ''
  message: [信息]  #提交时的信息，默认是Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}
  name: [git的用户名]
  email: [git的邮箱]
  extend_dirs: [extend directory]  #在此处设置要部署的目录
  ignore_hidden: false # 默认是true
  ignore_pattern: regexp  # 在进行部署时将要自动忽略的文件，regexp代表全部

# 或者这样:
deploy:
  type: git
  message: [信息]
  repo: <项目地址>[,分支名字]
  extend_dirs:
    - [extend directory]
    - [another extend directory]
  ignore_hidden:
    public: false
    [extend directory]: true
    [another extend directory]: false
  ignore_pattern:
    [folder]: regexp  # or you could specify the ignore_pattern under a certain directory

# 或者进行多项仓库的统一配置
deploy:
  repo:
    # Either syntax is supported
    [仓库名]: <项目地址>[,分支名字]
    [仓库名]:
      url: <项目地址>
      branch: [分支名字]
```

所以保存源目录的方式就很简单了，在GitHub上创立两个分支`gh-pages`和`master`（自然，你可以使用任意你想要的名字，把配置文件修改一番即可）然后按照一下方式修改配置文件（部署两次到两个分支去）

`gh-pages`是用来展示博客网站的分支，所以记得在项目的`Settings`中的`Pages`选项中将`Source`设置成 `Branch:gh-pages` 和`/root`(如果你有其他想法也可以设置成别的)

`master`文件中存储的即是所有需要保存的文件，需要的时候使用`hexo init`一个文件然后把`master`拷下来覆盖即可。

### 最终代码

```yaml
# _config.yaml
deploy:
  - type: git
    repo: git@github.com:<用户名>/<用户名>.github.io.git
    branch: gh-pages
  - type: git
    repo: git@github.com:<用户名>/<用户名>.github.io.git
    branch: master
    extend_dirs: /
    ignore_hidden: false
    ignore_pattern:
        public: .
```
### 注意事项

记得将博客源文件和主题源文件中的`.git`文件夹删除，如果有的话

#### 待解决

* 字体文件只能本机查看

* 每次部署都需要删除`.deploy_git`,有点麻烦且还没搞懂

    ```
    rm -rf .deploy_git
    ```

    

    
