---
title: jQuery中的removeAttr()方法
date: 2017-02-12 14:34:11
tags:
categories: [jQuery仓库]
---
#### removeAttr()删除方法
.removeAttr( attributeName ) : 为匹配的元素集合中的每个元素中移除一个属性（attribute）
<!--more-->
学习代码：
```js
//从任何 p 元素中移除 id 属性：
$("button").click(function(){
  $("p").removeAttr("id");
});
```