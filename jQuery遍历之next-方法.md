---
title: jQuery遍历之next()方法
date: 2017-02-15 12:50:48
tags:
categories: [jQuery仓库]
---
查找指定元素集合中每一个元素紧邻的后面同辈元素的元素集合
<!--more-->
#### 理解节点查找关系：
class="item-2"是class="item-1"元素的兄弟元素
```html
<ul>
    <li class="item-1">1</li>
    <li class="item-2">2</li>
    <li class="item-3">3</li>
</ul>
```
#### next()无参数
允许我们找遍元素集合中紧跟着这些元素的直接兄弟元素，并根据匹配的元素创建一个新的 jQuery 对象
```html
<ul>
    <li class="item-1">1</li>
    <li class="item-2">2</li>
    <li class="item-3">3</li>
</ul>
```
```js
$("button:first").click(function() {
    $('.item-1').next().css('border', '1px solid red')
    //给class=item-2的li加上红色的边
})
```
#### next()方法选择性地接受同一类型选择器表达式
同样的也是因为jQuery是合集对象，可能需要对这个合集对象进行一定的筛选，找出目标元素，所以允许传一个选择器的表达式
```js
$("button:last").click(function() {
    //找到所有class=item-3的li
    //然后筛选出第一个li，加上蓝色的边
    $('.item-2').next(':first').css('border', '1px solid blue')
})
```