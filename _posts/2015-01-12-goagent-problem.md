---
layout: post
title:  "Mac上GoAgent 3.2.3 无法使用的解决方法"
description: "Mac上GoAgent 3.2.3 无法使用的解决方法"
modified: 2015-01-12 20:53:01
tags: [GoAgent,Mac]
comments: true
share: true
---



升级GoAgent3.2.3版本后发现在Windows下面使用无任何问题,Mac下面一直无法使用.
后来在[issue](https://code.google.com/p/goagent/issues/detail?id=19213&colspec=ID%20Opened%20Reporter%20Modified%20Summary%20Stars)的40楼找到了问题所在

##### 升级``python``到2.7.8
mac下使用``brew``升级
{% highlight perl %} 
brew install python
{% endhighlight %}

调整``PATH``
{% highlight perl %} 
brew doctor
{% endhighlight %}

##### 升级``pyopenssl``到0.14
mac下使用``easy_install``升级
{% highlight perl %} 
easy_install PyOpenSSL
easy_install PyCrypto
{% endhighlight %}

> Written with [StackEdit](https://stackedit.io/).