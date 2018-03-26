---
title: bootstrap斑马线表格
date: 2017-02-18 14:41:03
tags:
categories: [bootstrap仓库]
---
Bootstrap在` <table class="table"> `的基础上增加类名“.table-striped”即可：
<!--more-->
```html
<table class="table table-striped">
…
</table>
```
其效果与基础表格相比，仅是在tbody隔行有一个浅灰色的背景色。其实现原理也非常的简单，利用CSS3的结构性选择器“:nth-child”来实现，所以对于IE8以及其以下浏览器，没有背景条纹效果。