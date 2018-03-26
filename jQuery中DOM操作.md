---
title: jQuery中DOM操作
date: 2017-02-12 19:56:05
tags: jQuery
categories: [前端,jQuery]
---
大神都是从DOM开始的
<!--more-->
### JavaScript中的一点原生方法：
- 创建元素：document.createElement
- 设置属性：setAttribute
- 添加文本：innerHTML
- 加入文档：appendChild
### DOM节点的创建
```js
<script type="text/javascript">
    var $body = $('body');
    $body.on("click",function() {
        //通过jQuery生成div元素节点
        var div = $("<div>动态创建DIV元素节点</div>")
        //通过jQuery生成div属性节点
        var div1 = $("<div id='test' class='aaron'>创建为属性节点</div>")
        $body.append(div)
        $body.append(div1)        
    })
</script>
```
### DOM节点的插入 ###
 #### 　　　DOM内部插入{% post_link jQuery中的append-方法 append() %} 与 {% post_link jQuery中的appendTo-方法 appendTo() %} 
- append(content):向每一个匹配的元素内部追加内容
- appendTo(content):把所有匹配的元素追加到另一个指定的元素集合中
 #### DOM外部插入{% post_link jQuery中的after-方法 after() %} 与 {% post_link jQuery中的befor-方法 before() %} 
- after(content):在匹配元素集合在中的每一个元素后面插入参数所制定的内容作为其兄弟元素
- before(content):根据参数设定，在匹配元素的前面插入内容
 #### DOM内部插入{% post_link jQuery中的prepend-方法 prepend() %} 与 {% post_link jQuery中的prependTo-方法 prependTo() %} 
- prepend(content):向每个匹配的元素内部前置内容
- prependTo(content):把所有匹配的元素前置到另一个指定的元素集合中
 #### DOM内部插入{% post_link jQuery中的insertAfter-方法 insertAfter() %} 与 {% post_link jQuery中的insertBefore-方法 insertBefore() %} 
- insertAfter():在目标元素前面插入集合中每个匹配的元素
- insertBefore():在目标元素后面插入集合中每个匹配的元素
### DOM节点的删除
- #### {% post_link DOM节点删除之empty-的基本用法 DOM节点删除之empty()的基本用法 %}
- #### {% post_link remove-的有参用法和无参用法 remove()的有参用法和无参用法 %}
- #### {% post_link 保留数据的删除操作detach 保留数据的删除操作detach() %}
### DOM节点的复制与替换
- #### {% post_link DOM拷贝clone DOM拷贝clone() %}
- #### {% post_link DOM替换replaceWith-和replaceAll DOM替换replaceWith()和replaceAll() %}
- #### {% post_link DOM包裹wrap-方法 DOM包裹wrap()方法 %}
wrap是针对单个dom元素处理
- #### {% post_link DOM删除包裹unwrap-方法 DOM删除包裹unwrap()方法 %}
unwrap是针对单个dom元素处理
- #### {% post_link DOM包裹wrapAll-方法 DOM包裹wrapAll()方法 %}
wrapAll是针对集合dom元素处理
- #### {% post_link DOM删除包裹wrapInner-方法 DOM删除包裹wrapInner()方法 %}
wrapInner是针对集合dom元素处理
