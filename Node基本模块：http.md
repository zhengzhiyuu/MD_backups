---
title: Node基本模块：http
date: 2017-05-28 11:46:15
tags: [Node.Js]
categories: [前端,Node.Js]
---
Node基本模块：http
<!--more-->
### 导入http模块:
```js
let http = require('http');
```
### 创建HTTP服务器： http.createServer()
- ` request `对象封装了HTTP请求，我们调用` request `对象的属性和方法就可以拿到所有HTTP请求的信息
- ` response `对象封装了HTTP响应，我们操作` response `对象的方法，就可以把HTTP响应返回给浏览器


```js
let http = require('http');

// 创建http server，并传入回调函数:
let server = http.createServer((request, response) => {
    // 回调函数接收request和response对象,
    // 获得HTTP请求的method和url:
    console.log(`${request.method} : ${request.url}`);
    // 将HTTP响应200写入response, 同时设置Content-Type: text/html:
    response.writeHead(200, {
        'Content-Type': 'text/html'
    });
    // 将HTTP响应的HTML内容写入response:
    response.end('<h1>Hello world!</h1>');
});

// 让服务器监听8080端口:
server.listen(8080);

console.log('Server is running at http://127.0.0.1:8080/');
```

### 创建文件服务器:
依赖模块: 
```js
 const fs = require('fs'),
     http = require('http'),
     url = require('url'),
     path = require('path');
```
#### 解析URl需要url模块,通过` url.parse() `解析为url对象:
```js
var url = require('url');

console.log(url.parse('http://user:pass@host.com:8080/path/to/file?query=string#hash'));
```
结果如下:
```js
Url {
  protocol: 'http:',
  slashes: true,
  auth: 'user:pass',
  host: 'host.com:8080',
  port: '8080',
  hostname: 'host.com',
  hash: '#hash',
  search: '?query=string',
  query: 'query=string',
  pathname: '/path/to/file',
  path: '/path/to/file?query=string',
  href: 'http://user:pass@host.com:8080/path/to/file?query=string#hash' }
```
#### 处理本地文件目录需要` path `模块,它可以方便地构造目录:
```js
let path = require('path');

// 解析当前目录:
let rootDir = path.resolve('.');
console.log(rootDir); // f:\Node

// 组合完整的文件路径:当前目录+'pub'+'index.html':
let filePath = path.join(rootDir, 'pub', 'index.html');
console.log(filePath); // f:\Node\pub\index.html'
```
#### 完整代码:
```js
 const fs = require('fs'),
     http = require('http'),
     url = require('url'),
     path = require('path');


 //获取root目录:
 let root = path.resolve('.');
 console.log('Static root dir: ' + root);

 //创建服务器:
 let server = http.createServer((request, response) => {
     // 获得URL的path
     let pathName = url.parse(request.url).pathname;
     // 获得对应的本地文件路径     
     let filePath = path.join(root, pathName);
     fs.stat(filePath, (err, stats) => {
         if (!err && stats.isFile()) {
             // 没有出错并且文件存在
             console.log(`200 ${request.url}`);
             // 发送200响应:
             response.writeHead(200);
             // 将文件流导向response:
             fs.createReadStream(filePath).pipe(response);
         } else {
             // 出错了或者文件不存在:response对象本身是一个Writable Stream
             console.log('404 ' + request.url);
             // 发送404响应:
             response.writeHead(404);
             response.end('404 Not Found');
         }
     })
 })

 server.listen(8080);
 console.log('Server is running at http://127.0.0.1:8080/');
```
运行文件 浏览器输入http://127.0.0.1:8080/pub/index.html

#### koa:
```js
const fs = require('fs');
const Koa = require('Koa');
const url = require('url');
const app = new Koa();

app.use(async(context, next) => {
    console.log(`${context.method}: ${context.url}`);
    let pathName = url.parse(context.request.url).pathname;
    let data = fs.readFileSync(__dirname + pathName, 'utf-8');
    context.response.body = data;
    await next();
})
app.use(router.routes());
```