---
title: bootstrap基础表格
date: 2017-02-18 14:23:00
tags:
categories: [bootstrap仓库]
---
#### 基础表格
在Bootstrap中，对于基础表格是通过类名“.table”来控制。如果在` <table> `元素中不添加任何类名，表格是无任何样式效果的。想得到基础表格，我们只需要在` <table> `元素上添加“.table”类名，就可以得到Bootstrap的基础表格：
<!--more-->
```html
<table class="table">
…
</table>
```
表格的结构
```html
<table>
<thead>
<tr>
<th>表格标题</th>
…
</tr>
</thead>
<tbody>
<tr>
<td>表格单元格</td>
…
</tr>
     …
</tbody>
</table>
```
示例：
```html
<table class="table">
   <thead>
     <tr>
       <th>表格标题</th>
       <th>表格标题</th>
       <th>表格标题</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
   </tbody>
</table>
```