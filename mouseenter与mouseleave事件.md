---
title: mouseenter与mouseleave事件
date: 2017-02-15 17:02:53
tags:
categories: [jQuery仓库]
---
监听用户移动到内部的操作
<!--more-->
三种参数传递方式与mouseover和mouseout是一模一样
#### mouseenter事件和mouseover的区别
- 关键点就是：冒泡的方式处理问题
简单的例子：
mouseover为例：
```html
<div class="aaron2">
    <p>鼠标离开此区域触发mouseleave事件</p>
</div>
```
如果在p元素与div元素都绑定mouseover事件，鼠标在离开p元素，但是没有离开div元素的时候，触发的结果:
p元素响应事件
div元素响应事件
这里的问题是div为什么会被触发？ 原因就是事件冒泡的问题，p元素触发了mouseover，他会一直往上找父元素上的mouseover事件，如果父元素有mouseover事件就会被触发
所以在这种情况下面，jQuery推荐我们使用 mouseenter事件
#### mouseenter事件只会在绑定它的元素上被调用，而不会在后代节点上被触发