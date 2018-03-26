---
title: jQuery遍历之siblings()
date: 2017-02-15 13:49:26
tags:
categories: [jQuery仓库]
---
查找指定元素集合中每一个元素的同辈元素
<!--more-->
#### 理解节点查找关系：
class="item-1",class="item-3"就是class="item-2"兄弟节点
```html
<ul>
    <li class="item-1">1</li>
    <li class="item-2">2</li>
    <li class="item-3">3</li>
</ul>
```
#### siblings()无参数
取得一个包含匹配的元素集合中每一个元素的同辈元素的元素集合
```js
.siblings().css('border', '2px solid red')
//找到class=item-2的所有兄弟节点,然后加上红色的边
```
#### siblings()方法选择性地接受同一类型选择器表达式
```js
$("button:last").click(function() {
    //找到class=item-2的所有兄弟节点
    //然后筛选出最后一个，加上蓝色的边
    $('.item-2').siblings(':last').css('border', '2px solid blue')
})
```