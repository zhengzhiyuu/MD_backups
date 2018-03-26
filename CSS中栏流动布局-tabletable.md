---
title: CSS中栏流动布局(table)
date: 2017-04-29 16:18:12
tags: [CSS]
categories: [前端,CSS]
---
把要实现的display属性都设为 table-cell , 两侧固定宽度 , 中间的内容就会随着内容而撑开.
<!--more-->
` DOM结构为: `
```html
<nav>left</nav>
<active>
    main
    <p id="none">
        <!--占位用的...-->
        mainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmainmian
    </p>
</active>
<aside>right</aside>
```

` CSS样式为: `
```css
nav{
    display: table-cell;
    width: 300px;
    height: 500px;
    background: palegreen;
}
active{
    display: table-cell;
    height: 500px;
    word-break: break-all;
    background: palevioletred;
}
aside{
    display: table-cell;
    width: 300px;
    height: 500px;
    background: palegoldenrod;
}
/* 占位的... */
#none{
    visibility: hidden;
}
```

` 实现效果为: `
![此处输入图片的描述][1]


  [1]: http://chuantu.biz/t5/75/1493454812x2890174058.jpg