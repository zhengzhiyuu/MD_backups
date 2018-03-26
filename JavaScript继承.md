---
title: JavaScript之继承
date: 2017-04-02 17:09:11
tags: [JavaScript,面向对象]
categories: [前端,JavaScript,面向对象]
---
继承我是理解不透了,照葫芦画瓢吧!
我觉得ES6的最简单最好用,一点不要费脑子 =-=
<!--more-->
### ES6继承：
```js
        class Person {
            constructor(name) {
                this.name = name;
            }
            getName() {
                return this.name;
            }
        }
        class Baby extends Person {
            constructor(name, age) {
                super(name); 
                //super 调用父类的constructor(name)
                this.age = age;
            }
            getAge() {
                return this.age;
            }
        }
        const baby = new Baby("baby", "1");
        console.log(baby.constructor == Person); //false
        console.log(baby.constructor == Baby); //true
        console.log(baby.__proto__); //Object
        console.log(baby.getName()); //baby
        console.log(baby.getAge()); //1
```
### 借用构造函数:
```js
        function SuperType(name) {
            this.name = name;
        }

        function SubType(name, age) {
            SuperType.apply(this, [name]);
            this.age = age;
        }

        const subType = new SubType("anson", 20);
        console.log(subType.name);//anson
        console.log(subType.age); //20
```
### 基于原型链的继承的写法：
```js
        function Person(name, age) {
            this.name = name;
            this.age = age;
        }
       
        Person.prototype.getName = function () {
            return this.name;
        }

        *******Baby继承于Person*********

        function Baby(name, age) {
            Person.apply(this, [name, age]);
            // Person.call(this,name,age;)
        }
        // Baby.prototype = new Person();
        // Baby.prototype.constructor = Baby;

        Baby.prototype=Object.create(Person.prototype)

        const baby = new Baby("baby", "1");
        console.log(baby.getName()); //baby
```
#### 注意：
需要注意的是，如果在子类的prototype对象上也有getName方法，就会覆盖父类的，因为查找时在自己上面就找到了，就不会向上回溯了
##### 问题：
- 1.没有实现传统oo该有的super方法来调用父类方法
- 2.直接将父类实例作为子类的原型，简单粗暴造成多余的原型属性
```js
Baby.prototype=Object.create(Person.prototype)
        console.log(baby._proto_); //undefined
```
- 3.construct的问题
```js
console.log(baby.constructor == Person) //true
console.log(baby.constructor == Baby) //false
```
### 对基于原型链的继承的写法进行改良：
```js
        function Person(name, age) {
            this.name = name;
            this.age = age;
        }

        Person.prototype.getName = function () {
            return this.name;
        }

        function Baby(name, age) {
            Person.apply(this, [name, age]);
            // Person.call(this,name,age;)
        }
        let Func = function () {};
        Func.prototype = Person.prototype;
        Baby.prototype = new Func();
        Baby.prototype.constructor = Baby;

        const baby = new Baby("baby", "1");
        console.log(baby.constructor == Person); //false
        console.log(baby.constructor == Baby); //true
        console.log(baby.__proto__); //Object
        console.log(baby.getName()); //baby
```
将其进行封装：
```js
        let Func = function () {};
        Func.prototype = Person.prototype;
        Baby.prototype = new Func();
        Baby.prototype.constructor = Baby;
```
封装为：
```js
        function objectCreate(prototype) {
            let Func = function () {};
            Func.prototype = prototype;
            return new Func();
        }

        function inherit(subclass, parentclass) {
            subclass.prototype = objectCreate(parentclass.prototype);
            subclass.prototype.constructor = subclass;
        }
```
于是继承可以写成：
```js
        function Person(name, age) {
            this.name = name;
            this.age = age;
        }

        Person.prototype.getName = function () {
            return this.name;
        }

        function objectCreate(prototype) {
            let Func = function () {};
            Func.prototype = prototype;
            return new Func();
        }

        function inherit(subclass, parentclass) {
            subclass.prototype = objectCreate(parentclass.prototype);
            subclass.prototype.constructor = subclass;
        }

        function Baby(name, age) {
            Person.apply(this, [name, age]);
            // Person.call(this,name,age;)
        }
        inherit(Baby,Person);

        const baby = new Baby("baby", "1");
        console.log(baby.constructor == Person); //false
        console.log(baby.constructor == Baby); //true
        console.log(baby.__proto__); //Object
        console.log(baby.getName()); //baby
```
