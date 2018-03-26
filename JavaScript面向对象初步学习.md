---
title: JavaScript面向对象初步学习
date: 2017-02-11 19:06:24
tags: JavaScript
categories: [前端,JavaScript]
---
面向对象三大基本特性：封装，继承，多态
<!-- more -->
```js
var dog = {
    name: "Pancake",
    legs: 4,
    isAwesome: true
}

//给对象添加方法
dog.back = function () {
    console.log("My name is " + this.name + "!")
}
dog.back() //My name is Pancake!
/*  
 **  给dog对象添加名为back属性 并给它分配了一个函数
 **  该函数使用了this.name 这会访问对象的name属性中存储的值
 **/

//在多个对象之间共享方法
//1.先创建一个函数
function speak() {
    console.log(this.sound + " My name is " + this.name + "!")
}
//2.创建多个对象
var cat = {
    sound: "Miaow",
    name: "Mittens",
    speak: speak
}
var pig = {
    sound: "Oink",
    name: "Charlie",
    speak: speak
}

//3.调用speak方法
cat.speak() //Miaow My name is Mittens!
pig.speak() //Oink My name is Charlie!


//构造方法函数
function Car(x, y) {
    this.x = x //构造方法Car接受参数 x,y 
    this.y = x //添加属性 this.x this.y
}
//调用Car构造方法
var tesla = new Car(10, 20)
tesla //Car {x: 10, y: 10}
```