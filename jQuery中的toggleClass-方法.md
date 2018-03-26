---
title: jQuery中的toggleClass()方法
date: 2017-02-12 14:14:54
tags:
categories: [jQuery仓库]
---
#### .toggleClass( )方法：
在匹配的元素集合中的每个元素上添加或删除一个或多个样式类,取决于这个样式类是否存在或值切换属性。即：如果存在（不存在）就删除（添加）一个类
<!--more-->
1. .toggleClass( className )：在匹配的元素集合中的每个元素上用来切换的一个或多个（用空格隔开）样式类名
2. .toggleClass( className, switch )：一个布尔值，用于判断样式是否应该被添加或移除
3. .toggleClass( [switch ] )：一个用来判断样式类添加还是移除的 布尔值
4. toggleClass( function(index, class, switch) [, switch ] )：用来返回在匹配的元素集合中的每个元素上用来切换的样式类名的一个函数。接收元素的索引位置和元素旧的样式类作为参数
#### 注意事项：
1. toggleClass是一个互斥的逻辑，也就是通过判断对应的元素上是否存在指定的2. toggleClass会保留原有的Class名后新增，通过空格隔开

学习代码:
```js
<script type="text/javascript">
    //给所有的tr元素加一个class="c"的样式
    $("#table tr").toggleClass("c");

    //给所有的偶数tr元素切换class="c"的样式
    //所有基数的样式保留，偶数的被删除
    $("#table tr:odd").toggleClass("c");
</script>
```