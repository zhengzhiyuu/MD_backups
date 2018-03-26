---
title: jQuery中的data()方法
date: 2017-02-12 18:28:13
tags:
categories: [jQuery仓库]
---
#### 定义和用法
data() 方法向被选元素附加数据，或者从被选元素获取数据。
<!--more-->
#### 向元素附加数据
向被选元素附加数据
#### 语法
```js
$(selector).data(name,value)
```
参数	  描述
name :	必需;规定要设置的数据的名称
value :	必需;规定要设置的数据的值

#### 从元素返回数据
从被选元素中返回附加的数据
#### 语法
```js
$(selector).data(name)
```
参数	  描述
name ： 可选。规定要取回的数据的名称
如果没有规定名称，则该方法将以对象的形式从元素中返回所有存储的数据

学习代码：
```js
<script>
        $(document).ready(function () {
            /* 
            ** 向p元素添加数据 a
            */
            $("#btn1").click(function () {
                $("p").data("a", "Hello! </br>");
            })
            /*
            ** 把p元素数据a取出，添加到div标签
            */
            $("#btn2").click(function () {
                var a = $("p").data("a");
                $("div").append(a);
            })
        })
</script>
```
```html
<body>
    <button id="btn1">赋值</button>
    <button id="btn2">取值</button>
    <p></p>
    <div></div>
</body>
```
#### 使用对象向元素附加数据
使用带有名称/值对的对象向被选元素添加数据。
#### 语法
```js
$(selector).data(object)
```
参数	    描述
object :  必需;规定包含名称/值对的对象

学习代码：
```js
<script type="text/javascript">
$(document).ready(function(){
  testObj=new Object();
  testObj.greetingMorn="Good Morning!";
  testObj.greetingEve="Good Evening!";
  $("#btn1").click(function(){
    $("div").data(testObj);
  });
  $("#btn2").click(function(){
    alert($("div").data("greetingEve"));
  }); // Good Evening!
});
</script>
```