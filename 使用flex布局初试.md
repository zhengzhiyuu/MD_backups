---
title: 使用flex布局初试
date: 2017-05-01 21:33:16
tags: [CSS]
categories: [前端,CSS]
---
第一次使用flex布局 有点混乱...
<!--more-->
` DOM结构: `
```html
    <div id="wrapper">
        <header>
            <section>
                <h1>Anson</h1>
            </section>
            <nav>
                <ul>
                    <li><a href="">Acticles</a></li>
                    <li><a href="">Books</a></li>
                    <li><a href="">Resources</a></li>
                    <li><a href="">bookshelf</a></li>
                    <li><a href="">Contact Me</a></li>
                </ul>
            </nav>
            <form action="#" method="post">
                <label for="urse_name">搜索</label>
                <input type="text" name="urse_name" id="urse_name" placeholder="搜索">
            </form>
        </header>
        <main>
            <section>
                <active>
                    <h4>May 1,2017</h4>
                    <a href="#">
                        <h3>this is...</h3>
                    </a>
                    <img src="mo.jpg" alt="" width="300px">
                    <p>This is ...This is ...This is ...This is ...This is ...This is ...This is ...This is ...This is ...This
                        is ...</p>
                </active>
            </section>
            <aside>
                <form action="#" method="post">
                    <h3>Sign In Code Updates</h3>
                    <label for="mail">Email</label>
                    <input type="text" name="mail" id="mail" placeholder="Emali">
                    <label for="pass">password</label>
                    <input type="password" name="psass" id="pass" placeholder="password">
                    <button type="submit" value="join in">Join In</button>
                    <p>Not signed up?<a href="#">Register now.</a></p>
                </form>
            </aside>
        </main>
        <footer>
            <p>Anson's exclusive page</p>
        </footer>
    </div>
```
` CSS样式为: `
```css
        * {
            margin: 0;
            padding: 0;
            text-decoration: none;
            list-style: none;
            outline: none;
        }

        body {
            background: #efefef;
        }

        #wrapper {
            display: flex;
            flex-direction: column;
            margin: 10px 60px;
        }

        header {
            flex: 1;
            display: flex;
            padding: 20px;
            height: 70px;
            line-height: 70px;
            background: #fff;
            border-radius: 20px 0 20px 0;
            box-shadow: 0px 2px 2px 0px black;
        }

        header section {
            flex: 0.5;
            letter-spacing: 0.25em;
            color: #4eb8ea;
        }

        header nav {
            flex: 1;
        }

        header form {
            flex: 0.5;
        }

        header nav li {
            float: left;
        }

        header nav li a {
            padding: 5px 9px;
        }

        header form input {
            width: 75px;
            border-radius: 10px 0 10px 0;
            padding: 2px 0 3px 5px;
            font-weight: 400;
            color: pink;
            transition: 1s width;
            float: right;
            position: relative;
            top: 23px;
        }

        header input:focus {
            width: 140px;
        }

        header input::-webkit-input-placeholder {
            color: paleturquoise;
        }

        header form label {
            display: none;
        }

        header nav li a {
            font-weight: 600;
            color: paleturquoise;
        }

        header nav li:nth-child(1) a {
            background: #f58c21;
            border-radius: 10px 0 0 5px;
        }

        header nav li:nth-child(2) a {
            background: #4eb8ea;
        }

        header nav li:nth-child(3) a {
            background: #d6e636;
        }

        header nav li:nth-child(4) a {
            background: #ee4c98;
        }

        header nav li:nth-child(5) a {
            background: #f58c21;
            border-radius: 0 5px 10px 0;
        }

        header nav li:hover a {
            color: #555;
        }

        main {
            flex: 1;
            display: flex;
            margin-top: 20px;
        }

        main section {
            flex: 1;
            margin-right: 20px;
            padding: 10px;
            border-radius: 20px 0 20px 0;
            background: #fff;
            box-shadow: 0px 2px 2px 0px black;
        }

        main img {
            float: left
        }

        main active p {
            float: left;
            padding-left: 20px;
            width: 300px;
            word-wrap: break-word;
        }

        main active p::first-letter {
            font-size: 4.5em;
            line-height: 0.7;
        }

        main aside {
            /*flex: 0.5;*/
            width: 300px;
            position: relative;
            right: 0;
            padding: 10px;
            border-radius: 20px 0 20px 0;
            background: #fff;
            box-shadow: 0px 2px 2px 0px black;
        }

        main form {
            margin-left: 30px;
        }

        main aside input {
            display: block;
            padding: 3px;
            margin: 3px;
        }

        main aside button {
            display: block;
            width: 100px;
            height: 30px;
            background: orange;
            border: none;
            border-radius: 10px 0 10px 0;
            margin: 10px 0 0 80px;
        }

        main aside p {
            margin-top: 20px;
            font-size: .6em
        }

        footer{
            flex: 1;
            background: #fff;
            margin-top: 30px;
            height: 50px;
            text-align: center;
            line-height: 50px;
            font-weight: 600;
            border-radius: 10px 0 10px 0; 
            
```
` 效果为: `
![此处输入图片的描述][1]


  [1]: http://chuantu.biz/t5/77/1493645778x2890174435.jpg