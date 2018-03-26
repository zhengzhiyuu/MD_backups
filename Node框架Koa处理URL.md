---
title: Node框架Koa处理URL
date: 2017-05-28 16:55:48
tags: [Node.Js,Koa]
categories: [前端,Node.Js,Koa]
---
引入koa-router这个中间件,让它负责处理URL映射
<!--more-->
### 安装koa-router:
```js
npm i koa-router
```
### 处理GET请求:
使用` router.get('/path', async fn) `来注册一个` GET请求 `。可以在请求路径中使用` 带变量的/hello/:name `，变量可以通过` ctx.params.name `访问。
```js
const Koa = require('Koa');
//函数调用 koa-router() :
const router = require('Koa-router')();
const app = new Koa();

app.use(async(ctx, next) => {
    console.log(`method: ${ctx.method}; url: ${ctx.request.url}`);
    await next();
})
//注册koa-router中间件
app.use(router.routes());

router.get('/', async(ctx, name) => {
    ctx.response.body = '<h1>Index</h1>';
})
router.get('/hello/:name', async(ctx, next) => {
    let name = ctx.params.name;
    ctx.response.body = `<h1>Hello,${name}</h1>`;
})

app.listen(8080);
console.log('app started at port 8080...');
```
### 处理POST请求:
使用` router.post('/path', async fn) `来注册一个` POST请求 `。
#### 坑：
用post请求处理URL时，会遇到一个问题：post请求通常会发送一个表单，或者JSON，它作为request的body发送，但无论是Node.js提供的原始request对象，还是koa提供的request对象，都不提供解析request的body的功能！
#### 解决办法：
引入` koa-bodyparser `中间件:
```js
npm i koa-bodyparser
```
由于中间件的顺序很重要，这个` koa-bodyparser `必须在` router `之前被注册到` app `对象上。
```js
const bodyParser = require('koa-bodyparser');
app.use(bodyParser());
```
#### post示例：
```js
const Koa = require('Koa');
const router = require('Koa-router')();
const bodyParser = require('koa-bodyparser');
const app = new Koa();

app.use(async(ctx, next) => {
    console.log(`method: ${ctx.method}; url: ${ctx.request.url}`);
    await next();
})
//注册koa-bodyparser中间件
app.use(bodyParser());
//注册koa-router中间件
app.use(router.routes());

router.get('/', async(ctx, name) => {
    ctx.response.body = `<h1>Index</h1>
        <form action="/signin" method="post">
            <p>Name: <input name="name" value="koa"></p>
            <p>Password: <input name="password" type="password"></p>
            <p><input type="submit" value="Submit"></p>
        </form>`;
})
router.post('/signin', async(ctx, next) => {
    let name = ctx.request.body.name || '',
        password = ctx.request.body.password || '';
    console.log(`name: ${name} ; password: ${password}`);

    if (name === 'koa' && password === '12345') {
        ctx.response.body = `<h1>Welcome, ${name}!</h1>`;
    } else {
        ctx.response.body = `<h1>Login failed!</h1>
        <p><a href="/">Try again</a></p>`;
    }
})

app.listen(8080);
console.log('app started at port 8080...');
```
通过` let name = ctx.request.body.name `拿到表单的` name `字段。
类似的，put、delete、head请求也可以由router处理。

### 重构:
把URL处理函数集中到某个js文件，或者某几个js文件中就好了，然后让app.js自动导入所有处理URL的函数
```js
koa工程项目/
|
+- .vscode/
|  |
|  +- launch.json <-- VSCode 配置文件
|
+- controllers/
|  |
|  +- login.js <-- 处理login相关URL
|  |
|  +- users.js <-- 处理用户管理相关URL
|
+- app.js <-- 使用koa的js
|
+- controller.js <-- 自定义中间件
|
+- package.json <-- 项目描述文件
|
+- node_modules/ <-- npm安装的所有依赖包
```
#### app.js主文件
```js
const Koa = require('Koa');
const bodyParser = require('koa-bodyparser');
const controller = require('./controller');
const app = new Koa();

app.use(async(ctx, next) => {
    console.log(`method: ${ctx.method}; url: ${ctx.request.url}`);
    await next();
})
//注册koa-bodyparser中间件
app.use(bodyParser());
//注册controller中间件
app.use(controller());

app.listen(8080);
console.log('app started at port 8080...');
```
#### 在controllers目录下编写login.js：
```js
let fn_index = async(ctx, name) => {
    ctx.response.body = `<h1>Index</h1>
        <form action="/signin" method="post">
            <p>Name: <input name="name" value="koa"></p>
            <p>Password: <input name="password" type="password"></p>
            <p><input type="submit" value="Submit"></p>
        </form>`;
};

let fn_signin = async(ctx, next) => {
    let name = ctx.request.body.name || '',
        password = ctx.request.body.password || '';
    console.log(`name: ${name} ; password: ${password}`);

    if (name === 'koa' && password === '12345') {
        ctx.response.body = `<h1>Welcome, ${name}!</h1>`;
    } else {
        ctx.response.body = `<h1>Login failed!</h1>
        <p><a href="/">Try again</a></p>`;
    }
};
//module.exports把两个URL处理函数暴露出来
module.exports = {
    'GET /': fn_index,
    'POST /signin': fn_signin
};
```
#### 在controllers目录下编写users.js：
```js
let fn_hello = async(ctx, next) => {
    let name = ctx.params.name;
    ctx.response.body = `<h1>Hello,${name}</h1>`;
};
module.exports = {
    'GET /hello/:name': fn_hello
};
```
#### 在根目录下编写controller.js：
```js
const fs = require('fs');

function addMapping(router, mapping) {
    for (let url in mapping) {
        if (url.startsWith('GET ')) {
            let path = url.substring(4);
            router.get(path, mapping[url]);
            console.log(`register URL mapping: GET ${path}`);
        } else if (url.startsWith('POST ')) {
            let path = url.substring(5);
            router.post(path, mapping[url]);
            console.log(`register URL mapping: POST ${path}`);
        } else if (url.startsWith('PUT ')) {
            let path = url.substring(4);
            router.put(path, mapping[url]);
            console.log(`register URL mapping: PUT ${path}`);
        } else if (url.startsWith('DELETE ')) {
            let path = url.substring(7);
            router.del(path, mapping[url]);
            console.log(`register URL mapping: DELETE ${path}`);
        } else {
            console.log(`invalid URL: ${url}`);
        }
    }
}

function addControllers(router, dir) {
    fs.readdirSync(__dirname + '/' + dir).filter((f) => {
        return f.endsWith('.js');
    }).forEach((f) => {
        console.log(`process controller: ${f}...`);
        let mapping = require(__dirname + '/' + dir + '/' + f);
        addMapping(router, mapping);
    });
}

module.exports = (dir) => {
    let controllers_dir = dir || 'controllers',
        router = require('koa-router')();
    addControllers(router, controllers_dir);
    return router.routes();
};
```