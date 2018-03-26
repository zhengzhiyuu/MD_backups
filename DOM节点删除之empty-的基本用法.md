---
title: DOM节点删除之empty()的基本用法
date: 2017-02-13 13:43:00
tags:
categories: [jQuery仓库]
---
empty()不仅移除子元素（和其他后代元素），同样移除元素里的文本
如果我们通过empty方法移除里面div的所有元素，它只是清空内部的html代码，但是标记仍然留在DOM中
<!--more-->
Html代码：
```js
<body>
    <h2>通过empty移除元素</h2>
    <div id="test">
        <p>p元素1</p>
        <p>p元素2</p>
    </div>
</body>
```
JavaScript代码：
```js
<button>点击通过jQuery的empty移除元素</button>
    <script type="text/javascript">
    $("button").on('click', function() {
        //通过empty移除了当前div元素下的所有p元素
        //但是本身id=test的div元素没有被删除
        $("#test").empty()
    })
</script>
```