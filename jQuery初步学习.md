---
title: jQuery初试(选择器)
date: 2017-02-11 19:12:25
updated: 2017-02-12 10:00:00
tags: jQuery
categories: [前端,jQuery]
---
jQuery是javascript的一个子集，jQuery使人们不用顾虑浏览器的兼容性（我说的就是IE）。
这里主要介绍jQuery的选择器
<!-- more -->
#### 引入jQuery库： ####
```js
<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
```
#### jQuery版的Hello，World！####
```js
<script>
        $(document).ready(function () {
            $("div").html("Hello,world!");
        })
</script>
```
#### jQuery中的页面加载后 “监听事件”的方法： ####
```js
$(document).ready(function(){});
```
等同于
```js
window.onload = function(){};
```
但ready事件优先于onload事件执行
#### 简单的jQuery选择器 ####
jQuery基本选择器

* ##### ID选择器：$("#id") 

* ##### Class选择器：$(".Class")

- ##### 标签选择器：$("tagname")

- ##### 通配选择器：$(" * ")

- ##### 组选择器：$("seletor1,seletor2,~N")

- ##### 层级选择器
![此处输入图片的描述][1]
```js
<script type="text/javascript">
        //子选择器
        //$('div > p') 选择所有div元素里面的子元素P
        $('div>p').css("border", "1px groove red");
</script>

<script type="text/javascript">
        //后代选择器
        //$('div  p') 选择所有div元素里面的p元素
        $('div p').css("border", "1px groove red");
</script>

<script type="text/javascript">
        //相邻兄弟选择器
        //选取prev后面的第一个的div兄弟节点
        $('div+span').css("border", "3px groove red");
</script>

<script type="text/javascript">
        //一般相邻选择器
        //选取prev后面的所有的div兄弟节点
        $('.prev~div').css("border", "3px groove green");
</script>
```
- ##### 基本筛选选择器
![此处输入图片的描述][2]
```js
<script type="text/javascript">
        //找到第一个div
        $(".div:first").css("color", "#CD00CD");
</script>

<script type="text/javascript">
        //找到最后一个div
        $(".div:last").css("color", "#CD00CD");
</script>

<script type="text/javascript">
        //:even 选择所引值为偶数的元素，从 0 开始计数
        $(".div:even").css("border", "3px groove red");
</script>

<script type="text/javascript">
        //:odd 选择所引值为奇数的元素，从 0 开始计数
        $(".div:odd").css("border", "3px groove blue");
</script>

<script type="text/javascript">
        //:eq
        //选择单个
        $(".aaron:eq(2)").css("border", "3px groove blue");
</script>

<script type="text/javascript">
        //:gt 选择匹配集合中所有索引值大于给定index参数的元素
        $("aaron:gt(3)").css("border", "3px groove blue");
</script>

<script type="text/javascript">
        //:lt 选择匹配集合中所有索引值小于给定index参数的元素
        //与:gt相反
        $(".aaron:lt(2)").css("color", "#CD00CD");
</script>

<script type="text/javascript">
        //:not 选择所有元素去除不匹配给定的选择器的元素
        //选中所有紧接着没有checked属性的input元素后的p元素，赋予颜色
        $("input:not(:checked)+p").css("background-color", "#CD00CD");
</script>  
```
* ##### 内容筛选选择器
![此处输入图片的描述][3]
```js
<script type="text/javascript">
        //查找所有class='div'中DOM元素中包含"box"的元素节点
        //并且设置颜色
        $(".div:contains('box')").css("color","#CD00CD");
</script>

<script type="text/javascript">
       //选择所有包含子元素或者文本的a元素
       //增加一个蓝色的边框
       $("a:parent").css("border", "3px groove blue");
</script>

<script type="text/javascript">
       //找到a元素下面的所有空节点(没有子元素)
       //增加一段文本与边框
       $("a:empty").text(":empty").css("border", "3px groove red"); 
</script>

<script type="text/javascript">
        //查找所有class='div'中DOM元素中包含"span"的元素节点
        //并且设置颜色
        $(".div:has(span)").css("color", "blue");
</script>
```
* ##### 可见性筛选选择器
![此处输入图片的描述][4]
```js
<script type="text/javascript">
    	//查找id = div1的DOM元素,是否可见
    	show($("#div1:visible"));
</script>

<script type="text/javascript">
    	//查找id = div1的DOM元素,是否隐藏
    	show($("div1:hidden"));
</script>
```
* ##### 属性筛选选择器
![此处输入图片的描述][5]
```js
<script type="text/javascript">
        //查找所有div中，属性name=p1的div元素
        $("div[name=p1]").css("border", "3px groove red");
</script>

<script type="text/javascript">
        //查找所有div中，有属性p2的div元素
        $("div[p2]").css("border", "3px groove blue");
</script>

<script type="text/javascript">
        //查找所有div中，有属性name中的值只包含一个连字符“-”的div元素
        $('div[name|="-"]').css("border", "3px groove #00FF00");
</script>

<script type="text/javascript">
        //查找所有div中，有属性name中的值包含一个连字符“空”和“a”的div元素
        $('div[name~="a"]').css("border", "3px groove #668B8B");
</script>

<script type="text/javascript">
        //查找所有div中，属性name的值是用bob开头的
        $('div[name^=bob]').css("border", "3px groove red");
</script>

<script type="text/javascript">
        //查找所有div中，属性name的值是用bob结尾的
        $("div[name$=bob]").css("border", "3px groove blue");
</script>
    
<script type="text/javascript">
        //查找所有div中，有属性name中的值包含一个test字符串的div元素
        $('div[name*="test"]').css("border", "3px groove #00FF00");
</script>

<script type="text/javascript">
        //查找所有div中，有属性testattr中的值没有包含"true"的div
        $('div[testattr!="true"]').css("border", "3px groove #668B8B");
</script>
```
* ##### 子元素筛选选择器
![此处输入图片的描述][6]
```js
<script type="text/javascript">
        //查找class="first-div"下的第一个a元素
        //针对所有父级下的第一个
        $('.first-div a:first-child').css("color", "#CD00CD");
</script>

<script type="text/javascript">
        //查找class="first-div"下的最后一个a元素
        //针对所有父级下的最后一个
        //如果只有一个元素的话，last也是第一个元素
        $('.first-div a:last-child').css("color", "red");
</script>

<script type="text/javascript">
        //查找class="first-div"下的只有一个子元素的a元素
        $('.first-div a:only-child').css("color", "blue");
</script>

<script type="text/javascript">
        //查找class="last-div"下的第二个a元素
        $('last-div a:nth-child(2)').css("color", "#CD00CD");
</script>

<script type="text/javascript">
        //查找class="last-div"下的倒数第二个a元素
        $('last-div a:nth-last-child(2)').css("color", "red");
</script>
```
* ##### 表单元素选择器
![此处输入图片的描述][7]
```js
<script type="text/javascript">
        //查找所有 input, textarea, select 和 button 元素
        //:input 选择器基本上选择所有表单控件
        $(':input').css("border", "1px groove red"); 
</script>

<script type="text/javascript">
        //匹配所有input元素中类型为text的input元素
        $('input:text').css("background", "#A2CD5A");
</script>

<script type="text/javascript">
        //匹配所有input元素中类型为password的input元素
        $('input:password').css("background", "yellow");
    </script>

<script type="text/javascript">
        //匹配所有input元素中的单选按钮,并选中
        $('input:radio').attr('checked','true');
</script>

<script type="text/javascript">
        //匹配所有input元素中的复选按钮,并选中
        $('input:checkbox').attr('checked','true'); 
</script>

<script type="text/javascript">
        //匹配所有input元素中的提交的按钮,修改背景颜色
        $('input:submit').css("background", "#C6E2FF");
</script>

<script type="text/javascript">
        //匹配所有input元素中的图像类型的元素,修改背景颜色
        $('input:img').css("background", "#F4A460");
</script>

<script type="text/javascript">
        //匹配所有input元素中类型为按钮的元素
        $('input:button').css("background", "red");
</script>

<script type="text/javascript">
        //匹配所有input元素中类型为file的元素
        $('input:file').css("background", "#CD1076");
</script>
```
* ##### 表单对象属性选择器
![此处输入图片的描述][8]
```js
<script type="text/javascript">
        //查找所有input所有可用的（未被禁用的元素）input元素。
        $('input:enabled').css("border", "2px groove red");
</script>

<script type="text/javascript">
        //查找所有input所有不可用的（被禁用的元素）input元素。
        $('input:disabled').css("border", "2px groove blue");
</script>

<script type="text/javascript">
         //查找所有input所有勾选的元素(单选框,复选框)
         //移除input的checked属性
        $('input:checked').removeAttr('checked')
</script>

<script type="text/javascript">
         //查找所有option元素中,有selected属性被选中的选项
         //移除option的selected属性
        $('option:selected').removeAttr('selected')
</script>
```
* ##### 特殊选择器this
JavaScript原生DOM处理
```js
<script type="text/javascript">
        var p1 = document.getElementById('test1')
        p1.addEventListener('click',function(){
            //直接通过dom的方法改变颜色
            this.style.color = "red"; 
        },false);
</script>
```
jQuery处理
```js
<script type="text/javascript">
        $('#test2').click(function(){
            //通过包装成jQuery对象改变颜色
            $(this).css('color','blue');
        })
</script>
```

#### Dom对象转换jQuery对象
```js
var div = document.getElementsByTagName('div'); //dom对象
        div[1].style.color = "blue";
        //将dom节点div转化为$div的jquery对象
        var $div = $(div);

        // var $first = $div.first(); //找到第一个div元素
        // $first.css('color', 'red'); //给第一个元素设置颜色
        $div.get(0).style.color = "red";
        $("div").get($div.length -1).style.color = "pink";
```
#### jQuery对象转换Dom对象
```js
var $div = $('div'); //jQuery对象
		var div = $div.get(0);
		div.style.color = 'red'; //操作dom对象的属性
```


  [1]: http://img.mukewang.com/5590e98b0001f60d06130229.jpg
  [2]: http://img.mukewang.com/57cd1df2000146de06020498.jpg
  [3]: http://img.mukewang.com/57cd20bf0001a97f05290214.jpg
  [4]: http://img.mukewang.com/5590f6de0001e2b204460106.jpg
  [5]: http://img.mukewang.com/57d654200001c46507360560.jpg
  [6]: http://img.mukewang.com/559105da0001301105960331.jpg
  [7]: http://img.mukewang.com/5592040d0001f8eb04940441.jpg
  [8]: http://img.mukewang.com/55920c2f0001198b04940201.jpg