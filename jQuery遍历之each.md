---
title: jQuery遍历之each()
date: 2017-02-15 14:16:30
tags:
categories: [jQuery仓库]
---
each() 方法就是一个for循环的迭代器，它会迭代jQuery对象合集中的每一个DOM元素。每次回调函数执行时，会传递当前循环次数作为参数(从0开始计数)
<!--more-->
#### 重点：
- each是一个for循环的包装迭代器
- each通过回调的方式处理，并且会有2个固定的实参，索引与元素
- each回调方法中的this指向当前迭代的dom元素
#### 案例
```html
<ul>
    <li>item-1</li>
    <li>item-2</li>
</ul>
```
开始迭代li，循环2次
```js
$("li").each(function(index, element) {
     index 索引 0,1
     element 是对应的li节点 li,li
     this 指向的是li
})
```
代码
```js
//遍历所有的li
//修改每个li内的字体颜色
$("li").each(function(index, element) {
     $(this).css('color','red')
})
```
```js
(function() {
    //遍历所有的li
    //修改偶数li内的字体颜色
    $("li").each(function(index, element) {
        if (index % 2) {
              $(this).css('color','blue')
         }
     })
})
```