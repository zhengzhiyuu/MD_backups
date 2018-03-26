---
title: HTML之localStorage
date: 2017-05-22 19:59:49
tags: [JavaScript]
categories: [前端,JavaScript]
---
直接给window.localStorage添加一个属性，例如：window.localStorage.name
<!--more-->
1. 赋值：
```js
localStorage.name = 'Anson';
```
2.取值:
```js
localStorage.getItem('name'); //Anson
```
3.设置setItem:
```js
localStorage.setItem('name','anson'); // 重新覆盖，变为了anson了
localStorage.setItem('age','20');
```
4.删除removeItem:
```js
localStorage.removeItem('name');
localStorage.getItem('name'); //null
```
5.全部清除clear:
```js
localStorage.clear(); // 清除了所有
localStorage.getItem('age'); //null
```