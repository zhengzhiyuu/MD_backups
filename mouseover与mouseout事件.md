---
title: mouseover与mouseout事件
date: 2017-02-15 16:53:14
tags:
categories: [jQuery仓库]
---
监听用户的移入移出操作
<!--more-->
#### 方法一：$ele.mouseover()
绑定$ele元素，不带任何参数一般是用来指定触发一个事件，用的比较少
```html
<div id="test">点击触发<div>
```
```js
$("ele").mouseover(function(){
    alert('触发指定事件')
})
$("#test").click(function(){
     $("ele").mouseover()  //指定触发事件 
});
```
#### 方法二：$ele.mouseover( handler(eventObject) )
绑定$ele元素，每次$ele元素触发点击操作会执行回调 handler函数
这样可以针对事件的反馈做很多操作了
```html
<div id="test">滑动触发<div>
```
```js
$("#test").mouseover(function() {
    //this指向 div元素 
});
```
#### 方法三：$ele.mouseover( [eventData ], handler(eventObject) )
使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题
```html
<div id="test">点击触发<div>
```
```js
$("#test").mouseover(11111,function(e) {
    //this指向 div元素
    //e.date  => 11111 传递数据
});
```