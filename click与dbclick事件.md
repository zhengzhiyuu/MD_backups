---
title: click与dbclick事件
date: 2017-02-15 15:31:05
tags:
categories: [jQuery仓库]
---
click方法用于监听用户单击操作;dbclick方法用于监听用户双击操作
<!--more-->
#### 方法一：$ele.click()
绑定$ele元素，不带任何参数一般是用来指定触发一个事件，用的比较少
```html
<div id="test">点击触发<div>
```
```js
$("ele").click(function(){
    alert('触发指定事件')
})
$("#test").click(function(){
     $("ele").click()  
     //手动指定触发事件 
});
```
#### 方法二：$ele.click( handler(eventObject) )
绑定$ele元素，每次$ele元素触发点击操作会执行回调 handler函数，这样可以针对事件的反馈做很多操作了，方法中的this是指向了绑定事件的元素
```html
<div id="test">点击触发<div>
```
```js
$("#test").click(function() {
    //this指向 div元素
});
```
#### 方法三：$ele.click( [eventData ], handler(eventObject) )
使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题
```html
<div id="test">点击触发<div>
```
```js
$("#test").click(11111,function(e) {
    //this指向 div元素
    //e.date  => 11111 传递数据
});
```
像：
```js
 //不同函数传递数据
    function data(e) {
        alert(e.data) //1111
     }

    function a() {
          $("button:eq(2)").click(1111, data)
     }
    a();
```
dblclick()的用法和click()的用法是类似的，可以参考以上click()的用法