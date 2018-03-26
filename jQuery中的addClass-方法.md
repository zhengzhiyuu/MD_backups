---
title: jQuery中的addClass()方法
date: 2017-02-12 13:39:24
tags:
categories: [jQuery仓库]
---
#### .addClass( className )方法
1. .addClass( className ) : 为每个匹配元素所要增加的一个或多个样式名
2. .addClass( function(index, currentClass) ) : 这个函数返回一个或更多用空格隔开的要增加的样式名
<!--more-->
#### 注意事项：
.addClass()方法不会替换一个样式类名。它只是简单的添加一个样式类名到元素上
简单的描述下：在p元素增加一个newClass的样式：
```js
<p class="orgClass">
<script>
$("p").addClass("newClass")
</script>
```
那么p元素的class实际上是 class="orgClass newClass"样式只会在原本的类上继续增加，通过空格分隔