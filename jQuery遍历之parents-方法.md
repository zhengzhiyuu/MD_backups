---
title: jQuery遍历之parents()方法
date: 2017-02-15 12:08:57
tags:
categories: [jQuery仓库]
---
类似find与children的区别，parent只会查找一级，parents则会往上一直查到查找到祖先节点
<!--more-->
#### 理解节点查找关系：
<div class="div">
    <ul class="son">
        <li class="grandson">1</li>
    </ul>
</div>
在li节点上找到祖辈元素div
```js
$("li").parents()
```
#### parents()无参数
parents()方法允许我们能够在DOM树中搜索到这些元素的祖先元素，从有序的向上匹配元素，并根据匹配的元素创建一个新的 jQuery 对象
返回的元素秩序是从离他们最近的父级元素开始的
```js
$("button:first").click(function() {
        $('.item').parents().css('border','1px solid red')
        //找到class="item"元素的所有祖辈元素并且附上一个红色的边框
})
```
#### parents()方法选择性地接受同一型选择器表达式
同样的也是因为jQuery是合集对象，可能需要对这个合集对象进行一定的筛选，找出目标元素，所以允许传一个选择器的表达式
```js
$("button:last").click(function() {
        //找到当前元素的所有祖辈元素,筛选出class="first-div"的元素
        //并且附上一个边
        $('.item').parents('.first-div').css('border', '2px solid blue')
})
```