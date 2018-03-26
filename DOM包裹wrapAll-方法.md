---
title: DOM包裹wrapAll()方法
date: 2017-02-15 09:21:18
tags:
categories: [jQuery仓库]
---
#### .wrapAll( wrappingElement )：
给集合中匹配的元素增加一个外面包裹HTML结构
<!--more-->
代码：
```html
<p>p元素</p>
<p>p元素</p>
```
给所有p元素增加一个div包裹
```js
$('p').wrapAll('<div></div>')
```
最后的结构，2个P元素都增加了一个父div的结构
```html
<div>
    <p>p元素</p>
    <p>p元素</p>
</div>
```
#### .wrapAll( function ) ：
一个回调函数，返回用于包裹匹配元素的 HTML 内容或 jQuery 对象
通过回调的方式可以单独处理每一个元素
以上面案例为例，
```js
$('p').wrapAll(function() {
    return '<div><div/>'; 
})
```