---
title: bootstrap排版
date: 2017-02-18 12:39:43
tags: bootstrap
categories: [前端,bootstrap]
---
<!--more-->
#### 副标题
```html
<h1>Hello，world <small> bootstrap之旅</small></h1>
```
#### 强调内容
```html
通过添加类名 .lead 实现
```
#### 文本加粗
```html
<b>和<strong>
```
#### 斜体和正常
```html
<em>和<cite>
```
#### 强调相关的类
- .text-muted：提示，使用浅灰色（#999）
- .text-primary：主要，使用蓝色（#428bca）
- .text-success：成功，使用浅绿色(#3c763d)
- .text-info：通知信息，使用浅蓝色（#31708f）
- .text-warning：警告，使用黄色（#8a6d3b）
- .text-danger：危险，使用褐色（#a94442）
#### 文本对齐风格
  ☑   .text-left：左对齐
  ☑   .text-center：居中对齐
  ☑   .text-right：右对齐
  ☑   .text-justify：两端对齐
#### 列表嵌套
```html
<ol>
    <li>有序列表</li>
    <li>
    有序列表
        <ol>
            <li>有序列表(2)</li>
            <li>有序列表(2)</li>
        </ol>
    </li>
    <li>有序列表</li>
</ol>
```
#### 列表--去点列表
```html
添加类名 .list-unstyled
```
#### 列表--内联列表
把垂直列表换成水平列表，而且去掉项目符号（编号），保持水平显示
```html
添加类名 .list-inline
```
#### 列表--定义列表
调整了行间距，外边距和字体加粗效果
```html
<dl>
    <dt>ANSON</dt><!--加粗-->
    <dd>anson</dd><!--正常-->
</dl>
```
#### 列表--水平定义列表
给定义列表实现水平显示效果
```html
<dl>添加类名 .dl-horizontal
```
#### 三种代码风格：
1、使用` <code></code> `来显示单行内联代码
2、使用` <pre></pre> `来显示多行块代码
3、使用` <kbd></kbd> `来显示用户输入代码
以` &lt; `开始，以` &gt; `结束
```html
<div>Bootstrap的代码风格有三种：
  <code>&lt;code&gt;</code>
  <code>&lt;pre&gt;</code>
  <code>&lt;kbd&gt;</code>
</div>
```
pre元素一般用于显示大块的代码，并保证原有格式不变。但有时候代码太多，而且不想让其占有太大的页面篇幅，就想控制代码块的大小。Bootstrap也考虑到这一点，你只需要在pre标签上添加类名“.pre-scrollable”，就可以控制代码块区域最大高度为340px，一旦超出这个高度，就会在Y轴出现滚动条。