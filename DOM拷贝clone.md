---
title: DOM拷贝clone()
date: 2017-02-13 14:17:19
tags:
categories: [jQuery仓库]
---
.clone()方法深度 复制所有匹配的元素集合，包括所有匹配元素、匹配元素的下级元素、文字节点。
<!--more-->
.clone(true) true可选 ：克隆附带的事件与数据

clone方法比较简单就是克隆节点，但是需要注意，如果节点有事件或者数据之类的其他处理，我们需要通过clone(ture)传递一个布尔值ture用来指定，这样不仅仅只是克隆单纯的节点结构，还要把附带的事件与数据给一并克隆了
Html代码：
```js
<body>
<h2>通过clone克隆元素</h2>
    <div class="left">
        <div class="aaron1">点击,clone浅拷贝</div>
        <div class="aaron2">点击,clone深拷贝,可以继续触发创建</div>
    </div>
</body>
```
javascript代码：
```js
<script type="text/javascript">
        //只克隆节点
    	//不克隆事件
	    $(".aaron1").on('click', function() {
	        $(".left").append( $(this).clone().css('color','red') )
	    })
</script>
```
```js
<script type="text/javascript">
    	//克隆节点
    	//克隆事件
	    $(".aaron2").on('click', function() {
	        $(".left").append( $(this).clone(true).css('color','blue') )
	    })
</script>
```