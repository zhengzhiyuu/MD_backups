---
title: JavaScript数组排序
date: 2017-03-04 18:15:10
tags: JavaScript
categories: [前端,JavaScript]
---
sort()方法
ES6的写法:` Array.sort((x, y) => x > y ? 1 : -1) `
之前实在是太low...
<!--more-->
先创建比较函数
```js
//从小到大
function compare(value1, value2) {
    if (value1 < value2) {
        return -1;
    } else if (value1 > value2) {
        return 1;
    } else {
        return 0;
    }
}
let value = [1,5,2,15,11,8];
let a = value.sort(compare);
console.log(a);//[1, 2, 5, 8, 11, 15]
```
反之
```js
function compare(value1,value2) {
    if(value1 < value2) {
        return 1;
    }else if(value1 > value2) {
        return -1;
    }else {
        return 0;
    }
}
```