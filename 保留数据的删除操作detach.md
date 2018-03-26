---
title: 保留数据的删除操作detach()
date: 2017-02-13 13:55:59
tags:
categories: [jQuery仓库]
---
如果我们希望临时删除页面上的节点，但是又不希望节点上的数据与事件丢失，并且能在下一个时间段让这个删除的节点显示到页面，这时候就可以使用detach方法来处理
<!--more-->
#### 注意：
detach方法是JQuery特有的，所以它只能处理通过JQuery的方法绑定的事件或者数据
Html代码：
```js
<body>
    <p>P元素1，默认给绑定一个点击事件</p>
    <p>P元素2，默认给绑定一个点击事件</p>
    <button id="bt1">点击删除 p 元素</button>
    <button id="bt2">点击移动 p 元素</button>
</body>
```
JavaScript代码：
```js
<script type="text/javascript">
    var p;
    $("#bt1").click(function() {
        if (!$("p").length) return; //去重
        //通过detach方法删除元素
        //只是页面不可见，但是这个节点还是保存在内存中
        //数据与事件都不会丢失
        p = $("p").detach()
    });

    $("#bt2").click(function() {
        //把p元素在添加到页面中
        //事件还是存在
        $("body").append(p);
    });
</script>
```