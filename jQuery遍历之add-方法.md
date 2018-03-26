---
title: jQuery遍历之add()方法
date: 2017-02-15 14:12:55
tags:
categories: [jQuery仓库]
---
.add()的参数可以几乎接受任何的$()，包括一个jQuery选择器表达式，DOM元素，或HTML片段引用。
<!--more-->
### 案例：
操作：选择所有的li元素，之后把p元素也加入到li的合集中
```html
<ul>
    <li>list item 1</li>
    <li>list item 2</li>    
    <li>list item 3</li>
</ul>
<p>p元素</p>
```
处理一：传递选择器
```js
$('li').add('p')
```
处理二：传递dom元素
```js
$('li').add(document.getElementsByTagName('p')[0])
```
还有一种方式，就是动态创建P标签加入到合集，然后插入到指定的位置，但是这样就改变元素的本身的排列了
```js
 $('li').add('<p>新的p元素</p>').appendTo(目标位置)
 ```