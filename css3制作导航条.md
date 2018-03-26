---
title: css3制作导航条
date: 2017-03-09 16:44:42
tags: [CSS]
categories: [前端,CSS]
---
<!--more-->
```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>CSS制作立体导航</title>
    <style>
        body {
            background: #ebebeb;
        }
        
        .nav {
            width: 560px;
            height: 50px;
            font: bold 0/50px Arial;
            text-align: center;
            margin: 40px auto 0;
            background: #f65f57;
            /*制作圆*/
            border-radius: 10px;
            /*制作导航立体风格*/
            box-shadow: 1px 5px rgb(108, 74, 64)
        }
        
        .nav a {
            display: inline-block;
            -webkit-transition: all 0.2s ease-in;
            -moz-transition: all 0.2s ease-in;
            -o-transition: all 0.2s ease-in;
            -ms-transition: all 0.2s ease-in;
            transition: all 0.2s ease-in;
        }
        
        .nav a:hover {
            -webkit-transform: rotate(10deg);
            -moz-transform: rotate(10deg);
            -o-transform: rotate(10deg);
            -ms-transform: rotate(10deg);
            transform: rotate(10deg);
        }
        
        .nav li {
            position: relative;
            display: inline-block;
            padding: 0 16px;
            font-size: 13px;
            text-shadow: 1px 2px 4px rgba(0, 0, 0, .5);
            list-style: none outside none;
            /*使用伪元素制作导航列表项分隔线*/
            background: no-repeat left/ 1px 15px linear-gradient(to right, #dd2926, #a82724);
            /*no-repeat 背景不会重复*/
        } 

        /*删除第一项和最后一项导航分隔线*/
        .nav li:first-child {
            background: none;
        }
        
        .nav a,
        .nav a:hover {
            color: #fff;
            text-decoration: none;
        }
    </style>
</head>

<body>
    <ul class="nav">
        <li><a href="">Home</a></li>
        <li><a href="">About Me</a></li>
        <li><a href="">Portfolio</a></li>
        <li><a href="">Blog</a></li>
        <li><a href="">Resources</a></li>
        <li><a href="">Contact Me</a></li>
    </ul>
</body>

</html>
```