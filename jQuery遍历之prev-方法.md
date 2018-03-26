---
title: jQuery遍历之prev()方法
date: 2017-02-15 13:20:33
tags:
categories: [jQuery仓库]
---
快速查找指定元素集合中每一个元素紧邻的前面同辈元素的元素集合
<!--more-->
#### 理解节点查找关系：
class="item-1"就是class="item-2"的兄弟节点
```html
<ul class="level-3">
    <li class="item-1">1</li>
    <li class="item-2">2</li>
    <li class="item-3">3</li>
</ul>
```
#### prev()无参数
取得一个包含匹配的元素集合中每一个元素紧邻的前一个同辈元素的元素集合
```html
<ul>
     <li class="item-1">1</li>
     <li class="item-2">2</li>
     <li class="item-3">3</li>
</ul>
```
```js
  $('.item-2').prev().css('border', '1px solid red')
  //找到class=item-2所对应的上一个兄弟节点
```
#### prev()方法选择性地接受同一类型选择器表达式
同样的也是因为jQuery是合集对象，可能需要对这个合集对象进行一定的筛选，找出目标元素，所以允许传一个选择器的表达式
```js
  //找到class=item-2
  //然后筛选出最后一个，加上蓝色的边
  $('.item-3').prev(':last').css('border', '1px solid blue')
```