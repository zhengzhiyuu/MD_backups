---
title: mousedown与mouseup事件
date: 2017-02-15 15:33:39
tags:
categories: [jQuery仓库]
---
mousedown方法可以监听用户鼠标按下的操作；mouseup方法可以监听用户鼠标弹起的操作
<!--more-->
#### 方法一：$ele.mousedown()
绑定$ele元素，不带任何参数一般是用来指定触发一个事件，可能一般用的比较少
```html
<div id="test">点击触发<div>
```
```js
$("ele").mousedown(function(){
    alert('触发指定事件')
})
$("#test").mousedown(function(){
     $("ele").mousedown()  //手动指定触发事件 
});
```
#### 方法二：$ele.mousedown( handler(eventObject) )
绑定$ele元素，每次$ele元素触发点击操作会执行回调 handler函数
这样可以针对事件的反馈做很多操作了
```html
<div id="test">点击触发<div>
```
```js
$("#test").mousedown(function() {
    //this指向 div元素
});
```
#### 方法三：$ele.mousedown( [eventData ], handler(eventObject) )
使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题
```html
<div id="test">点击触发<div>
```
```js
$("#test").mousedown(11111,function(e) {
    //this指向 div元素
    //e.date  => 11111 传递数据
});
```
像:
```js
//不同函数传递数据
    function data(e) {
        alert(e.data) //1111
    }

    function a() {
        $("button:eq(2)").mousedown(1111, data)
    }
    a();
```
mouseup与mousedown用法相似
#### mouseup事件触发需要以下几点：
- mouseup强调是松手触发，与mousedown是相反的
- mouseup与mousedown组合起来就是click事件
- 如果用户在一个元素上按下鼠标按键，并且拖动鼠标离开这个元素，然后释放鼠标键，这仍然是算作mouseup事件
任何鼠标按钮松手时都能触发mouseup事件
- 用event 对象的which区别按键，敲击鼠标左键which的值是1，敲击鼠标中键which的值是2，敲击鼠标右键which的值是3
#### click与mousedown的区别：
click事件其实是由mousedown于mouseup 2个动作构成，所以点击的动作只有在松手后才触发