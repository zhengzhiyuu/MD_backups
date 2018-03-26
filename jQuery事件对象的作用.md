---
title: jQuery事件对象的作用
date: 2017-02-16 11:02:44
tags:
categories: [jQuery仓库]
---
一个标准的"click"点击事件
```js
$(elem).on("click",function(event){
   event //事件对象
})
```
<!--more-->
```html
<ul>
    <li>点击：触发一</li>
    <!--触发的元素是内容是:点击：触发一-->
    <li>点击：触发二</li>
    <!--触发的元素是内容是:点击：触发二-->
    <li>点击：触发三</li>
    <!--触发的元素是内容是:点击：触发三-->
    <li>点击：触发四</li>
    <!--触发的元素是内容是:点击：触发四-->    
</ul>
```
```js
//多事件绑定
$("ul").on('click',function(e){
     alert('触发的元素是内容是: ' + e.target.textContent)
})
```
#### event.target
target 属性可以是注册事件时的元素，或者它的子元素。通常用于比较 event.target 和 this 来确定事件是不是由于冒泡而触发的。经常用于事件冒泡时处理事件委托
简单来说：event.target代表当前触发事件的元素，可以通过当前元素对象的一系列属性来判断是不是我们想要的元素