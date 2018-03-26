---
title: JSON的常用方法
date: 2017-04-15 17:51:57
tags: JavaScript
categories: [前端,JavaScript]
---
JSON是一种数据交换格式
<!--more-->
#### 序列化
把对象转换为JSON格式:
```js
const MyObj = {
    name: 'anson',
    age: 20
}
JSON.stringify(MyObj);
//"{"name":"anson","age":20}"
```
#### 格式换行:
```js
const MyObj = {
    name: 'anson',
    age: 20
}
JSON.stringify(MyObj,null,' ');
/*
   "{
    "name":"anson",
    "age":20
    }"
*/
```
#### 第二个参数:
##### 筛选对象键值
```js
JSON.stringify(MyObj,["name"],' ');
/*
    {
    "name":"anson"
    }
*/
```
##### 传入函数对每个键值进行处理
```js
function convert(key,value) {
    if(typeof value == 'string') {
        return value.toUpperCase();
    }
    return value;
}
JSON.stringify(MyObj,convert,' ');
/*
   {
     "name": "ANSON",
     "age": 20
   }
*/
```
#### 精确控制序列化:
` 似乎方法名称必须是toJSON `
```js
const MyObj = {
    name: 'anson',
    age: 20,
    toJSON() {
        return {
            name: this.name
        };
    }
 }
JSON.stringify(MyObj);
//{"name":"anson"} 
```
#### 反序列化:
把JSON转换为对象
```js
const MyObj = {
    name: 'anson',
    age: 20
 }
const MyJson = JSON.stringify(MyObj);
JSON.parse(MyJson)
//Object {name: "anson", age: 2}
```