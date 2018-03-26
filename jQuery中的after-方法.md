---
title: jQuery中的after()方法
date: 2017-02-12 21:00:50
tags:
categories: [jQuery仓库]
---
after()前面是被插入的对象，后面是要在对象内插入的元素内容
<!--more-->
#### 注意：
after向元素的后边添加html代码，如果元素后面有元素了，那将后面的元素后移，然后将html代码插入
```js
<script type="text/javascript">
    $("#bt1").on('click', function() {
        //在匹配test1元素集合中的每个元素后面插入p元素
        $(".test2").after('<p style="color:blue">after,在匹配元素之后增加</p>', '<p style="color:blue">多参数</p>')

    })
</script>
```