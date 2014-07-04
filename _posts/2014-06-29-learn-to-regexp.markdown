---
layout: post
title:  "正则表达式学习记录"
date:   2014-06-29 20:53:01
categories: jekyll update
tags: Regular
excerpt: 正则表达式的一些基础、常用字符和用法
comments: true
---

##Egrep 元字符
 
* 行的开始和结束： ``^`` 开始  ``$`` 结束   例：``^cat$``
* 字符组：``[something here]``
    1. ``-`` 连字符   表示一个范围   例： ``[1-9a-f]``
    2. 排除型字符组    在字符组中出现的第一个``^`` 表示匹配任何未列出的字符  例： ``[^1-6]``
    3. ``.`` 匹配任意字符
    4. 一个字符组只能匹配目标文本中的**单个字符**
* 多选结构  ``|``
    1. 匹配任意子表达式 ``|``  例： ``grey|gray`` 等同于 ``gr(e|a)y`` 等同于 ``gr[ea]y``
* 忽略大小写  ``-i`` 参数   一般写在正则表达式之前
* 单词分界符  开始``\<``     结束``\>``
* 量词
    1. 可选元素  ``?``    例： ``colou?r``可以匹配单词 color 和 colour    ``?`` 只作用于它的前一个字符
    2. ``*`` 出现0次以上
    3. ``+`` 出现1次以上
    4. ``{}``  出现区间   例： ``[a-zA-Z]{1,5}``   表示1到5个字母
* 括号以及反向引用
    1. ``\1``  ``\2``  等等  例：``\<([a-zA-Z])+ +\1\>`` 可以匹配重复出现的单词  ``\1``表示的是第一个括号匹配的内容  ``(?:something)``表示**只分组不匹配**
    2. ``\`` 转义符  **字符组内无效**

##ShortHands

* ``\t`` 制表符 Tab
* ``\n`` 换行符
* ``\r`` 回车符
* ``\s`` 任何空白字符
* ``\S``  除了任何``\s``以外的字符
* ``\w``  等同于``[a-zA-Z0-9]``   (``\w+``可以用来匹配一个单词)
* ``\W``  等同于``[^a-zA-Z0-9]``      
* ``\d``  数字
* ``\D`` 非数字   即``[^0-9]``
* ``\b``  单词分界符
* ``[\u4e00-\u9fa5]``  中文

##环视   

* 确定位置，不匹配文本
* 逆序环视
    1. ``(?<=..........)``    肯定逆序环视，子表达式能够匹配**左侧**文本，位置在文本右侧
    2. ``(?<！..........)``   否定逆序环视，子表达式不能够匹配**左侧**文本，位置在文本右侧
* 顺序环视
    1. ``(?=........)``        肯定顺序环视，子表达式能够匹配**右侧**文本，位置在文本左侧
    1. ``(?！........)``       否定顺序环视，子表达式不能够匹配**右侧**文本，位置在文本左侧
* ``(?<!\w)(?=\w)|(?<=\w)(?!\w)`` 等同于``\b``   也就是单词分界符


##常用正则表达式（perl）

* Email : ``\b(\w[-.\w]*\@[-a-z0-9]+(\.[-a-z0-9]+)*\.([a-z]+)\b``
* Url地址 : ``\b((https?|ftp):\/\/[-a-z0-9]+(\.[-a-z0-9]+)*\.([a-z]+)\b([-a-z0-9_:\@&?=+,.!/~*`%\$]*(?<![.,?!]))?``



##JavaScript用法
* test  检查指定的字符串是否存在
{% highlight javascript %}
var str = 'hellow word!';
var reg = /low/gi;
console.log(reg.test(str));  //true  参数g为全局  参数i为忽略大小写
{% endhighlight %}

* exec  返回查询值
{% highlight javascript %}
var str = 'hellow word!';
var reg = /low/gi;
console.log(reg.exec(str));  //low
{% endhighlight %}

* match  得到查询数组
{% highlight javascript %}
var str = 'hellow word!';
var reg = /o/gi;
var arrays = str.match(reg);  //返回数组
{% endhighlight %}

* search  返回搜索位置  类似于indexof
{% highlight javascript %}
var str = 'hellow word!';
var reg = /o/gi;
var num= str.search(reg);  // 4
{% endhighlight %}

* replace  替换字符  利用正则替换
{% highlight javascript %}
var str = 'hellow word!';
var reg = /o/gi;
var num= str.replace(reg,'l');  // 'helllw wlrd!'
{% endhighlight %}

* split   利用正则分割数组
{% highlight javascript %}
var str = 'hellow word!';
var reg = /o/gi;
var arrays = str.split(reg);  //返回数组
{% endhighlight %}


 

















