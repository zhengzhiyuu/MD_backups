---
title: DOM删除包裹wrapInner()方法
date: 2017-02-15 09:28:57
tags:
categories: [jQuery仓库]
---
.wrapInner( wrappingElement )：
给集合中匹配的元素的内部，增加包裹的HTML结构
<!--more-->
代码：
```html
<div>p元素</div>
<div>p元素</div>
```
给所有元素增加一个p包裹
```js
$('div').wrapInner('<p></p>')
```
最后的结构，匹配的div元素的内部元素被p给包裹了
```html
<div>
    <p>p元素</p>
</div>
<div>
    <p>p元素</p>
</div>
```
#### .wrapInner( function ) ：
允许我们用一个callback函数做参数，每次遇到匹配元素时，该函数被执行，返回一个DOM元素，jQuery对象，或者HTML片段，用来包住匹配元素的内容
```js
$('div').wrapInner(function() {
    return '<p></p>'; 
})
```