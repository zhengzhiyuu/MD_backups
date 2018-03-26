---
title: CSS中栏流动布局(flex)
date: 2017-04-29 17:57:08
tags: [CSS]
categories: [前端,CSS]
---
这回用flex实现左右固定 , 中间流动的布局格式.
实现 圣杯布局 ....
<!--more-->
### 最基本的
` DOM结构为： ·
```html
<div class="container">
    <div id="left">left</div>
    <div id="main">main</div>
    <div id="right">right</div>
</div>
```

` CSS样式为: `
```css
.container{
    display: flex;
}
#main{
    flex: 1;
    height: 300px;            
    background: palevioletred
}
#left{
    flex: 0 0 300px;
    height: 300px;            
    background: palegreen;
}
#right{
    flex: 0 0 300px;
    height: 300px;
    background: palegoldenrod;
}
```

` 实现效果为: `
![此处输入图片的描述][1]

### 实现圣杯布局
` DOM结构为: `
```html
<div class="HolyGrail">
    <header class="HolyGrail_header">header</header>
    <div class="HolyGrail_body">
        <main class="HolyGrail_baoy_main">main</main>
        <nav class="HolyGrail_baoy_nav">nav</nav>
        <aside class="HolyGrail_baoy_aside">aside</aside>
    </div>
    <footer class="HolyGrail_footer">footer</footer>
</div>
```
` CSS样式为: `
```css
.HolyGrail {
    display: flex;
    min-height: 100vh;
    flex-direction: column;
}
.HolyGrail_header,
.HolyGrail_body,
.HolyGrail_footer {
    flex: 1;
}
.HolyGrail_body{
    display: flex;
}
.HolyGrail_baoy_main{
    background: palegoldenrod;
    flex: 1;
}
.HolyGrail_baoy_nav{
    flex: 0 0 12em;
    order: -1;
    background: pink;
}
.HolyGrail_baoy_aside{
    flex: 0 0 12em;
    background: palegreen;
}
.HolyGrail_header{
    background: palevioletred;
}
.HolyGrail_footer{
    background: powderblue;
}
 
 @media (max-width:760px){
    .HolyGrail_body{
        display: flex;
        flex-direction: column;
    }
    .HolyGrail_baoy_main,
    .HolyGrail_baoy_nav,
    .HolyGrail_baoy_aside{
        flex: auto;
    }
}
```
` 实现效果为: `
![此处输入图片的描述][2]


  [1]: http://chuantu.biz/t5/75/1493461666x2890173771.jpg
  [2]: http://chuantu.biz/t5/75/1493464754x2890174058.jpg