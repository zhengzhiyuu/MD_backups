---
title: DOM元素的获取index方法
date: 2017-02-17 10:44:50
tags:
categories: [jQuery仓库]
---
.index()方法，从匹配的元素中搜索给定元素的索引值，从0开始计数
<!--more-->
#### 语法：
参数接受一个jQuery或者dom对象作为查找的条件
```js
.index()
.index( selector )
.index( element )
```
- 如果不传递任何参数给 .index() 方法，则返回值就是jQuery对象中第一个元素相对于它同辈元素的位置
- 如果在一组元素上调用 .index() ，并且参数是一个DOM元素或jQuery对象， .index() 返回值就是传入的元素相对于原先集合的位置
- 如果参数是一个选择器， .index() 返回值就是原先元素相对于选择器匹配元素的位置。如果找不到匹配的元素，则 .index() 返回 -1
简单来说：
```html
<ul>
    <a></a>
    <li id="test1">1</li>
    <li id="test2">2</li>
    <li id="test3">3</li>
</ul>
```
` $("li").index() ` 没有传递参数，返回的结果是1，它的意思是返回同辈的排列循序，第一个li之前有a元素,同辈元素是a开始为0，所以li的开始索引是1
如果要快速找到第二个li在列表中的索引,可以通过如下2种方式处理
```js
$("li").index(document.getElementById("test2")) //结果：1
$("li").index($("#test2"))  //结果:1
```