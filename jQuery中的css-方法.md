---
title: jQuery中的css()方法
date: 2017-02-12 13:07:16
tags: 
categories: [jQuery仓库]
---
#### .css() 方法：获取元素样式属性的计算值或者设置元素的CSS属性
<!--- more -->
#### 获取：
1. .css( propertyName ) ：获取匹配元素集合中的第一个元素的样式属性的计算值
2. .css( propertyNames )：传递一组数组，返回一个对象结果
#### 设置：
1. .css(propertyName, value )：设置CSS
2. .css( propertyName, function )：可以传入一个回调函数，返回取到对应的值进行处理
3. .css( properties )：可以传一个对象，同时设置多个样式
#### 注意事项：
1. 浏览器属性获取方式不同，在获取某些值的时候都jQuery采用统一的处理，比如颜色采用RBG，尺寸采用px
2. .css()方法支持驼峰写法与大小写混搭的写法，内部做了容错的处理
当一个数只被作为值（value）的时候， jQuery会将其转换为一个字符串，并添在字符串的结尾处添加px，例如 .css("width",50}) 与 .css("width","50px"})一样
学习代码：

```js
<script type="text/javascript">
        //多种写法设置颜色
        $('.fourth').css("background-color", "red")
        // $('.fifth').get(0).style.background="yellow"
        $('.fifth').css("backgroundColor", "yellow")
    </script>
    <script type="text/javascript">
        //多种写法设置字体大小
        $('.fourth').css("font-size", "15px")
        $('.fifth').css("foontSize", "0.9em")
    </script>
```