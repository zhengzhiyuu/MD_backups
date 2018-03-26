---
title: change事件
date: 2017-02-15 18:58:16
categories: [jQuery仓库]
---
input元素，textarea和select元素的值都是可以发生改变的，通过change事件去监听这些改变的动作
<!--more-->
#### 注释：
当用于 select 元素时，change 事件会在选择某个选项时发生。当用于 textfield 或 textarea 时，该事件会在元素失去焦点时发生
#### input元素
监听value值的变化，当有改变时，失去焦点后触发change事件。对于单选按钮和复选框，当用户用鼠标做出选择时，该事件立即触发。 
#### select元素
对于下拉选择框，当用户用鼠标作出选择时，该事件立即触发 
#### textarea元素
多行文本输入框，当有改变时，失去焦点后触发change事件
```html
<div class="left">
    //监听input的改变
    <div class="aaron">input：
         <input class="target1" type="text" value="监听input的改变" />
    </div>
    //监听select的改变
    <div class="aaron1">select：
        <select class="target2">
            <option value="option1" selected="selected">Option 1</option>
            <option value="option2">Option 2</option>
       </select>
    </div>
    //监听textarea的改变
    <div class="aaron3">textarea：
        <textarea class="target2" rows="3" cols="20">多行的文本输入控件</textarea>
    </div>
</div>
    输出结果：  
    <div id="result"></div>
```
```js
//监听input值的改变
    $('.target1').change(function(e) {
        $("#result").html(e.target.value)
    });

    //监听select：
    $(".target2").change(function(e) {
        $("#result").html(e.target.value)
    })

     //监听textarea：
    $(".target3").change(function(e) {
        $("#result").html(e.target.value)
    })
```