---
title: 停止动画stop
date: 2017-02-16 17:45:52
tags:
categories: [jQuery仓库]
---
动画在执行过程中是允许被暂停的，当一个元素调用.stop()方法，当前正在运行的动画（如果有的话）立即停止
<!--more-->
#### 语法：
```js
.stop( [clearQueue ], [ jumpToEnd ] )
.stop( [queue ], [ clearQueue ] ,[ jumpToEnd ] )
```
stop可选的参数:
- .stop(); 停止当前动画，点击在暂停处继续开始
- .stop(true); 如果同一元素调用多个动画方法，尚未被执行的动画被放置在元素的效果队列中。这些动画不会开始，直到第一个完成。当调用.stop()的时候，队列中的下一个动画立即开始。如果clearQueue参数提供true值,那么在队列中的动画其余被删除并永远不会运行
- .stop(true,true); 当前动画将停止，但该元素上的 CSS 属性会被立刻修改成动画的目标值
#### 参考下面代码:
```js
$("#anson").animate({
    height: 300
}, 5000)
$("#anson").animate({
    width: 300
}, 5000)
$("#anson").animate({
    opacity: 0.6
}, 2000)
```
stop()：只会停止第一个动画，第二个第三个继续
stop(true)：停止第一个、第二个和第三个动画
stop(true ture)：停止动画，直接跳到第一个动画的最终状态 
```js
//点击执行动画
$("#exec").click(function(){
    $("#anson").animate({
         height: 300
    }, 5000)
    $("#anson").animate({
         width: 300
    }, 5000)
    $("#anson").animate({
         opacity: 0.6
    }, 2000)
})


$("#stop").click(function() {
     var v = $("#animation").val();
     var $anson = $("#anson");
    if (v == "1") {
         //当前当前动画
           $anson.stop()
     } else if (v == "2") {
            //停止所以队列
         $anson.stop(true)
     } else if (v == "3") {
        //停止动画，直接跳到当前动画的结束
        $anson.stop(true,true)
    } 
});
```