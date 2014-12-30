---
layout: post
title:  "AngularJS 记录"
description: "AngularJS 记录"
modified: 2014-11-18 20:53:01
tags: [angular,javascript]
comments: true
share: true
---

##JavaScript相关

#### 1. chrome下input标签的Date,Time,Number格式

- date : ``yyyy-mm-dd`` eg: '2013-02-01'
- time : ``hh-mm-ss`` eg: '10:20:30' 或者 '10:20'
- number: 类型必须为number,String无法赋值

#### 2. 推荐封装函数写法
{% highlight javascript %} 
+function ($) {
 //your code here
}(jQuery)
{% endhighlight %}

> 这样写可以避免之前的括号没有闭合，导致的冲突


    



------------

##AngularJS

#### 1.检查当前页面$watcher数量(2000以下最好)
{% highlight javascript %} 
	(function () { 
	    var root = $(document.getElementsByTagName('body'));
	    var watchers = [];
	    var f = function (element) {
	        if (element.data().hasOwnProperty('$scope')) {
	            angular.forEach(element.data().$scope.$$watchers, function (watcher) {
	                watchers.push(watcher);
	            });
	        }
	        angular.forEach(element.children(), function (childElement) {
	            f($(childElement));
	        });
	    };
	     f(root);
	    console.log(watchers.length);
	})()
{% endhighlight %}

---------
> Written with [StackEdit](https://stackedit.io/).