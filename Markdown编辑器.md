---
title: Markdown编辑器
date: 2017-06-04 20:27:25
tags: [JavaScript,Markdown]
categories: [前端,JavaScript]
---
多学一点总是没错的
<!--more-->
Markdown编辑器：[SimpleMDE][1]
Markdown语法解析：[marked][2]
代码语法高亮：[highlight][3]
### 实例：
#### 引入样式：
```html
    <link rel="stylesheet" href="./dist/simplemde.min.css">
    <link rel="stylesheet" href="./highlight/styles/default.css">
```
#### 引入js：
```js
    <script src="./dist/simplemde.min.js"></script>
    <script src="./node_modules/marked/lib/marked.js"></script>
    <script src="./highlight/highlight.pack.js"></script>
```
#### html：
```html
    <input type="textarea " name="" id="mde" value="">
    <button type="" id="sub">show</button>
    <div id="content"></div>
```
#### JavaScript:
```js
        let simplemde = new SimpleMDE({
            element: document.getElementById('mde')
        });

        let renderer = new marked.Renderer();

        marked.setOptions({
            renderer: renderer,
            gfm: true,
            pedantic: false,
            sanitize: false,
            tables: true,
            breaks: true,
            smartLists: true,
            smartypants: true,
            highlight: function (code) {
                return hljs.highlightAuto(code).value;
            }
        });
        document.getElementById('sub').addEventListener('click', function () {
            console.log(simplemde.value());
            document.getElementById('content').innerHTML =
                marked(simplemde.value());
        });
        hljs.initHighlightingOnLoad();
    </script>
```


  [1]: https://github.com/sparksuite/simplemde-markdown-editor
  [2]: https://github.com/chjj/marked
  [3]: https://github.com/isagalaev/highlight.js