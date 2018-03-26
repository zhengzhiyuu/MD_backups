---
title: jQuery中的insertBefore()方法
date: 2017-02-13 12:55:48
tags:
categories: [jQuery仓库]
---
.before()和.insertBefore()实现同样的功能。主要的区别是语法——内容和目标的位置。 对于before()选择表达式在函数前面，内容作为参数，而.insertBefore()刚好相反，内容在方法前面，它将被放在参数里元素的前面
<!--more-->
insertBefore将JQuery封装好的元素插入到指定元素的前面，如果元素前面有元素了，那将前面的元素前移，然后将JQuery对象插入
```js
<script type="text/javascript">
    $("#bt1").on('click', function() {
        //在test1元素前后插入集合中每个匹配的元素
        //不支持多参数
        $('<p style="color:red">测试insertBefore方法增加</p>').insertBefore($(".test1"))
    })
</script>
```