---
title: CSS中栏流动布局(圣杯?)
date: 2017-04-29 10:00:22
tags: [CSS]
categories: [前端,CSS]
---
大概可能是圣杯布局吧 ? 不管了 , 反正是三栏中栏流动式布局 , 中间也没有被遮盖 !
<!--more-->
` DOM 结构为: `
```html
<div id="main">
    <div id="left">left</div>
    <div id="center">center</div>
    <div id="right">right</div>
</div>
```
` CSS样式为: `
```css
    * {
        margin: 0;
        padding: 0;
    }
    #main {
        position: relative;
        /*
            给左右两固定栏流出位置 
            解决遮盖中间流动层的被遮盖问题
        */
        padding-left: 300px;
        padding-right: 300px;
        /*
            如果想要固定main宽度 则需抛出左右两侧的宽度
            width:360px;
            实际宽度则是:(360+300+300)px
         */
    }

    #center {
        width: 100%;
        height: 500px;
        background: greenyellow;
    }

    #left {
        width: 300px;
        height: 500px;
        background: paleturquoise;
        position: absolute;
        top: 0;
        left: 0;
    }
    #right {
        width: 300px;
        height: 500px;
        background: pink;
        position: absolute;
        top: 0;
        right: 0;
    }
```
`实现效果为: `
![此处输入图片的描述][1]


  [1]: http://chuantu.biz/t5/75/1493432534x2890174088.jpg