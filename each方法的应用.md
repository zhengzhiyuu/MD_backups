---
title: each方法的应用
date: 2017-02-16 18:54:55
tags:
categories: [jQuery仓库]
---
jQuery中有个很重要的核心方法each，大部分jQuery方法在内部都会调用each，其主要的原因的就是jQuery的实例是一个元素合集
<!--more-->
jQuery的大部分方法都是针元素合集的操作，所以jQuery会提供$(selector).each()来遍历jQuery对象
.each只是处理jQuery对象的方法，jQuery还提供了一个通用的jQuery.each方法，用来处理对象和数组的遍历
#### 语法
```js
jQuery.each(array, callback )
jQuery.each( object, callback )
```
第一个参数传递的就是一个对象或者数组，第二个是回调函数
```js
$.each(["anson", "安森"], function(index, value) {
   //index是索引,也就是数组的索引
   //value就是数组中的值了
});
```
each就是for循环方法的一个包装，内部就是通过for遍历数组与对象，通过回调函数返回内部迭代的一些参数，第一个参数是当前迭代成员在对象或数组中的索引值(从0开始计数)，第二个参数是当前迭代成员(与this的引用相同

jQuery.each()函数还会根据每次调用函数callback的返回值来决定后续动作。如果返回值为false，则停止循环(相当于普通循环中的break)；如果返回其他任何值，均表示继续执行下一个循环。
```js
$.each(["anson", "安森"], function(index, value) {
    return false; //停止迭代
});
```
示例：
```js
// 遍历数组元素
$.each(['anson', '安森'], function(i, item) {
    $anson.append("索引=" + i + " 元素=" + item);
});//索引=0元素=anson 索引=1元素=安森

// 遍历对象属性
$.each({
    name: "anson",
    age: 18
}, function(property, value) {
     $anson.append("属性名=" + property + "; 属性值=" + value);
});//属性名=name属性值=anson 属性名=age属性值=18
```