---
title: Node基本模块：fs
date: 2017-05-27 21:10:47
tags: [Node.Js]
categories: [前端,Node.Js]
---
Node基本模块：fs
<!--more-->
### 引入fs模块：
```js
const fs = require("fs");
```
### 读取文件: fs.readFile()
```js
fs.readFile('input.txt', 'utf-8', (err, data) => {
    if (err) {
        return console.log(err);
    }else{
        console.log(data.toString());
    }
})
```
### 写入文件: fs.writeFile()
```js
let data = 'My name is zhiyu!'
fs.writeFile('input.txt', data, err => {
    if (err) {
        console.log(err);
    } else {
        console.log('ok');
    }
});
```
### stat
- isFile() 是否是文件
- isDirectory() 是否是目录
- size 文件大小
- birthtime 创建时间
- mtime 修改时间


```js
fs.stat('input.txt', (err, stat) => {
    if (err) {
        console.log(err);
    } else {
        // 是否是文件:
        console.log(`isFile: ${stat.isFile()}`);
        // 是否是目录:
        console.log(`isDirectory: ${stat.isDirectory()}`);
        if (stat.isFile()) {
            // 文件大小:
            console.log(`size: ${stat.size}`);
            // 创建时间, Date对象:
            console.log(`birth time: ${stat.birthtime}`);
            // 修改时间, Date对象:
            console.log(`modified time: ${stat.mtime}`);
        }
    }
})
```