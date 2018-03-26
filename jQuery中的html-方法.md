---
title: jQuery中的html()方法
date: 2017-02-12 13:31:11
tags:
categories: [jQuery仓库]
---
#### .html()方法 
获取集合中第一个匹配元素的HTML内容 或 设置每一个匹配元素的html内容
<!--more-->
具体有3种用法：
1. .html() 不传入值，就是获取集合中第一个匹配元素的HTML内容
2. .html( htmlString )  设置每一个匹配元素的html内容
3. .html( function(index, oldhtml) ) 用来返回设置HTML内容的一个函数

###注意事项：
.html()方法内部使用的是DOM的innerHTML属性来处理的，所以在设置与获取上需要注意的一个最重要的问题，这个操作是针对整个HTML内容（不仅仅只是文本内容）

```js
<script type="text/javascript">
        //通过.html()方法替换html结构
        $("div:first").html('整个div的子节点都被替换了')
</script>
```