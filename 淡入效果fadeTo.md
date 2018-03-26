---
title: 淡入效果fadeTo
date: 2017-02-16 17:09:09
tags:
categories: [jQuery仓库]
---
淡入淡出fadeIn与fadeOut都是修改元素样式的opacity属性，但是他们都有个共同的特点，变化的区间要么是0，要么是1
fadeIn：淡入效果，内容显示，opacity是0到1
fadeOut：淡出效果，内容隐藏，opacity是1到0
fadeTo： 自定义透明度
#### 语法
```js
.fadeTo( duration, opacity ,callback)
```
必需的 duration参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。fadeTo() 方法中必需的 opacity 参数将淡入淡出效果设置为给定的不透明度（值介于 0 与 1 之间）。可选的 callback 参数是该函数完成后所执行的函数名称。
```js
$("p").fadeTo(1000, 0.2);
```