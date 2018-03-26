---
title: jQuery中的append()方法
date: 2017-02-12 20:47:35
tags: 
categories: [jQuery仓库]
---
append：这个操作与对指定的元素执行原生的appendChild方法，将它们添加到文档中的情况类似
<!--more-->
append()前面是被插入的对象，后面是要在对象内插入的元素内容
```js
 <script type="text/javascript">

        $("#bt1").on('click', function() {
    		//.append(), 内容在方法的后面，
    		//参数是将要插入的内容。
    		$(".content").append('<div class="append">通过append方法添加的元素</div>')
    	})
</script>
```