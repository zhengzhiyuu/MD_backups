---
title: DOM替换replaceWith()和replaceAll()
date: 2017-02-13 16:03:47
tags:
categories: [jQuery仓库]
---
#### .replaceWith( newContent )：用提供的内容替换集合中所有匹配的元素并且返回被删除元素的集合
简单来说：用$()选择节点A，调用replaceWith方法，传入一个新的内容B（HTML字符串，DOM元素，或者jQuery对象）用来替换选中的节点A
<!--more-->
学习代码,Html部分:
```html
<div>
    <p>第一段</p>
    <p>第二段</p>
    <p>第三段</p>
</div>
```
替换第二段的节点与内容:
```js
<script type="text/javascript">
//找到第二个p元素
//通过replaceWith删除并替换这个节点
$("p:eq(1)").replaceWith('<a style="color:red">替换第二段的内容</a>')
</script>
```
结果如下：
```html
<div>
    <p>第一段</p>
    <a style="color:red">替换第二段的内容</a>'
    <p>第三段</p>
</div>
```
#### .replaceAll( target ) ：用集合的匹配元素替换每个目标元素
.replaceAll()和.replaceWith()功能类似，但是目标和源相反，用上述的HTML结构，我们用replaceAll处理
```js
$('<a style="color:red">替换第二段的内容</a>').replaceAll('p:eq(1)')
```
- .replaceAll()和.replaceWith()功能类似，主要是目标和源的位置区别
- .replaceWith()与.replaceAll() 方法会删除与节点相关联的所有数据和事件处理程序
- .replaceWith()方法返回jQuery对象，所以可以和其他方法链接使用
- .replaceWith()方法返回的jQuery对象引用的是替换前的节点，而不是通过replaceWith/replaceAll方法替换后的节点
代码：
```js
$("#div").append($("p:eq(1)").replaceWith('<a style="color:red">replaceWith替换第二段的内容</a>'))
//找到第二个p标签，用·replaceWith()方法替换为颜色为红色的a标签，并把替换掉的添加到Id为div的标签中
```