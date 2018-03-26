---
title: bootstrap表格行的类
date: 2017-02-18 14:18:46
tags:
categories: [bootstrap仓库]
---
Bootstrap还为表格的行元素` <tr> `提供了五种不同的类名，每种类名控制了行的不同背景颜色，具体说明如下表所示：
![表格行的类][1]
示例：
```html
<tr class="active">
    <td>…</td>
</tr>
```
实现悬浮状态，需要在` <table> `标签上加入table-hover类
```html
<table class="table table-hover table-bordered">
  <thead>
    <tr>
      <th>类名</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr class="active">
      <td>.active</td>
      <td>表示当前活动的信息</td>
    </tr>
  </tbody>
</table> 
</body>
</html>
```



  [1]: http://img.mukewang.com/53ad213f0001b08807340508.jpg