---
title: keypress()事件
date: 2017-02-16 09:43:23
tags:
categories: [jQuery仓库]
---
#### 在input元素上绑定keydown事件会发现一个问题：
每次获取的内容都是之前输入的，当前输入的获取不到
<!--more-->
#### keypress事件与keydown和keyup的主要区别
- 只能捕获单个字符，不能捕获组合键
- 无法响应系统功能键（如delete，backspace）
- 不区分小键盘和主键盘的数字字符
#### 总而言之，
KeyPress主要用来接收字母、数字等ANSI字符，而 KeyDown 和 KeyUP 事件过程可以处理任何不被 KeyPress 识别的击键。诸如：功能键（F1-F12）、编辑键、定位键以及任何这些键和键盘换档键的组合等。
用法：
```js
//直接绑定事件
$elem.keypress( handler(eventObject) )
//传递参数
$elem.keypress( [eventData ], handler(eventObject) )
//手动触发已绑定的事件
$elem.keypress()
代码：
```
```html
<div class="left">
    <div class="aaron">监听keypress输入:
        <input class="target1" type="text" value="" /><br />
         输入中文测试，无法显示:<em></em>
    </div>
</div>
```
```js
//监听键盘按键
//获取输入的值
$('.target1').keypress(function(e) {
     $("em").text(e.target.value)
});
```