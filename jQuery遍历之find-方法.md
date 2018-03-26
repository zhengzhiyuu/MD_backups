---
title: jQuery遍历之find()方法
date: 2017-02-15 10:32:12
tags:
categories: [jQuery仓库]
---
快速查找DOM树中的元素的后代元素
<!--more-->
注意 children与find方法的区别，children是父子关系查找，find是后代关系（包含父子关系）
#### 理解节点查找关系：
```html
<div class="div">
    <ul class="son">
        <li class="grandson">1</li>
    </ul>
</div>
```
代码如果是$("div").find("li")，此时，li与div是祖辈关系，通过find方法就可以快速的查找到了
#### .find()方法要注意的知识点：
find是遍历当前元素集合中每个元素的后代。只要符合，不管是儿子辈，孙子辈都可以。
与其他的树遍历方法不同，选择器表达式对于 .find() 是必需的参数。如果我们需要实现对所有后代元素的取回，可以传递通配选择器 '*'。
find只在后代中遍历，不包括自己。
选择器 context 是由 .find() 方法实现的；因此，$('.item-ii').find('li') 等价于 $('li', '.item-ii')(找到类名为item-ii的标签下的li标签)
#### 注意重点：
.find()和.children()方法是相似的
1.children只查找第一级的子节点
2.find查找范围包括子节点的所有后代节点
代码：
```js
$("button:first").click(function() {
        $(".left").find("li:last").css("border","1px solid red")
        /*
        在class="left"的元素中
        找到后代元素li中的最后一个
        并加上红色的边框
        */ 
})
```
```js
$("button:last").click(function() {
        //找到所有p元素，然后筛选出子元素是span标签的节点
        //改变其字体颜色
        var $spans = $('span');
        $("p").find($spans).css('color', 'red');
})
```