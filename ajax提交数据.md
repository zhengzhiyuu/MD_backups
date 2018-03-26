---
title: php获取Ajax数据
date: 2017-05-22 18:43:49
tags: [JavaScript]
categories: [前端,JavaScript]
---
最近一直苦于怎么用Ajax把数据提交到php,终于找到了解决变法.
<!--more-->
代码如下：
```js
let params = new URLSearchParams();
params.append('username',   'Anson');
axios.post('url', params)
     .then(response => msgP.innerHTML = username.value)
     .catch(error => console.log(error));
```
```php
<?php
$name = $_POST["username"];
echo "$name";
?>
```
使用的axios库