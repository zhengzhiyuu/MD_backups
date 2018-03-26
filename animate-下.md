---
title: animate(下)
date: 2017-02-16 17:36:50
tags:
categories: [jQuery仓库]
---
animate在执行动画中，如果需要观察动画的一些执行情况，或者在动画进行中的某一时刻进行一些其他处理，我们可以通过animate提供的第二种设置语法，传递一个对象参数，可以拿到动画执行状态一些通知
<!--more-->
```js
.animate( properties, options )
```
#### options参数
- duration - 设置动画执行的时间
- easing - 规定要使用的 easing 函数，过渡使用哪种缓动函数
- step：规定每个动画的每一步完成之后要执行的函数
- progress：每一次动画调用的时候会执行这个回调，就是一个进度的概念
- complete：动画完成回调
其中最关键的一点就是：
` 如果多个元素执行动画，回调将在每个匹配的元素上执行一次，不是作为整个动画执行一次 `
列出常用的方式
```js
$('#elem').animate({
    width: 'toggle',  
    height: 'toggle'
  }, {
    duration: 5000,
    specialEasing: {
    width: 'linear',
    height: 'easeOutBounce'
},
 complete: function() {
     $(this).after('<div>Animation complete.</div>');
}
});
```
```js
$ele.animate({
    height: '50'
  }, {
    duration :2000,
    //每一个动画都会调用
    step: function(now) {
        $aaron.text('高度的改变值:'+now)
    }
})