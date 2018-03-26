---
title: Angular2初试
date: 2017-02-13 10:22:55
tags: Angular2
categories: [前端,Angular2]
---
Angular2初试之利用angular-cli
<!--more-->
先说一说我在NPM angular-cli包时候遇到的小白问题
在NPM安装的时候出现了Python环境配置错误问题
解决办法：
下载Python2.7版本，在安装界面(windows)下如下配置，然后重启电脑即可
![此处输入图片的描述][1]
另外在 npm install 遇到其他Python问题可以参考[这篇文章][2]
#### 创建工程
Angular2为我们提供一个便捷的工程构建工具angular-cli，可以快速的搭建需要的开发环境
- 最新版的npm安装命令：
```js
$ npm install -g angular-cli@latest
```
旧版本的更新命令：
```js
$ npm uninstall -g angular-cli             //卸载
$ npm cache clean                         //清空缓存
$ npm install -g angular-cli@latest    //安装最新版本
```
创建工程文件命令：
```js
$ ng new project-name         //建立新项目
$ cd project-nam             //进入工程目录
```
本地端浏览：
```js
$ ng server || $ ng s
```
指定端口：
```
$ ng server --ng server --host 0.0.0.0 --port 4000
```
项目打包：
```js
$ ng build
```


  [1]: https://pic1.zhimg.com/9514fd3f7fd168670054ad99bd73f314_b.jpg
  [2]: https://my.oschina.net/homeemail/blog/335961