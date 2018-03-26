---
title: jQuery遍历之parent()方法
date: 2017-02-15 10:57:18
tags:
categories: [jQuery仓库]
---
快速查找合集里面的每一个元素的父元素（这里可以理解为就是父亲-儿子的关系）
<!--more-->
#### 理解节点查找关系：
```html
<div class="div">
    <ul class="son">
        <li class="grandson">1</li>
    </ul>
</div>
```
查找ul的父元素div
```js
$(ul).parent()
```
#### parent()无参数
parent()方法允许我们能够在DOM树中搜索到这些元素的父级元素，从有序的向上匹配元素，并根据匹配的元素创建一个新的 jQuery 对象
```js
$("button:first").click(function() {
        $('.div').parent().css("border","1px solid red")
        /*
        找到所有class=div的元素
        找到它的父元素,并且加上一个红色的边框
        */
})
```
#### parent()方法选择性地接受同一型选择器表达式
同样的也是因为jQuery是合集对象，可能需要对这个合集对象进行一定的筛选，找出目标元素，所以允许传一个选择器的表达式
```js
$("button:last").click(function() {
        //找到所有class=item的父元素
        //然后筛选出最后一个，加上蓝色的边
       $('.item').parent(':last').css('border', '1px solid blue')
})
```
