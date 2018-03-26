---
title: React初试
date: 2017-02-11 13:57:05
tags: React
categories: [前端,React]
---
前几天学习了React.js(我其实连jQuery还没有学好)，我就先随便写点，目前就会用React写出Hello，World！（大大的尴尬）
<!-- more -->
#### 1.1 CDN引用
React需要引入三个库:
react.min.js - React 的核心库
react-dom.min.js - 提供与 DOM 相关的功能
browser.min.js - 用于将 JSX 语法转为 JavaScript 语法

两个React库
```javascript
<script src="//cdn.bootcss.com/react/15.4.2/react.js"></script>
<script src="//cdn.bootcss.com/react/15.4.2/react-dom.js"></script>
```
和一个jsx语法解析库
```javascript
<script src="//cdn.bootcss.com/babel-core/6.1.19/browser.min.js"></script>
```
#### 1.2 Heool,world!
script部分代码，必须在script后面加上 type="text/babel"
下面是React版的Hello，World!
```javascript
ReactDOM.render(
        <h1>Hello, world!</h1>, 
        document.getElementById('example') 
        );
```
Html代码：
```js
<div id="example"></div>
```
### 以下内容摘抄自菜鸟教程，纯属凑字，我按照教程实验并没有起到任何作用，不知道哪里写的不对，希望有会得同学教一教我！
#### 1.3 通过NPM安装React
第一步、安装全局包
```js
$ npm install babel -g
$ npm install webpack -g
$ npm install webpack-dev-server --save-dev | npm install webpack -g
```
第二步、创建根目录
创建一个根目录，目录名为：reactApp，再使用 npm init 初始化，生成 package.json 文件：
```js
$ mkdir reactApp
$ cd reactApp/
$ npm init

name: (react) zhengzhiyuu
version: (1.0.0)
description: 测试
entry point: (index.js)
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to D:\react\package.json:

{
  "name": "zhengzhiyuu",
  "version": "1.0.0",
  "description": "测试",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this ok? (yes)
```
第三步、添加依赖包及插件
因为要使用 React, 所以需要先安装它，--save 命令用于将包添加至 package.json 文件。
```js
$ npm install react --save
$ npm install react-dom --save
```
同时我们也要安装一些 babel 插件
```js
$ npm install babel-core
$ npm install babel-loader
$ npm install babel-preset-react
$ npm install babel-preset-es2015
```
第四步、创建文件
```js
$ touch index.html
$ touch App.jsx
$ touch main.js
$ touch webpack.config.js
```
第五步、设置编译器，服务器，载入器
打开 webpack.config.js 文件添加以下代码:
```js
 var config = {
   entry: './main.js',
	
   output: {
      path:'./',
      filename: 'index.js',
   },
	
   devServer: {
      inline: true,
      port: 7777
   },
	
   module: {
      loaders: [ {
         test: /\.jsx?$/,
         exclude: /node_modules/,
         loader: 'babel',
			
         query: {
            presets: ['es2015', 'react']
         }
      }]
   }
	
}

module.exports = config;
```
- entry: 指定打包的入口文件 main.js。
- output：配置打包结果，path定义了输出的文件夹，filename则定义了打包结果文件的名称。
- devServer：设置服务器端口号为 7777，端口后你可以自己设定 。
module：定义了对模块的处理逻辑，这里可以用loaders定义了一系列的加载器，以及一些正则。当需要加载的文件匹配test的正则时，就会调用后面的loader对文件进行处理，这正是webpack强大的原因。

现在打开 package.json 文件，找到 "scripts" 中的 "test" , "echo \"Error: no test specified\" && exit 1" 使用以下代码替换：
```js
"start": "webpack-dev-server --hot"
```
现在我们可以使用 npm start 命令来启动服务。--hot 命令会在文件变化后重新载入，这样我们就不需要在代码修改后重新刷新浏览器就能看到变化。

第六步、index.html
设置 div id = "app" 为我们应用的根元素，并引入 index.js 脚本文件。
```js
<!DOCTYPE html>
<html>

   <head>
      <meta charset = "UTF-8">
      <title>React App</title>
   </head>

   <body>
      <div id = "app"></div>
      <script src = "index.js"></script>
   </body>

</html>
```
第七步、App.jsx 和 main.js
这是第一个 react 组件这个组件将输出 Hello World!。
App.jsx 文件代码:
```js
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            Hello World!<br />
         </div>
      );
   }
}

export default App;
```
需要引入组件并将其渲染到根元素 App 上，这样才可以在浏览器上看到它。
main.js 文件代码:
```js
import React from 'react';
import ReactDOM from 'react-dom';

import App from './App.jsx';

ReactDOM.render(<App />, document.getElementById('app'))
```
第八步、运行服务
完成以上配置后，即可运行该服务：
```js
$ npm start
```