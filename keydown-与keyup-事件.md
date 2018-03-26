---
title: keydown()与keyup()事件
date: 2017-02-16 09:23:49
tags:
categories: [jQuery仓库]
---
键盘按下与松手，对应keydown与keyup方法来监听
<!--more-->
#### keydown事件：
当用户在一个元素上第一次按下键盘上字母键的时候，就会触发它。使用上非常简单，与基本事件参数处理保持一致，这里使用不在重复了，列出使用的方法
```js
//直接绑定事件
$elem.keydown( handler(eventObject) )
//传递参数
$elem.keydown( [eventData ], handler(eventObject) )
//手动触发已绑定的事件
$elem.keydown()
```
#### keyup事件：
当用户在一个元素上第一次松手键盘上的键的时候，就会触发它。使用方法与keydown是一致的只是触发的条件是方法的
代码：
```html
<div>监听keydown输入:
    <input class="target1" type="text" value="" /><br />
     按下显示输入的值:<em></em>
</div>
      
<div>监听keyup输入:
    <input class="target2" type="text" value="" /><br />
    松手显示输入的值:<em></em>
</div>
```
```js
//监听键盘按键
//获取输入的值
$('.target1').keydown(function(e) {
    $("em:first").text(e.target.value)
});

//监听键盘按键
//获取输入的值
$('.target2').keyup(function(e) {
    $("em:last").text(e.target.value)
});
```