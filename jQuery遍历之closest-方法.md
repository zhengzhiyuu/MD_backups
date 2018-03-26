---
title: jQuery遍历之closest()方法
date: 2017-02-15 12:33:48
tags:
categories: [jQuery仓库]
---
#### closest()方法接受一个匹配元素的选择器字符串
从元素本身开始，在DOM 树上逐级向上级元素匹配，并返回最先匹配的祖先元素
例如：在div元素中，往上查找li元素，可以这样表达
```js
$("div").closet("li')
```
```js
$("button:first").click(function() {
    $('.item').closest('.level').css('border', '1px solid red')
    /*
    找到class="item"的li元素
    通过closest方法往上找到class=".level"的元素
    加上边框颜色
    */
})
```
#### .parents()和.closest()区别:
- 起始位置不同：
.closest开始于当前元素
.parents开始于父元素
- 遍历的目标不同：
.closest要找到指定的目标
.parents遍历到文档根元素
.closest向上查找，直到找到一个匹配的就停止查找
.parents一直查找到根元素，并将匹配的元素加入集合
- 结果不同：
.closest返回的是包含零个或一个元素的jquery对象
.parents返回的是包含零个或一个或多个元素的jquery对象