---
title: 隐藏元素的hide方法
date: 2017-02-16 13:26:59
tags:
categories: [jQuery仓库]
---
类似于设置css的display为none属性
<!--more-->
```js
$elem.hide()
```
##### 提供参数：
```js
.hide( options )
```
当提供hide方法一个参数时，.hide()就会成为一个动画方法。.hide()方法将会匹配元素的宽度，高度，以及不透明度，同时进行动画操作
##### 快捷参数：
```js
.hide("fast / slow")
```
这是一个动画设置的快捷方式，'fast' 和 'slow' 分别代表200和600毫秒的延时，就是元素会执行200/600毫秒的动画后再隐藏
代码：
```js
 $("div").hide( 3000,function() {
     alert('执行3000ms动画完毕')
})
```