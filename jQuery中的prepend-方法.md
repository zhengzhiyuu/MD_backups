---
title: jQuery中的prepend()方法
date: 2017-02-12 21:12:34
tags:
categories: [jQuery仓库]
---
prepend()方法将指定元素插入到匹配元素里面作为它的第一个子元素 (如果要作为最后一个子元素插入用.append())
<!--more-->
对于.prepend() 而言，选择器表达式写在方法的前面，作为待插入内容的容器，将要被插入的内容作为方法的参数
```js
<script type="text/javascript">
    $("#bt1").on('click', function() {
        //找到class="aaron1"的div节点
        //然后通过prepend在内部的首位置添加一个新的p节点
        $('.aaron1').prepend('<p>prepend增加的p元素</p>')
    })
</script>
```