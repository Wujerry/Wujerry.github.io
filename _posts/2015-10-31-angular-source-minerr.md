---
layout: post
title:  "AngularJS 源码分析 - minErr.js"
description: "AngularJS 源码分析 - minErr.js"
modified: 2015-10-31 15:53:01
tags: [angular,javascript]
comments: true
share: true
---
###文件
``minErr.js``

###代码 && 注释
{% highlight javascript %} 
'use strict';

/**
 * @描述
 *
 * 这个对象提供一个在angular中打印详细错误信息的工具。
 * 使用示例如下：
 *
 * var exampleMinErr = minErr('example');  // 调用minErr() , 返回一个Error对象 
 * throw exampleMinErr('one', 'This {0} is {1}', foo, bar);  // 抛出错误
 *
 * 上面的代码在 example 命名空间下创建了一个minErr的实例。抛出的错误在
 * 命名空间 example.one 下，第二个参数错误信息中的{0}和{1}会被后面的参数依次替换，
 * 替换的参数数量没有限制。
 *
 * 如果参数少于模板中定义的数量，多余的标记不会被替换。
 * 
 * 由于在build步骤中数据被静态传递，所有minErr的实例的创建和调用必须要遵循一定
 * 的限制。minErr实例在创建时必须要有命名空间(如: minErr('namespace'))。
 * 错误代码、命名空间和模板字符串必须是静态的，不能是变量或者一般的表达式。
 * 
 * @param {string} module 命名空间
 * @param {function} ErrorConstructor 自定义错误构造对象
 * @returns {function(code:string, template:string, ...templateArgs): Error} minErr 实例
 */

function minErr(module, ErrorConstructor) {
  ErrorConstructor = ErrorConstructor || Error;
  return function() {
    var SKIP_INDEXES = 2;

    var templateArgs = arguments,
      code = templateArgs[0],
      message = '[' + (module ? module + ':' : '') + code + '] ',
      template = templateArgs[1],
      paramPrefix, i;

    message += template.replace(/\{\d+\}/g, function(match) {
      var index = +match.slice(1, -1),
        shiftedIndex = index + SKIP_INDEXES;

      if (shiftedIndex < templateArgs.length) {
        return toDebugString(templateArgs[shiftedIndex]);
      }

      return match;
    });

    message += '\nhttp://errors.angularjs.org/"NG_VERSION_FULL"/' +
      (module ? module + '/' : '') + code;

    for (i = SKIP_INDEXES, paramPrefix = '?'; i < templateArgs.length; i++, paramPrefix = '&') {
      message += paramPrefix + 'p' + (i - SKIP_INDEXES) + '=' +
        encodeURIComponent(toDebugString(templateArgs[i]));
    }

    return new ErrorConstructor(message);
  };
}

{% endhighlight %}




> Written with [StackEdit](https://stackedit.io/).