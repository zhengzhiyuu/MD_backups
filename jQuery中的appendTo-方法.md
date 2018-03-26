---
title: jQuery中的appendTo()方法
date: 2017-02-12 20:52:33
tags:
categories: [jQuery仓库]
---
appendTo：实际上，使用这个方法是颠倒了常规的$(A).append(B)的操作，即不是把B追加到A中，而是把A追加到B中
<!--more-->
appendTo()前面是要插入的元素内容，而后面是被插入的对象
```js
<script type="text/javascript">

    	$("#bt2").on('click', function() {
    		//.appendTo()刚好相反，内容在方法前面，
    		//无论是一个选择器表达式 或创建作为标记上的标记
    		//它都将被插入到目标容器的末尾。
    		$('<div class="appendTo">通过appendTo方法添加的元素</div>').appendTo($(".content"))
    	})

</script>
```