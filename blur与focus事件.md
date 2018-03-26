---
title: blur与focus事件
date: 2017-02-15 18:44:55
tags:
categories: [jQuery仓库]
---
focusin事件,focusout事件与focus,blur事件
聚焦focus　失焦blur
<!--more-->
#### 区别：
是否支持冒泡处理
例子
```html
<div>
  <input type="text" />
</div>
```
其中input元素可以触发focus()事件
div是input的父元素，当它包含的元素input触发了focus事件时，它就产生了focusin()事件。
focus()在元素本身产生，focusin()在元素包含的元素中产生
blur与focusout也亦是如此