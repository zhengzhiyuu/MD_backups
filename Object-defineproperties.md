---
title: Object.defineproperties
date: 2017-03-05 11:00:20
tags: JavaScript
categories: [前端,JavaScript]
---
和` Object.defineProperty `类似，只不过这个方法可以设置多个属性。
继承defineproperty的参数

### 语法
` Object.defineProperties(obj, props,descriptor) `

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
```js
//用面向字面量的方式创建一个book对象
var book={};
//调用Object.defineProperties(对象名，要添加的属性)方法，为对象一次定义多个属性(1.数据属性)(2.访问器属性)
Object.defineProperties(book,{
//添加的两个数据属性(_year,edition)
_year:{//(_year)前面的下划线表示只能通过对象方法访问的属性
value:2004
},
edition:{
value:1
},
//添加了访问器属性(year)
year:{
//调用get方法读取属性
get:function(){
return this._year;
},
//调用set方法写入属性
set:function(newValue){
if (newValue>2004) {
this._year=newValue;
this.edition+=newValue-2004;
}
}
}
});
//测试
book.year=2005;//访问器属性常见方式，设置一个属性的值会导致其他属性发生变化
alert(book.edition);
```