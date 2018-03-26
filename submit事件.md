---
title: submit事件
date: 2017-02-16 08:51:20
tags:
categories: [jQuery仓库]
---
在表单提交的时候过滤一些的数据、做一些必要的操作（例如：验证表单输入的正确性，如果错误就阻止提交，从新输入）此时可以通过submit事件，监听下提交表单的这个动作
<!--more-->
#### 方法一：$ele.submit()
绑定$ele元素，不带任何参数一般是用来指定触发一个事件，用的比较少
```html
<div id="test">点击触发<div>
```
```js
$("ele").submit(function(){
    alert('触发指定事件')
})
$("#text").click(function(){
     $("ele").submit()  //指定触发事件 
});
 ```
#### 方法二：$ele.submit( handler(eventObject) )
绑定$ele元素，每次$ele元素触发点击操作会执行回调 handler函数
这样可以针对事件的反馈做很多操作了
```html
<form id="target" action="destination.html">
  <input type="submit" value="Go" />
</form>
```
```js
$("#target").submit(function() { //绑定提交表单触发
    //this指向 from元素 
});
```
#### 方法三：$ele.submit( [eventData ], handler(eventObject) )
使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题
```html
<form id="target" action="destination.html">
  <input type="submit" value="Go" />
</form>
```
```js
$("#target").submit(11111,function(data) { //绑定提交表单触发
    //data => 1111 //传递的data数据
});
```