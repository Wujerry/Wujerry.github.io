---
layout: post
title:  "svg学习记录"
description: "记录SVG"
modified: 2014-07-13 20:53:01
tags: [SVG]
comments: true
share: true
---

参考自: [MDN](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial)

----------

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

----------

##**PATH**

###直线

- **move** : ``M x y`` 或者 ``m dx dy``

例如``<path d="M10 10"/>``,就像在Canvas里面将画笔移动至坐标(10,10)处

- **line to** : ``L x y `` 或者 ``l dx dy``
- **H line to** : ``H x `` 或者 `` h dx``
- **V line to** : ``V y  `` 或者 ``v dy``

例子：画一个边距为10的正方形
{% highlight html%}
<?xml version="1.0" standalone="no"?>

<svg width="100px" height="100px" version="1.1" xmlns="http://www.w3.org/2000/svg">

  <!-- 路径 -->
  <path d="M10 10 H 90 V 90 H 10 L 10 10"/>

  <!-- Points -->
  <circle cx="10" cy="10" r="2" fill="red"/>
  <circle cx="90" cy="90" r="2" fill="red"/>
  <circle cx="90" cy="10" r="2" fill="red"/>
  <circle cx="10" cy="90" r="2" fill="red"/>

</svg>
{% endhighlight %}

- **闭合路径** : ``z``

例如上面的例子`` <path d="M10 10 H 90 V 90 H 10 Z" fill="transparent" stroke="black"/>``

- **相对路径（小写）**

相对命令使用的是小写字母，它们的参数不是指定一个明确的坐标，而是表示相对于它前面的点需要移动多少距离。例如前面的示例，画的是一个80*80的正方形，用相对命令可以这样描述:``<path d="M10 10 h 80 v 80 h -80 Z" fill="transparent" stroke="black"/>``

----------

##曲线

###三次贝塞尔曲线:``C``
{% highlight html %}
<!-- C x1 y1, x2 y2, x y (or c dx1 dy1, dx2 dy2, dx dy) -->
<!-- 三次贝塞尔曲线需要定义一个点和两个控制点 -->
<!-- 这里的最后一个坐标(x,y)表示的是曲线的终点，另外两个坐标是控制点，
(x1,y1)是起点的控制点，(x2,y2)是终点的控制点 -->
<path d="M10 10 C 20 20, 40 20, 50 10" stroke="black" fill="transparent"/>
{% endhighlight %}

你可以将若干个贝塞尔曲线连起来，从而创建出一条很长的平滑曲线。如果将一个点的控制点在它的另一侧建立一个对称点（斜率不变），可以通过一个简写的命令来实现:``S or s``

S命令可以用来创建与之前那些曲线一样的贝塞尔曲线，但是，如果S命令跟在一个C命令或者另一个S命令的后面，它的第一个控制点，就会被假设成前一个控制点的对称点。如果S命令单独使用，前面没有C命令或者另一个S命令，那么它的两个控制点就会被假设为同一个点。
{% highlight html %}
<!-- S x2 y2, x y (or s dx2 dy2, dx dy) -->
<path d="M10 80 C 40 10, 65 10, 95 80 S 150 150, 180 80" stroke="black" fill="transparent"/>
{% endhighlight %}

###二次贝塞尔曲线:``Q``
{% highlight html %}
<!-- Q x1 y1, x y (or q dx1 dy1, dx dy) -->
<!-- 两组参数，控制点和终点坐标 -->
<path d="M10 80 Q 95 10 180 80" stroke="black" fill="transparent"/>

<!-- T x y (or t dx dy) -->
<!-- 就像三次贝塞尔曲线有一个S命令，二次贝塞尔曲线有
一个差不多的T命令，可以通过更简短的参数，延长二次贝塞尔曲线。 -->
<path d="M10 80 Q 52.5 10, 95 80 T 180 80" stroke="black" fill="transparent"/>
{% endhighlight %}

###弧形:``A``
不好理解，物理学得不好，直接看例子
{% highlight html %}
<!-- A rx ry x-axis-rotation large-arc-flag sweep-flag x y-->
<path d="M10 315
           L 110 215
           A 30 50 0 0 1 162.55 162.45
           L 172.55 152.45
           A 30 50 -45 0 1 215.1 109.9
           L 315 10" stroke="black" fill="green" stroke-width="2" fill-opacity="0.5"/>
{% endhighlight %}

----------

##填充与边框
在SVG绘图中，可以使用若干方法上色，比如给图形对象增加指定的属性，使用行间CSS，使用CSS嵌入段落，或者使用外部引用的CSS文件。

###fill（填充）和stroke（边框）

####上色
{% highlight html %}
<!-- 大多数基本的颜色可以使用fill和stroke两个属性来设置。
fill设置的是对象的填充色，stroke设置的是对象的边框颜色。
SVG中你可以分别定义填充色和边框色的透明度，它们分别由 fill-opacity 和 stroke-opacity 两个属性控制。
-->
<rect x="10" y="10" width="100" height="100" stroke="blue" fill="purple"

       fill-opacity="0.5" stroke-opacity="0.8"/>
{% endhighlight %}

####边框

- ``stroke-width`` : 边框的粗细
- ``stroke-linecap`` : 边框的形状 可选项有3种，butt表示用直边结束边框，square的效果差不多，但是会稍微超出path的范围，超出的大小是stroke-width控制的。round表示边框的终点是圆角，圆角的半径也是stroke-width控制的
- ``stroke-linejoin`` : 控制两条边框线段之间，用什么方式连接。它有三个可用的值，miter是默认值，表示用方形画笔在连接处形成直角，round表示用圆角连接，实现平滑效果。最后还有一个值bevel，连接处会形成一个斜线
- ``stroke-dasharray`` : 将边框定义成虚线,参数是一组用逗号分割的数字组成的序列.这组序列表示虚线中实线和空白的长度。

###Use CSS
- 可以像普通元素一样定义SVG的样式
- 在html里这样的段落一般放在里，在svg则放在<defs>标签里。<defs>表示定义，这里可以定义一些不会在SVG图形中出现的元素，但是它们可以被其他元素使用，例如
{% highlight html %}
<?xml version="1.0" standalone="no"?>
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <style type="text/css"><![CDATA[
       #MyRect {
         stroke: black;
         fill: red;
       }
    ]]></style>
  </defs>
  <rect x="10" height="180" y="10" width="180" id="MyRect"/>
</svg>
{% endhighlight %}