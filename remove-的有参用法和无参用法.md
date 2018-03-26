---
title: remove()的有参用法和无参用法
date: 2017-02-13 13:49:17
tags:
categories: [jQuery仓库]
---
emove与empty一样，都是移除元素的方法，但是remove会将元素自身移除，同时也会移除元素内部的一切，包括绑定的事件及与该元素相关的jQuery数据
<!--more-->
Html代码：
 ```js
<body>
    <h2>通过jQuery remove方法移除元素</h2>
    <div class="test1">
        <p>p元素1</p>
        <p>p元素2</p>
    </div>
    <div class="test2">
        <p>p元素3</p>
        <p>p元素4</p>
    </div>
    <button>通过点击jQuery的empty移除元素</button>
    <button>通过点击jQuery的empty移除指定元素</button>
</body>
 ```
 JavaScript代码：
 ```js
<script type="text/javascript">
    $("button:first").on('click', function() {
        //删除整个 class=test1的div节点
        $(".test1").remove()
    })

    $("button:last").on('click', function() {
        //找到所有p元素中，包含了3的元素
        //这个也是一个过滤器的处理
        $("p").remove(":contains('3')")
    })
</script>
 ```