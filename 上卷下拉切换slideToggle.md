---
title: 上卷下拉切换slideToggle
date: 2017-02-16 16:18:40
tags:
categories: [jQuery仓库]
---
基本的操作：slideToggle()
<!--more-->
这是最基本的操作，获取元素的高度，使这个元素的高度发生改变，从而让元素里的内容往下或往上滑。
提供参数：.slideToggle( [duration ] ,[ complete ] )
同样的提供了时间、还有动画结束的回调。在参数对应的时间内，元素会完成动画，然后出发回调函数
同时也提供了时间的快速定义，字符串 'fast' 和 'slow' 分别代表200和600毫秒的延时
```js
slideToggle("fast") 
slideToggle("slow") 
```
#### 注意：
- display属性值保存在jQuery的数据缓存中，所以display可以方便以后可以恢复到其初始值
- 当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局