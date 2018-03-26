---
title: 显示元素的show方法
date: 2017-02-16 13:37:17
tags:
categories: [jQuery仓库]
---
类似于display:block
<!--more-->
```js
$('elem').hide(3000).show(3000)
```
让元素执行3秒的隐藏动画，然后执行3秒的显示动画
#### 注意事项：
- show与hide方法是修改的display属性，通过是visibility属性布局需要通过css方法单独设置
- 如果使用!important在你的样式中，比如display: none !important，如果你希望.show()方法正常工作，必须使用.css('display', 'block !important')重写样式
- 如果让show与hide成为一个动画，那么默认执行动画会改变元素的高度，高度，透明度