---
title: hover事件
date: 2017-02-15 17:59:15
tags:
categories: [jQuery仓库]
---
hover　=　mouseenter　+　mouseleave
<!--more-->
在元素上移进移出切换其换色，一般通过2个事件配合就可以达到，这里用mouseenter与mouseleave，这样可以避免冒泡问题
```js
$(ele).mouseenter(function(){
     $(this).css("background", '#bbffaa');
 })
$(ele).mouseleave(function(){
    $(this).css("background", 'red');
})
```
等同于
```js
//只需要在hover方法中传递2个回调函数就可以了
//不需要显示的绑定2个事件
$(selector).hover(handlerIn, handlerOut)
```
- handlerIn(eventObject)：当鼠标指针进入元素时触发执行的事件函数
- handlerOut(eventObject)：当鼠标指针离开元素时触发执行的事件函数
代码：
```js
// hover()方法是同时绑定 mouseenter和 mouseleave事件。
// 我们可以用它来简单地应用在 鼠标在元素上行为
$("p").hover(
    function() {
          $(this).css("background", 'red');
    },
    function() {
          $(this).css("background", '#bbffaa');
    }
);
```