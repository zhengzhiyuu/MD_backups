---
title: DOM删除包裹unwrap()方法
date: 2017-02-15 09:12:14
tags:
categories: [jQuery仓库]
---
.unwarp()方法 ，作用与wrap方法是相反的。将匹配元素集合的父级元素删除，保留自身（和兄弟元素，如果存在）在原来的位置
<!--more-->
案例：
```html
<div>
    <p>p元素</p>
</div>
```
保留内部元素p,删除父元素div
```js
$('p').unwarp();
//找到p元素，然后调用unwarp方法，这样只会删除父辈div元素了
```
结果：
```html
<p>p元素</p>
```
参看：
```js
    <script type="text/javascript">
    $(".aaron1").on('click', function() {
        //找到所有p元素，删除父容器div
        $('p').unwrap('<div></div>')
    })
    </script>
    <script type="text/javascript">
    $(".aaron2").on('click', function() {
        //找到所有p元素，删除父容器div
        $('a').unwrap(function() {
            return '<div></div>';
        })
    })
    </script>
```