---
layout: post
title:  "svg学习记录"
description: "记录SVG"
modified: 2014-07-13 20:53:01
tags: [SVG]
comments: true
share: true
---

##最基本的例子

{% highlight html%}
<!-- 
    version && baseProfile 必需的属性
 -->
<svg version="1.1"  
     baseProfile="full"
     width="300" height="200"
     xmlns="http://www.w3.org/2000/svg">

  <rect width="100%" height="100%" fill="red" />  <!-- 画方形 有点像canvas -->

  <circle cx="150" cy="100" r="80" fill="green" />  <!-- 画圆 -->

  <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>

</svg>
{% endhighlight %}

<iframe width="100%" height="300" src="http://jsfiddle.net/JerryImba/LdCuR/embedded/result,html/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>


##嵌入方法

- 通过``object``
{% highlight html%}
 <object data="image.svg" type="image/svg+xml" />
{% endhighlight %}

- 通过``iframe ``
{% highlight html%}
 <iframe src="image.svg"></iframe>
{% endhighlight %}


##网格

对于所有元素，SVG使用的坐标系统：以页面的左上角为(0,0)坐标点，坐标以像素为单位，x轴正方向是向右，y轴正方向是向下。

##缩放
{% highlight html%}
<svg width="200" height="200" viewBox="0 0 100 100">
{% endhighlight %}
这里定义的画布是200*200px，但是，viewBox属性定义了画布上可以显示的区域：从(0,0)点开始，100宽*100高的区域。这个100*100的区域，会放到200*200的画布上显示。于是就形成了放大两倍的效果。

##一些基本的形状
{% highlight html%}
<?xml version="1.0" standalone="no"?>
<svg width="200" height="250" version="1.1" xmlns="http://www.w3.org/2000/svg">

  <rect x="10" y="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/>
  <rect x="60" y="10" rx="10" ry="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/>

  <circle cx="25" cy="75" r="20" stroke="red" fill="transparent" stroke-width="5"/>
  <ellipse cx="75" cy="75" rx="20" ry="5" stroke="red" fill="transparent" stroke-width="5"/>

  <line x1="10" x2="50" y1="110" y2="150" stroke="orange" fill="transparent" stroke-width="5"/>
  <polyline points="60 110 65 120 70 115 75 130 80 125 85 140 90 135 95 150 100 145"
      stroke="orange" fill="transparent" stroke-width="5"/>

  <polygon points="50 160 55 180 70 180 60 190 65 205 50 195 35 205 40 190 30 180 45 180"
      stroke="green" fill="transparent" stroke-width="5"/>

  <path d="M20,230 Q40,205 50,230 T90,230" fill="none" stroke="blue" stroke-width="5"/>
</svg>
{% endhighlight %}
<iframe width="100%" height="300" src="http://jsfiddle.net/JerryImba/3pNSB/embedded/result,html/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>


##**PATH**
