---
title: mousemove事件
date: 2017-02-15 16:13:26
tags:
categories: [jQuery仓库]
---
mousemove方法可以监听用户鼠标移动的操作
<!--more-->
#### 方法一：$ele.mousemove()
绑定$ele元素，不带任何参数一般是用来指定触发一个事件，用的比较少
```html
<div id="test">点击触发<div>
```
```js
$("ele").mousemove(function(){
    alert('触发指定事件')
})
$("#test").click(function(){
     $("ele").mousemove()  //指定触发事件 
});
```
#### 方法二：$ele.mousemove( handler(eventObject) )
绑定$ele元素，每次$ele元素触发点击操作会执行回调 handler函数
这样可以针对事件的反馈做很多操作了
```html
<div id="test">滑动触发<div>
```
```js
$("#test").mousemove(function() {
    //this指向 div元素 
});
```
像:
```js
 //绑定一个mousemove事件
    //触发后修改内容
    $(".aaron1").mousemove(function(e) {
        $(this).find('p:last').html('移动的X位置：' + e.pageX)
    })
```
#### 方法三：$ele.mousemove( [eventData ], handler(eventObject) )
使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题
```html
<div id="test">点击触发<div>
```
```js
$("#test").mousemove(11111,function(e) {
    //this指向 div元素
    //e.date  => 11111 传递数据
});
```
像：
```js
//不同函数传递数据
    function data(e) {
        $(this).find('p:last').html('数据:' + e.data)
    }

    function a() {
        $(".right").mousemove(1111, data)
    }
    a();
```