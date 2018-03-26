---
title: Flex基本语法
date: 2017-04-29 20:32:35
tags: [CSS]
categories: [前端,CSS]
---
Flex是Flexible Box的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
<!--more-->
### 1. 指定Flex布局 
` 块级元素: `
```css
#content{
    display: flex;
}
```
` 行内元素: `
```css
 #content{
     display: flex;
 }
```
### 2. 基本属性
- ` flex-direction `

属性决定主轴的方向（即项目的排列方向）

flex-direction：row(左对齐) | row-reverse(右对齐) | column(顶对齐) | column-reverse(底对齐)

```css
.box {
  display:flex;
  flex-direction: row | row-reverse | column | column-reverse;
}
```
- ` flex-wrap `
  
如果一条轴线排不下，如何换行

flex-wrap: nowrap(不换行) | wrap(换行，第一行在上方) | wrap-reverse(换行，第一行在下方)

```css
.boxs{
    display: flex;
}
.box1{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```
- ` flex-flow `

是` flex-direction `属性和` flex-wrap `属性的简写形式，默认值为` row nowrap `
不写了...
[菜鸟教程 Flex][1]
[阮一峰 Flex语法基础][2]
[阮一峰 Flex布局实例][3]


  [1]: http://www.runoob.com/cssref/css-reference.html#flexbox
  [2]: http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool
  [3]: http://www.ruanyifeng.com/blog/2015/07/flex-examples.html