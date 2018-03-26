---
title: on()的高级用法
date: 2017-02-16 10:28:42
tags:
categories: [jQuery仓库]
---
#### on的另一个事件机制委托的机制
<!--more-->
#### 委托机制
```js
.on( events ,[ selector ] ,[ data ], handler(eventObject) )
```
在on的第二参数中提供了一个selector选择器，简单的来描述下
参考下面3层结构
```html
<div class="left">
    <p class="aaron">
        <a>目标节点</a> //点击在这个元素上
    </p>
</div>
```
给出如下代码：
```js
$("div").on("click","p",fn)
```
事件绑定在最上层div元素上，当用户触发在a元素上，事件将往上冒泡，一直会冒泡在div元素上。如果提供了第二参数，那么事件在往上冒泡的过程中遇到了选择器匹配的元素，将会触发事件回调函数
示例：
```html
<div class="left">
    <div class="aaron">
         <a>点击这里</a>
     </div>
</div>
```
```js
//给body绑定一个click事件
//没有直接a元素绑定点击事件
//通过委托机制，点击a元素的时候，事件触发
$('body').on('click', 'a', function(e) {
    alert(e.target.textContent)
})
```