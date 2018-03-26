---
title: jQuery中的text()方法
date: 2017-02-12 13:36:14
tags:
categories: [jQuery仓库]
---
#### .text()方法
得到匹配元素集合中每个元素的文本内容结合，包括他们的后代，或设置匹配元素集合中每个元素的文本内容为指定的文本内容
<!--more-->
具体有3种用法：
1. .text() 得到匹配元素集合中每个元素的合并文本，包括他们的后代
2. .text( textString ) 用于设置匹配元素内容的文本
3. .text( function(index, text) ) 用来返回设置文本内容的一个函数
#### 注意事项：
.text()结果返回一个字符串，包含所有匹配元素的合并文本

```js
<script type="text/javascript">
        //通过.text()方法替换文本内容
        $("a:first").text('替换第一个a标签的内容')
</script>
```