---
title: on()的多事件绑定
date: 2017-02-16 10:07:34
tags:
categories: [jQuery仓库]
---
基本用法：.on( events ,[ selector ] ,[ data ] )
<!--more-->
最常见的给元素绑定一个点击事件，对比一下快捷方式与on方式的不同
```js
$("#elem").click(function(){})  //快捷方式
$("#elem").on('click',function(){}) //on方式
```
最大的不同点就是on是可以自定义事件名
#### 多个事件绑定同一个函数
```js
 $("#elem").on("mouseover mouseout",function(){ });
 ```
通过空格分离，传递不同的事件名，可以同时绑定多个事件
#### 多个事件绑定不同函数
```js
$("#elem").on({
    mouseover:function(){},  
    mouseout:function(){},
});
```
通过空格分离，传递不同的事件名，可以同时绑定多个事件，每一个事件执行自己的回调方法
#### 将数据传递到处理程序
```js
function greet( event ) {
  alert( "Hello " + event.data.name ); //Hello anson
}
$( "button" ).on( "click", {
  name: "anson"
}, greet );
```
可以通过第二参数（对象），当一个事件被触发时，要传递给事件处理函数的
