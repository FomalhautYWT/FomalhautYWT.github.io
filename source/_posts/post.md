---
title: 关于yilia代码高亮中出现滚动条的问题
date: 2016-08-15 17:30:30
tags:
---
<!-- more -->
配置hexo的yilia主题的时候发现了code-block的highlight会出现一个问题就是代码会被一个滚动条遮住，很难看很不舒服
所以查了一下发现了解决方案
在hexo/themes/yilia/source/css/_partial/highlight.styl文件中将
```
.line
font-size: 15px
height: 15px
```
删掉height选项
之后就可以了。。。
