---
title: trigger事件
date: 2017-02-16 11:24:26
tags:
categories: [jQuery仓库]
---
#### .trigger()
根据绑定到匹配元素的给定的事件类型执行所有的处理程序和行为
<!--more-->
在jQuery通过on方法绑定一个原生事件
```js
$('#elem').on('click', function() {
    alert("触发系统事件")
 });
 ```
 alert需要执行的条件：必须有用户点击才可以。如果不同用户交互是否能在某一时刻自动触发该事件呢？ 正常来说是不可以的，但是jQuery解决了这个问题，提供了一个trigger方法来触发浏览器事件
 所以我们可以这样：
 ```js
 $('#elem').trigger('click');
 ```
在绑定on的事件元素上，通过trigger方法就可以调用到alert
#### trigge支持自定义事件，并且自定义时间还支持传递参数
```js
$('#elem').on('Aaron', function(event,arg1,arg2) {
    alert("自触自定义时间")
 });
$('#elem').trigger('Aaron',['参数1','参数2'])
```