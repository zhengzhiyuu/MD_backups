---
title: 淡入淡出切换fadeToggle
date: 2017-02-16 16:57:29
tags:
categories: [jQuery仓库]
---
fadeToggle()函数用于切换所有匹配的元素，并带有淡入/淡出的过渡动画效果
<!--more-->
```js
.fadeToggle( [duration ] ,[ complete ] )
```
可选的 duration 参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。 可选的 callback 参数是 fadeToggle完成后所执行的函数名称。
fadeToggle() 方法可以在 fadeIn() 与 fadeOut() 方法之间进行切换。如果元素已淡出，则 fadeToggle() 会向元素添加淡入效果。如果元素已淡入，则 fadeToggle() 会向元素添加淡出效果。