---
title: animate
date: 2017-02-16 17:18:21
tags:
categories: [jQuery仓库]
---
复杂的动画通过之前几个动画函数是不能够实现，这时候就需要强大的animate方法了
<!--more-->
操作一个元素执行3秒的淡入动画，对比一下2组动画设置的区别
```js
$(elem).fadeOut(3000)  

$(elem).animate({   
    opacity:0
},3000)
```
#### 语法：
```js
.animate( properties ,[ duration ], [ easing ], [ complete ] )
.animate( properties, options )
```
.animate()方法允许我们在任意的数值的CSS属性上创建动画。2种语法使用，几乎差不多了，唯一必要的属性就是一组CSS属性键值对。这组属性和用于设置.css()方法的属性键值对类似，除了属性范围做了更多限制。第二个参数开始可以单独传递多个实参也可以合并成一个对象传递了
#### 参数分解：
properties：一个或多个css属性的键值对所构成的Object对象。要特别注意所有用于动画的属性` 必须是数字的 `，除非另有说明；这些属性如果不是数字的将不能使用基本的jQuery功能。比如常见的，border、margin、padding、width、height、font、left、top、right、bottom、wordSpacing等等这些都是能产生动画效果的。background-color很明显不可以，因为参数是red或者GBG这样的值，非常用插件，否则正常情况下是不能只用动画效果的。注意，CSS 样式使用 DOM 名称（比如 "fontSize"）来设置，而非 CSS 名称（比如 "font-size"）。
` 特别注意单位 `，属性值的单位像素（px）,除非另有说明。单位em 和 %需要指定使用
```js
.animate({
    left: 50, 
    width: '50px'   
    opacity: 'show',  
    fontSize: "10em",
}, 500);
```
除了定义数值，每个属性能使用'show', 'hide', 和 'toggle'。这些快捷方式允许定制隐藏和显示动画用来控制元素的显示或隐藏
```js
.animate({
    width: "toggle"
});
```
如果提供一个` 以+= 或 -=开始 `的值，那么目标值就是以这个属性的当前值加上或者减去给定的数字来计算的
```js
.animate({ 
    left: '+=50px'
}, "slow");
```
#### duration时间
动画执行的时间，持续时间是以毫秒为单位的；值越大表示动画执行的越慢，不是越快。还可以提供'fast' 和 'slow'字符串，分别表示持续时间为200 和 600毫秒。
#### easing动画运动的算法
jQuery库中默认调用 swing。如果需要其他的动画算法，请查找相关的插件
#### complete回调
动画完成时执行的函数，这个可以保证当前动画确定完成后发会触发
示例：
```css
<style>
p {
    color: red;
}
div{
    width:200px; 
    height: 100px; 
    background-color: yellow;
    color:red;
}
</style>
```
```html
<div id="aaron">内部动画</div>
    点击观察动画效果：
    <select id="animation">
        <option value="1">动画1</option>
        <option value="2">动画2</option>
        <option value="3">动画3</option>
        <option value="4">动画4</option>
    </select>
<input id="exec" type="button" value="执行动画">
```
```js
$("#exec").click(function() {
    var v = $("#animation").val();
    var $aaron = $("#aaron");
    if (v == "1") {
         // 数值的单位默认是px
         $aaron.animate({
             width  :300,
             height :300
         });
    } else if (v == "2") {
         // 在现有高度的基础上增加100px
        $aaron.animate({
             width  : "+=100px",
               height : "+=100px"
         });
    } else if (v == "3") {
        $aaron.animate({
              fontSize: "5em"
         }, 2000, function() {
              alert("动画 fontSize执行完毕!");
        });
    } else if (v == "4") {
         //通过toggle参数切换高度
        $aaron.animate({
              width: "toggle"
         });
    } 
});
```