---
title: Ajax 常用方法
date: 2017-05-05 16:38:13
tags: [JavaScript]
categories: [前端,JavaScript]
---
Ajax是交互不可缺少的
<!--more-->
### 1.创建XMLHttpRequest对象:
```js
const xhr = new XMLHttpRequest()'
```
IE5,IE6使用ActiveXObject("Microsoft.XMLHTTP")
我觉得可以抛弃IE5,IE6...
### 2.向服务器发送请求:
(使用 open()方法 和 send()方法)
```js
xhr.open("GET","a.txt",true);
xhr.send();
```
` open(method,url,async) `
- methid: 请求类型;GET或POST
- url: 文件地址
- async: 是否开启异步
` send(string) `
将请求发送到服务器
- string: 仅用于POST方法


#### GET与POST比较:
大部分情况请使用GET;
以下情况使用POST:
- 无法使用缓存文件(更新服务器上的数据或数据库)
- 向服务器发送大量数据(POST没有数据限制)
- 发送包含未知字符的用户输入,POST更稳当
` setRequestHeader(header,value) `
此方法仅用于POST方法
向请求添加HTTP头
- header: 头的名称
- value: 头的值
```js
 //加上时间戳为了组织缓存 new Date().getTime()
xhr.open("POST","a.txt"+ "?" + new Date().getTime(),true);
xhr.setrequestHeader("Content-type","application/x-www-form-urlencoded");
xhr.send();
```
### 3.获得服务器响应:
` responseText: `获得字符串形式的响应数据
`responseXML: `获得XML形式的响应数据
不是XML的使用responseText
### 4. onreadystatechange 事件:
执行一些基于响应的任务
每当 readyState 改变时，就会触发 onreadystatechange 事件
下面是 XMLHttpRequest 对象的三个重要的属性：
![此处输入图片的描述][1]
当 readyState 等于 4 且 status 状态为 200 时，表示响应已就绪：
```js
	xhr.onreadystatechange=function()
	{
		if (xhr.readyState==4 && xhr.status==200)
		{
            //获得数据
			let text = xhr.responseText;
		}
	}
```

Ajax方法封装:
比较简陋...
```js
 ajaxi({
    url: "ajax_1.txt",
    success: function (res) {
           console.log(res);
     },
    error: function () {
           console.log("失败");
     },
    data: {
           name: 'anson',
           age : 17
     },
    method: "post", //默认为GET
    cache: false, //默认false阻止缓存 开启缓存设为true
    async: true //默认为开启异步
   })
});
```
```js
function ajaxi(json) {
    let method = json.method ? json.method.toUpperCase() : "GET",
        url = json.url,
        txt = /.txt$/,jsons = /.json$/,
        success = json.success,
        error = json.error,
        async = json.async ? json.async : true,
        cache = json.cache ? json.cache : false,
        cacheUrl = cache ? url : url + "?a=" + new Date().getTime(),
        data = json.data ? json.data : null,
        datas = '',        
        ajaxi = new XMLHttpRequest();
        if(data instanceof Object){
            for(key in data){
                if(data.hasOwnProperty(key)){
                    datas += key + ":" + data[key] + " ; "
            }
          }
        }         
    ajaxi.open(method, cacheUrl, async);
    ajaxi.setRequestHeader('content-type' , 'application/x-www-form-urlencoded');
    ajaxi.send(datas);  
    console.log(datas);  
    ajaxi.onreadystatechange = function () {
        if (ajaxi.readyState == 4) {
            if (ajaxi.status == 200) {
                if(txt.test(url)){
                success(ajaxi.responseText)
                }else if (jsons.test(url)){
                    success(eval(ajaxi.responseText));
                }else{
                    success(ajaxi.responseText);
                }
            } else {
                error(ajaxi.status);
            }
        }
    }
}
```

底下这是啥 不知道 不知道 不知道
```js
new Anson("url地址")
    .content(function (rse) {
         console.log(rse[0].user)
     }, function () {
         console.log("错误");
                
```
```js
class Anson {
    constructor(url) {
        this.url = url;
        this.ajaxi = new XMLHttpRequest();

    }
    content(text,error) {
        let that = this;
        that.ajaxi.open("GET", this.url, true);
        that.ajaxi.send();
        that.ajaxi.onreadystatechange = function () {
            if (that.ajaxi.readyState == 4) {
                if (that.ajaxi.status == 200) {
                    text(eval(that.ajaxi.responseText));
                } else {
                    error(that.ajaxi.status);
                }
            }
        }
    }
}
```


  [1]: http://i1.piimg.com/1949/b25889aa6aaef02b.jpg