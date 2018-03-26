---
title: 查找数组中的索引inArray
date: 2017-02-17 10:27:44
tags:
categories: [jQuery仓库]
---
等同ECMAScript5的indexOf
<!--more-->
jQuery.inArray()函数用于在数组中搜索指定的值，并返回其索引值。如果数组中不存在该值，则返回 -1。
#### 语法：
```js
jQuery.inArray( value, array ,[ fromIndex ] )
```
ECMAScript5中indexOf用法
```js
var str="Hello world!"
document.write(str.indexOf("Hello") + "<br />") //0
document.write(str.indexOf("World") + "<br />") //-1
document.write(str.indexOf("world")) // 6
```
用法非常简单，传递一个检测的目标值，然后传递原始的数组，可以通过fromIndex规定查找的起始值，默认数组是0开始
例如：在数组中查找值是5的索引
```js
$.inArray(5,[1,2,3,4,5,6,7]) //返回对应的索引：4
```