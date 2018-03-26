---
title: Node框架Koa入门
date: 2017-05-28 15:41:36
tags: [Node.Js,Koa]
categories: [前端,Node.Js,Koa]
---
安装` koa：npm install koa `
<!--more-->
### 创建koa2工程文件app.js：
```js
//在Koa2中，Koa一个class，因此用大写的Koa表示:
const Koa = require('Koa');
//创建Koa对象,表示web app本身
const app = new Koa();

// 对于任何请求,app都将调用该异步函数处理请求:
app.use(async (ctx,next)=>{
    await next();
    // 设置response的Content-Type:
    ctx.response.type = 'text/html';
    // 设置response的内容:
    ctx.response.body = '<h1>Hello,koa2!</h1>';
})
// 在端口8080监听:
app.listen(8080);
console.log('app started at port 8080...');
``` 
### use参数:
- #### ctx :
是封装了` request `和` response `的变量，可以通过它访问` request `和 `response `
- #### next :
是koa传入的将要处理的下一个异步函数


上面的异步函数中，首先用` await next(); `处理下一个异步函数,然后，设置` response的Content-Type和内容 `
由` async `标记的函数称为异步函数,在异步函数中,可以用` await `调用另一个异步函数

### 注意:
` ctx `对象有一些简写的方法,例如` ctx.url `相当于` ctx.request.url `,` ctx.type `相当于` ctx.response.type `