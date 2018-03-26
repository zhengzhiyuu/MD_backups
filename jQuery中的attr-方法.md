---
title: jQuery中的attr()方法
date: 2017-02-12 14:24:28
tags:
categories: [jQuery仓库]
---
jQuery中用attr()方法来获取和设置元素属性,attr是attribute（属性）的缩写，在jQuery DOM操作中会经常用到attr()
<!--more-->
#### attr()有4个表达式
1. attr(传入属性名)：获取属性的值
2. attr(属性名, 属性值)：设置属性的值
3. attr(属性名,函数值)：设置属性的函数值
4. attr(attributes)：给指定元素设置多个属性值，即：{属性名一: “属性值一” , 属性名二: “属性值二” , … … }
#### 注意的问题：
dom中有个概念的区分：Attribute和Property翻译出来都是“属性”，《js高级程序设计》书中翻译为“特性”和“属性”。简单理解，Attribute就是dom节点自带的属性
例如：html中常用的id、class、title、align等：
<div id="独一" title="无二"></div>
而Property是这个DOM元素作为对象，其附加的内容，例如,tagName, nodeName, nodeType,, defaultChecked, 和 defaultSelected 使用.prop()方法进行取值或赋值等
#### 获取Attribute就需要用attr，获取Property就需要用prop

学习代码：
```js
    <script type="text/javascript">
    	//找到第一个input，通过attr设置属性value的值
        $('input:first').attr('value','嗯哼')
    </script>
```