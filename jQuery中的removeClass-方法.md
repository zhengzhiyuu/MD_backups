---
title: jQuery中的removeClass()方法
date: 2017-02-12 14:05:25
tags:
categories: [jQuery仓库]
---
#### .removeClass( )方法
1. .removeClass( [className ] )：每个匹配元素移除的一个或多个用空格隔开的样式名
2. .removeClass( function(index, class) ) ： 一个函数，返回一个或多个将要被移除的样式名
<!--more-->
#### 注意事项
如果一个样式类名作为一个参数,只有这样式类会被从匹配的元素集合中删除 。 如果没有样式名作为参数，那么所有的样式类将被移除

学习代码：
```js
    <script type="text/javascript"> 
        //class=left下div元素删除newClass样式
        $('.left div').removeClass('newClass')
    </script>
```
```js
    <script type="text/javascript"> 
        //.removeClass() 方法允许我们指定一个函数作为参数，返回将要被删除的样式
        $('.right > div:first').removeClass(function(index,className){
            
            //className = aa bb oClass
            //把div的className赋给下一个兄弟元素div上作为它的class
            $(this).next().addClass(className)

            //删除自己本身的oClass
            return 'oClass'
        })


    </script>
```