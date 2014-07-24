---
layout: post
title:  "AngularJs 源码阅读"
description: "AngularJs 源码阅读"
modified: 2014-07-24 20:53:01
tags: [AngularJS]
comments: true
share: true
---

####源码版本 v1.3.0-beta.10

----------

##开始
从文件的最后开始看

{% highlight javascript%}
  //检查AngularJS是否已经加载
  if (window.angular.bootstrap) {
    //AngularJS 已经加载，所以在此return
    console.log('WARNING: Tried to load angular more than once.');
    return;
  }

  //try to bind to jquery now so that one can write angular.element().read()
  //but we will rebind on bootstrap again.
  bindJQuery();

  publishExternalAPI(angular);

  jqLite(document).ready(function() {
    angularInit(document, bootstrap);
  });
{% endhighlight %}

