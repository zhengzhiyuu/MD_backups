---
title: Object.defineproperty
date: 2017-03-05 10:59:56
tags: JavaScript
categories: [前端,JavaScript]
---
直接在一个对象上定义一个新的属性，或修改一个已经存在的属性。这个方法会返回该对象。

### 语法
` Object.defineProperty(obj, prop, descriptor) `

### 参数
` Object obj ` 目标对象
` String prop ` 需要定义的属性
` Object descriptor ` 该属性拥有的特性，可设置的值有：
- value 属性的值，默认为 undefined。
- writable 该属性是否可写，如果设置成 false，则任何对该属性改写的操作都无效（但不会报错），默认为 false。
- get 一旦目标对象访问该属性，就会调用这个方法，并返回结果。默认为 undefined。
- set 一旦目标对象设置该属性，就会调用这个方法。默认为 undeinfed。
- configurable 如果为false，则任何尝试删除目标属性或修改属性以下特性（writable, configurable, enumerable）的行为将被无效化，默认为 false。
- enumerable 是否能在for...in循环中遍历出来或在Object.keys中列举出来。默认为 false。
#### 注意:

~ 在 descriptor 中不能同时设置访问器 (get 和 set) 和 wriable 或 value，否则会报错误