---
title: jQuery中的insertAfter()方法
date: 2017-02-13 12:43:23
tags:
categories: [jQuery仓库]
---
.after()和.insertAfter() 实现同样的功能。主要的不同是语法——特别是（插入）内容和目标的位置。 对于after()选择表达式在函数的前面，参数是将要插入的内容。对于 .insertAfter(), 刚好相反，内容在方法前面，它将被放在参数里元素的后面
<!--more-->
insertAfter将JQuery封装好的元素插入到指定元素的后面，如果元素后面有元素了，那将后面的元素后移，然后将JQuery对象插入
```js
    <script type="text/javascript">
    $("#btn1").on('click', function() {
        //在box元素前后插入集合中每个匹配的元素
        //不支持多参数
        $('<p style="color:red">测试insertAfter方法增加</p>').insertAfter($(".box"))
    })
    </script>
```