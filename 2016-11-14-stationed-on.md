---
title: 正式驻扎在HEXO!
date: 2016-10-23 14:27:09
tags: hexo
categories:
  - Post
---
好了，搞了差不多有两节课的时间，终于把WP上的博文全数迁移到了HEXO上，实在是很不容易。
<!--more-->
{% blockquote HEXO https://hexo.io/zh-cn/docs/migration.html 迁移 %}
首先，安装 hexo-migrator-wordpress 插件。

$ npm install hexo-migrator-wordpress --save

在 WordPress 仪表盘中导出数据(“Tools” → “Export” → “WordPress”)（详情参考WP支持页面）。
插件安装完成后，执行下列命令来迁移所有文章。source 可以是 WordPress 导出的文件路径或网址。

$ hexo migrate wordpress <source>

{% endblockquote %}
没错，官方是有这么一个插件可以将WordPress上的博文直接迁移到hexo上，十分的简单而又快捷。
不过唯一麻烦的是代码块方面，就只能一个一个的改了。

还有的就是分类，一定不要搞太多，而且层次结构一定一定不要搞乱，不然就会出现下列坑爹的情况。。。
![img](https://cybirdy.files.wordpress.com/2016/10/harm_back1.jpg)

当然，如果你现在去看我的分类就会发现舒服很多(后来我改了改字体，从谷歌的外链字体库扒下来了许多好看的字体，不过代价就是网页加载速度。。不忍直视。)
 
然后是网易云音乐的外链播放器的实验:

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=280 height=52 src="http://music.163.com/outchain/player?type=2&id=1077407&auto=1&height=32"></iframe>

11 13

B站外链视频的测试

<embed height="485" width="584" quality="high" allowfullscreen="true" type="application/x-shockwave-flash" src="http://static.hdslb.com/miniloader.swf" flashvars="aid=5658797&page=1" pluginspage="http://www.adobe.com/shockwave/download/download.cgi?P1_Prod_Version=ShockwaveFlash"></embed>