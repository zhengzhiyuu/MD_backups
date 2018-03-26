---
title: Vue自定义指令
date: 2017-06-30 12:00:00
tags: Vue
categories: [前端,Vue]
---
自定义过滤器和自定义指令一定要写在vue实例之前
<!--more-->
### 自定义过滤器
```js
Vue.filter('a', input => {
    return '$'+input;
})
```
```html
<li v-for="v in myData">{{v | a}}</li>
```
### 自定义指令：实现拖拽功能
```js
Vue.directive('drag', {
    inserted: function (el,binding) {
        el.style.position = 'absolute';
        el.style.left = `${binding.value.left}px`;
        el.style.top = `${binding.value.top}px`;
        el.onmousedown = function (ev) {
            let disX = ev.clientX - el.offsetLeft;
            let disY = ev.clientY - el.offsetTop;
            document.onmousemove = function (ev) {
                let left = ev.clientX - disX;
                let top = ev.clientY - disY;
                el.style.left = `${left}px`;
                el.style.top = `${top}px`;
            }
            document.onmouseup = function (ev) {
                document.onmousemove = null;
                document.onmouseup = null;
            }
        }
    }
})
```
```html
<div class="box" v-drag="{left:0,top:200}"></div>
<div class="box" v-drag="{left:500,top:200}"></div> 
```