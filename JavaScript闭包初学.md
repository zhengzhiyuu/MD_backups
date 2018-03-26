---
title: JavaScript闭包初识
date: 2017-04-02 15:09:11
tags: [闭包,JavaScript]
categories: [前端,JavaScript]
---
稀碎啊稀碎!
　　模块的一般形式是：一个定义了“私有变量”和函数的函数，利用闭包的特性(即创建了可以访问“私有变量和函数”的特权函数)，最后将这些特权函数返回或保存到一个可以访问的地方。
<!--more-->
IIFE立即调用
```js
let person = (function () {
            let age = 21;
            return {
                name: "Anson",
                getAge: function () {
                    return age;
                },
                growOlder: function () {
                    age++;
                }
            };
        }());
        console.log(person.name); //Anson
        console.log(person.getAge()); //21
        person.age = 100;
        console.log(person.getAge()); //21
        person.growOlder();
        console.log(person.getAge()); //22
```
使用模块模式创建person对象,变量age是给对象的私有属性,它无法被外界直接访问,但可以通过对象方法来访问，该对象有两个特权方法getAge()和goewOlder()
模块模式的变种暴露模式：
```js
let person = (function () {
            let age = 21;

            function getAge() {
                return age;
            }

            function gorwOlder() {
                age++;
            }
            return {
                name: "Anson",
                getAge: getAge,
                gorwOlder: gorwOlder
            };
        }());
```
它将所有变量和方法都组织在IIFE的顶部，然后将它们设置到需要被返回的对象上
它可以保障所有的变量和函数声明都在一处


理解下面的结果：
```js
var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　return function(){
　　　　　　　　return this.name;
　　　　　　};
　　　　}
　　};
　　alert(object.getNameFunc()());
```
```js
var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　var that = this;
　　　　　　return function(){
　　　　　　　　return that.name;
　　　　　　};
　　　　}
　　};
　　alert(object.getNameFunc()());
```