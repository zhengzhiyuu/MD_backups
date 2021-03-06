---
title: HTML5语义化
date: 2017-10-17 08:58:50
tags: [前端,HTML5]
categories: [前端]
---
HTML5语义化
<!-- more -->
### 语义化作用：
1. 搜索引擎友好。
2. 更容易让屏幕阅读器读出网页内容。
3. 去掉或样式丢失的时候能让页面呈现清晰的结构。
4. 便于团队开发和维护。
### 基本结构：
![此处输入图片的描述][1]
### 常用标签
#### ` <header></header> `：
页眉通常包括网站标志、主导航、全站链接以及搜索框。也适合对页面内部一组介绍性或导航性内容进行标记。
#### ` <nav></nav> `：
标记导航，仅对文档中重要的链接群使用。html5规范不推荐对辅助性页脚链接使用nav，除非页脚再次显示顶级全局导航、或者包含招聘信息等重要链接。
#### ` <main></main> `：
页面主要内容，一个页面只能使用一次。如果是web应用，则包围其主要功能。
#### ` <section></section> `：
表示文档中的一个区域（或节），比如，内容中的一个专题组，一般来说会有包含一个标题（heading）。
#### ` <article></article>`：
是一个特殊的section标签，它比section具有更明确的语义，它代表一个独立的、完整的相关内容块，可独立于页面其它内容使用。例如一篇完整的论坛帖子，一篇博客文章，一个用户评论等等。一般来说，article会有标题部分（通常包含在header内），有时也会包含footer。article可以嵌套，内层的article对外层的article标签有隶属关系。例如，一篇博客的文章，可以用article显示，然后一些评论可以以article的形式嵌入其中。
#### ` <aside></aside> `：
指定附注栏，包括引述、侧栏、指向文章的一组链接、广告、友情链接、相关产品列表等。如果放在main内，应该与所在内容密切相关。
#### ` <footer></footer> `：
页脚，只有当父级是body时，才是整个页面的页脚
#### ` <figure></figure> `：
创建图（默认有40px左右margin）。
#### ` <figcaption></figcaption> `：
figure的标题，必须是figure内嵌的第一个或者最后一个元素。
#### ` <time></time> `：
标签定义日期或时间，或者两者。
```html
<time datetime="2017-10-17">2017.10.17</time>
```



  [1]: http://ow7xl4sc8.bkt.clouddn.com/1.png