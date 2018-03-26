---
title: typings的使用方法
date: 2017-05-27 20:43:07
tags: [工具]
categories: [前端,工具]
---
通过typings完成代码提示
<!--more-->
### npm安装typings
```npm
npm install -g typings
```
### 查看版本
```npm
typings --version
```
### 搜索是否有需要的类型文件
```npm
typings search exampleName
```
###  安装相关提示信息文件
```npm
typings install dt~node --global --save
typings install lodash --save
```
#### ` --global `参数的使用场景
- 如果安装的包使用` script `标记来引用(如jQuery)(也就是在浏览器中使用)
- 这个包是属于环境的一部分(如` node `)时
- 该包没有使用` --global `安装失败时


### 启用智能提示功能
方法一:
```js
/// <reference path="./typings/index.d.ts" />
```
方法二:
在根目录建立` jsconfig.json `文件:
基本格式如下:
```js
{
    "files": [
        "./typings/index.d.ts"
    ]
}
```