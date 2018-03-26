---
title: .ssh设置
date: 2017-02-17 18:31:52
tags: 工具
categories: [工具]
---
运行环境deepin
- 检查电脑是否有ssh key 存在
```js
ls -a .ssh
```
- 如果没有则
```js
ssh-keygen -t rsa -C "your emlie"
```
其他回车即可
然后
```js
cd .ssh
```
```js
dir
```
```js
vi id_rsa.pub
```