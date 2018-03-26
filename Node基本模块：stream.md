---
title: Node基本模块：stream
date: 2017-05-28 10:56:32
tags: [Node.Js]
categories: [前端,Node.Js]
---
stream是Node.js提供的基本模块，目的是支持“流”这种数据结构。
<!--more-->
### 流读取数据: fs.createReadStream()
- ` data `事件表示流的数据已经可以读取了
- ` end `事件表示这个流已经到末尾了，没有数据可以读取
- ` error `事件表示出错了


样例：
```js
let fs = require('fs');
//打开一个流
let rs = fs.createReadStream('input.txt','utf-8');
rs.on('data',datas=>console.log(`DATA: ${datas}`));
rs.on('end',()=>console.log('END'));
rs.on('error',err=>console.log(`ERROR: ${err}`));
```
### 流写入数据: fs.createWriteStream
以流的形式写入文件，只需要不断调用` write() `方法，最后以` end() `结束
```js
let fs = require('fs');
let ws = fs.createWriteStream('output.txt', 'utf-8');
ws.write('使用Stream写入文本数据...\n');
ws.write('END');
ws.end();
```
### pipe: readable.pipe(writable)
所有的数据自动从` Readable `流进入` Writable `流，这种操作叫` pipe `,也就是复制文件
```js
let fs = require('fs');
let rs = fs.createReadStream('input.png');
let ws = fs.createWriteStream('output.png');
rs.pipe(ws);
```
默认情况下，当` Readable `流的数据读取完毕,` end `事件触发后，将自动关闭` Writable `流。如果我们不希望自动关闭` Writable `流，需要传入参数：
```js
readable.pipe(writable, { end: false });
```
#### 也可以这样?
```js
let fs = require('fs');
let rs = fs.createReadStream('input.png');
let ws = fs.createWriteStream('output.png');
rs.on('data', data => {
    ws.write(data);
    ws.end();
});
rs.on('end', () => console.log('END'));
rs.on('error', err => console(`ERROR: ${err}`));
```