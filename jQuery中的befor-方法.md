---
title: jQuery中的befor()方法
date: 2017-02-12 21:06:03
tags:
categories: [jQuery仓库]
---
befor()前面是要插入的元素内容，而后面是被插入的对象
<!--more-->
#### 注意：
before向元素的前边添加html代码，如果元素前面有元素了，那将前面的元素前移，然后将html代码插入
```js
<script type="text/javascript">
    $("#bt1").on('click', function() {
        //在匹配test1元素集合中的每个元素前面插入p元素
        $(".test1").before('<p style="color:red">before,在匹配元素之前增加</p>', '<p style="color:red">多参数</p>')
    })
</script>
```