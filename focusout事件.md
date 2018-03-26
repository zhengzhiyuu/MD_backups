---
title: focusout事件
date: 2017-02-15 18:33:43
tags:
categories: [jQuery仓库]
---
当一个元素，或者其内部任何一个元素失去焦点的时候，比如input元素，用户在点击失去焦的时候，如果开发者需要捕获这个动作，jQuery提供了一个focusout事件
<!--more-->
#### 方法一：$ele.focusout()
绑定$ele元素，不带任何参数一般是用来指定触发一个事件，可能一般用的比较少
```html
<div id="test">点击触发<div>
```
```js
$("ele").focusout(function(){
    alert('触发指定事件')
})
$("#test").mouseup(function(){
     $("ele").focusout()  //指定触发事件 
});
```
#### 方法二：$ele.focusout( handler )
绑定$ele元素，每次$ele元素触发点击操作会执行回调 handler函数
这样可以针对事件的反馈做很多操作了
```html
<div id="test">点击触发<div>
```
```js
$("#test").focusout(function() {
    //this指向 div元素
});
```
代码:
```js
//input失去焦点
//给input元素增加一个边框
$("input:first").focusout(function() {
    $(this).css('border','2px solid red')
})
```
#### 方法三：$ele.focusout( [eventData ], handler )
使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题
```html
<div id="test">点击触发<div>
```
```js
$("#test").focusout(11111,function(e) {
    //this指向 div元素
    //e.date  => 11111 传递数据
});
```