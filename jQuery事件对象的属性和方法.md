---
title: jQuery事件对象的属性和方法
date: 2017-02-16 11:17:59
tags:
categories: [jQuery仓库]
---
常用的事件对象的属于与方法
<!--more-->
#### event.type：获取事件的类型
触发元素的事件类型
```js
$("a").click(function(event) {
  alert(event.type); // "click"事件
});
```
#### event.pageX 和 event.pageY：获取鼠标当前相对于页面的坐标
通过这2个属性，可以确定元素在当前页面的坐标值，鼠标相对于文档的左边缘的位置（左边）与 （顶边）的距离，简单来说是从页面左上角开始,即是以页面为参考点,不随滑动条移动而变化
#### event.preventDefault() 方法：阻止默认行为
这个用的特别多，在执行这个方法后，如果点击一个链接（a标签），浏览器不会跳转到新的 URL 去了。我们可以用 event.isDefaultPrevented() 来确定这个方法是否(在那个事件对象上)被调用过了
#### event.stopPropagation() 方法：阻止事件冒泡
事件是可以冒泡的，为防止事件冒泡到DOM树上，也就是不触发的任何前辈元素上的事件处理函数
#### event.which：获取在鼠标单击时，单击的是鼠标的哪个键
event.which 将 event.keyCode 和 event.charCode 标准化了。event.which也将正常化的按钮按下(mousedown 和 mouseupevents)，左键报告1，中间键报告2，右键报告3
#### event.currentTarget : 在事件冒泡过程中的当前DOM元素
冒泡前的当前触发事件的DOM对象, 等同于this.
#### this和event.target的区别：
js中事件是会冒泡的，所以this是可以变化的，但event.target不会变化，它永远是直接接受事件的目标DOM元素；
.this和event.target都是dom对象
如果要使用jquey中的方法可以将他们转换为jquery对象。比如this和$(this)的使用、event.target和$(event.target)的使用；