---
title: Node模块概念
date: 2017-05-27 20:23:42
tags: [Node.Js]
categories: [前端,Node.Js]
---
### 输出模块:
```js
function hello(name) {
    console.log(`Hello,${name}!`);
}
module.exports = hello;
```
### 引入模块:
```js
const hello = require('./hello');
hello('Anson'); //Hello,Anson!
```
### 模块输出多个方法:
```js
//文件名为modules
function hello() {
    console.log(`Hello,${name}!`);
}

function seyHei(name) {
    console.log(`Hei,${name}!`);
}

module.exports = {
    hello: hello,
    seyHei: seyHei,
};
```
### 使用一个模块多个方法:
```js
const modules = require('./modules');
helloModule.hello('Anson');
helloModule.seyHei('Anson');
```