---
title: 显示与隐藏切换toggle方法
date: 2017-02-16 13:45:33
tags:
categories: [jQuery仓库]
---
toggle用于切换显示或隐藏匹配元素
<!--more-->
#### 基本的操作：.toggle()
- 如果元素是最初显示，它会被隐藏
- 如果隐藏的，它会显示出来
#### 提供参数：.toggle( [duration ] [complete ] )
#### 直接定位：.toggle(display)
直接提供一个参数，指定要改变的元素的最终效果
其实就是确定是使用show还是hide方法
```js
if ( display === true ) {
  $( "elem" ).show();
} else if ( display === false ) {
  $( "elem" ).hide();
}
```
代码：
```js
$("div").toggle(3000)
//3000毫秒后隐藏
```