---
title: select事件
date: 2017-02-16 08:28:11
tags:
categories: [jQuery仓库]
---
textarea 或文本类型的 input 元素中的文本被选择时，会发生 select 事件
<!--more-->
这个函数会调用执行绑定到select事件的所有函数，包括浏览器的默认行为。可以通过在某个绑定的函数中返回false来防止触发浏览器的默认行为
#### 方法一：.select()
触发元素的select事件:
```js
$("input").select();
```
#### 方法二：$ele.select( handler(eventObject) )
绑定$ele元素，每次$ele元素触发点击操作会执行回调 handler函数
这样可以针对事件的反馈做很多操作了
```html
<input id="test" value="文字选中"></input>
```
```js
$("#test").select(function() { //响应文字选中回调
    //this指向 input元素 
});
```
#### 方法三：$ele.select( [eventData ], handler(eventObject) )
使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题
```html
<input id="test" value="文字选中"></input>
```
```js
$("#test").select(11111,function(e) {//响应文字选中回调
    //this指向 div元素 
   //e.date  => 11111 传递数据
});
```

代码:
```js
//监听input元素中value的选中
//触发元素的select事件
$("input").select(function(e){
    alert(e.target.value)
})

//监听textarea元素中value的选中
$('textarea').select(function(e) {
    alert(e.target.value);
});
```
代码：
```html
<div class="aaron">
    <form id="target1" action="test.html">
         回车键或者点击提交表单： 
         <input type="text" value="输入新的值" />
         <input type="submit" value="Go" />
    </form>
</div>
<div class="aaron">
    <form id="target2" action="destination.html">
         回车键或者点击提交表单,禁止浏览器默认跳转： 
        <input type="text" value="输入新的值" />
          <input type="submit" value="Go" />
   </form>
</div>
```
```js
//回车键或者点击提交表单
$('#target1').submit(function(e) {
    alert('捕获提交表达动作,不阻止页面跳转')
});
//回车键或者点击提交表单,禁止浏览器默认跳转：
$('#target2').submit(function() {
    alert('捕获提交表达动作,阻止页面跳转')
    return false;
});
```
#### 通过在form元素上绑定submit事件，可以监听到用户的提交表单的的行为
具体能触发submit事件的行为：
```html
1. <input type="submit">
2. <input type="image">
3. <button type="submit">
4. 当某些表单元素获取焦点时，敲击Enter（回车键）
```
#### 注意：
form元素是有默认提交表单的行为，如果通过submit处理的话，需要禁止浏览器的这个默认行为
传统的方式是调用事件对象  e.preventDefault() 来处理， jQuery中可以直接在函数中最后结尾return false即可
jQuery处理如下：
```js
$("#target").submit(function(data) { 
   return false; //阻止默认行为，提交表单
});
```