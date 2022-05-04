---
title: 新的评论系统终于建成
date: 2017-04-29 13:28:03
categories:
- Post
tags:
- blog
keywords: 网易云跟帖
description:
---
最后还是决定用网易云跟帖作为新的评论系统(为什么不用Disqus?恩,这是过好问题)
<!--more-->

### 后台管理导出数据

进入多说的后台管理系统,从工具——导出数据.

一定要记得勾选包含文章数据和包含评论数据.

导出后就是一个json文件,用于后面上传到新评论系统内的。

### 导入以往数据

注册好帐号后,进入后台管理,绑定好自己的站点网址,在数据统计——数据管理——数据导入中,上传之前导出的文件进去,就完成了.

实在是懒得截图了,操作并不繁琐,恩.

### 配置
网易云跟帖的后台里可以进行一些基本设置,主要说下hexo下next主题的配置.

因为主题里面集合了网易云跟帖所以操作起来简便.

#### 获取Product Key

登陆 `网易云跟帖` 获取你的 `Product Key`. 编辑 主题配置文件,编辑 `gentie_productKey` 字段,设置如下：
```
gentie_productKey: #your-gentie-product-key
```
#### 细节优化

我是找到了一位大神的博文,链接放在[这里](http://www.cduyzh.com/hexo-settings-7/)

就直接重写覆盖在 `hexo\blog\themes\next\source\css\_custom\custom.styl`
修改代码如下：
```
//网易云跟帖评论样式增添
.post-comments-count a::before {
    content: "评论";
}
#yun-tie-sdk-wrap .input-box .tie-submit-row .tie-submit-btn {
    background-color: #649ab6;
}
#yun-tie-sdk-wrap .input-box .tie-submit-row .tie-submit-btn:hover {
    background-color: #4c618f;
}
.tie-empty-tip {
    display: none;
}
//即将发布消息人样式
#yun-tie-sdk-wrap .input-box .tie-submit-row .user-info img:hover {
box-shadow: 0 0 10px #fff;
rgba(255, 255, 255, .6) inset 0 0 20px rgba(255, 255, 255, 1);
-webkit-box-shadow: 0 0 10px #fff;
rgba(255, 255, 255, .6) inset 0 0 20px rgba(255, 255, 255, 1);
transform: rotateZ(360deg); 
-webkit-transform: rotateZ(360deg);
-moz-transform: rotateZ(360deg);
}
#yun-tie-sdk-wrap .input-box .tie-submit-row .user-info img {
width: 32px;
height: 32px;
border-radius: 50%;
margin: 4px 10px 4px 8px;
padding: 0;
cursor: pointer;
box-shadow: inset 0 -1px 0 #3333sf; /*设置图像阴影效果*/
-webkit-box-shadow: inset 0 -1px 0 #3333sf;
-webkit-transition: 0.4s;
-webkit-transition: -webkit-transform 0.4s ease-out;
transition: transform 0.4s ease-out; /*变化时间设置为0.4秒(变化动作即为下面的图像旋转360读）*/
-moz-transition: -moz-transform 0.4s ease-out;
}
//评论框内其他人样式
#yun-tie-sdk-wrap .single-tie .photo img:hover {
box-shadow: 0 0 10px #fff;
rgba(255, 255, 255, .6) inset 0 0 20px rgba(255, 255, 255, 1);
-webkit-box-shadow: 0 0 10px #fff;
rgba(255, 255, 255, .6) inset 0 0 20px rgba(255, 255, 255, 1);
transform: rotateZ(360deg); 
-webkit-transform: rotateZ(360deg);
-moz-transform: rotateZ(360deg);
}
#yun-tie-sdk-wrap .single-tie .photo img {
width: 42px;
height: 42px;
border-radius: 50%;
padding: 0;
cursor: pointer;
box-shadow: inset 0 -1px 0 #3333sf; /*设置图像阴影效果*/
-webkit-box-shadow: inset 0 -1px 0 #3333sf;
-webkit-transition: 0.4s;
-webkit-transition: -webkit-transform 0.4s ease-out;
transition: transform 0.4s ease-out; /*变化时间设置为0.4秒(变化动作即为下面的图像旋转360读）*/
-moz-transition: -moz-transform 0.4s ease-out;
}
.name-nick:hover {
    border-left: 14px solid #3264b4;
}
.name-desp:hover {
    border-left: 14px solid #3264b4;
}
#yun-tie-sdk-wrap .single-tie .tie-author .name-nick{
    cursor: pointer;
    transition: border-width 0.3s linear 0.1s, color 0.2s linear 0.3s;
}
#yun-tie-sdk-wrap .single-tie .tie-author .name-desp {
    cursor: pointer;
    transition: border-width 0.3s linear 0.1s, color 0.2s linear 0.3s;
}
.tie-time:hover {
    border-right: 14px solid #3264b4;
}
#yun-tie-sdk-wrap .single-tie .tie-time {
    transition: border-width 0.3s linear 0.1s, color 0.2s linear 0.3s;
    cursor: pointer;
}
```
