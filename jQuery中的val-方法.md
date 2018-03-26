---
title: jQuery中的val()方法
date: 2017-02-12 14:42:55
tags:
categories: [jQuery仓库]
---
jQuery中有一个.val()方法主要是用于处理表单元素的值，比如 input, select 和 textarea
<!--more-->
#### .val()方法
1. .val()无参数，获取匹配的元素集合中第一个元素的当前值
2. .val( value )，设置匹配的元素集合中每个元素的值
3. .val( function ) ，一个用来返回设置值的函数
#### 注意事项：
1. 通过.val()处理select元素， 当没有选择项被选中，它返回null
2. .val()方法多用来设置表单的字段的值
3. 如果select元素有multiple（多选）属性，并且至少一个选择项被选中， .val()方法返回一个数组，这个数组包含每个选中选择项的值