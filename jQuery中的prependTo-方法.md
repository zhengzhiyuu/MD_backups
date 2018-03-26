---
title: jQuery中的prependTo()方法
date: 2017-02-12 21:16:20
tags:
categories: [jQuery仓库]
---
.prepend()和.prependTo()实现同样的功能，主要的不同是语法，插入的内容和目标的位置不同
<!--more-->
对于.prependTo() 而言，将要被插入的内容写在方法的前面，可以是选择器表达式或动态创建的标记，待插入内容的容器作为参数
```js
<script type="text/javascript">
    $("#bt2").on('click', function() {
        //找到class="aaron2"的div节点
        //然后通过prependTo内部的首位置添加一个新的p节点
        $('<p>prependTo增加的p元素</p>').prependTo($('.aaron2'))
    })
</script>
```