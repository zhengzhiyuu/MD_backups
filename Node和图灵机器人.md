---
title: Node和图灵机器人
date: 2017-06-01 22:48:28
tags: [Node.Js]
categories: [前端,Node.Js]
---
一点都不会，我要学习Node了
<!--more-->
### turing.js
```js
const http = require('http');

const getMessage = function (info, callback) {
    let key = '图灵官网key',
        url = 'http://www.tuling123.com/openapi/api?key=' + key + 'info=' + info,
        req = http.get(url, function (res) {
            let body = '';
            console.log("Got response: " + res.statusCode);
            res.on('data', function (data) {
                body += data;
            }).on('end', function () {
                console.log(res.headers);
                console.log(body);
                callback(JSON.parse(body)["text"]);
            });
        }).on('error', function (e) {
            console.log("Got error: " + e.message);
        });
    req.end();
}

module.exports.getMessage = getMessage;
```
### app.js
```js
const http = require('http'),
    url = require('url'),
    turing = require('./turing');

http.createServer((request, response) => {
    let msg = url.parse(request.url).pathname;
    turing.getMessage(msg, data => {
        var html = "<h1>" + data + "</h1>";
        response.writeHead(200, {
            "Content-Type": "text/html;charset=utf-8"
        });
        response.write(html);
        response.end();
    });
}).listen(8080);
```