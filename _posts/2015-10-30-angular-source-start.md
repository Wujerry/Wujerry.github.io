---
layout: post
title:  "AngularJS 源码分析 - Start"
description: "AngularJS 源码分析 - Start"
modified: 2015-10-30 15:53:01
tags: [angular,javascript]
comments: true
share: true
---
###背景
用AngularJS做项目开发算起来有两年，从移动端做到Desktop，期间也遇到了很多坑，有些爬出来了，有些绕过去了，还有一些依然在坑里。一直以来都想仔细看一下angular的源码，顺便记录下来，换个新姿势装装逼。

###姿势
既然是读源码，当然要以源码为主，这一系列文章呢还是以代码注释为主，总结为辅。

###开始
看源码还是得到angular的[Github](https://github.com/angular/angular.js)仓库去，大概看了下目录，根据我多年的精验，目测源码应该都在``src``目录下，根目录唯一能打的是一个叫``angularFiles.js``的文件。

- ``angularFiles.js``
   此文件描述了AngularJs的一个大概的组成结构，同时也是build的配置文件，构建工具会根据此配置文件将所有js文件组装在一起，然后压缩发布。

###目录

 -  [minErr.js](http://www.jerryimba.com/angular-source-minerr/)

> Written with [StackEdit](https://stackedit.io/).