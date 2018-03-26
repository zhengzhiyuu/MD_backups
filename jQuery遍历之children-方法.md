---
title: jQuery遍历之children()方法
date: 2017-02-15 09:59:57
tags:
categories: [jQuery仓库]
---
返回匹配元素集合中每个元素的子元素，添加可选参数可通过选择器进行过滤
<!--more-->
#### 理解节点查找关系：
```html
<div class="div">
    <ul class="son">
        <li class="grandson">1</li>
    </ul>
</div>
```
代码如果是$("div").children()，那么意味着只能找到ul，因为div与ul是父子关系，li与div是祖辈关系，因此无法找到
#### children()无参数
允许我们通过在DOM树中对这些元素的直接子元素进行搜索，并且构造一个新的匹配元素的jQuery对象
注意：jQuery是一个合集对象，所以通过children是匹配合集中每一给元素的第一级子元素
```js
 $("#bt1").click(function() {
    $(".div").children().css("color","red")
   //找到所有class=div的元素节点，然后找到其对应的子元素，改变颜色
})
```
#### .children()方法选择性地接受同一类型选择器表达式
$("div").children(".selected")
同样的也是因为jQuery是合集对象，可能需要对这个合集对象进行一定的筛选，找出目标元素，所以允许传一个选择器的表达式
```js
$("#bt2").click(function() {
    //找到所有class=div的元素
    //找到其对应的子元素ul，然后筛选出最后一个，给边宽加上颜色
    $('.div').children(':last').css('border', '3px solid blue')
})
```