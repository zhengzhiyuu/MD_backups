---
title: vue过度效果配合annimate.css
date: 2017-07-05 10:09:39
tags: Vue
categories: [前端,Vue]
---
### 只有一个运动元素使用transition标签
enter-active-class 进入样式
leave-active-class 离开样式
```css
p {
    width: 100px;
    height: 100px;
    background: palegreen;
    margin: 10px auto;
}
```
```html
<div id="app">
    <button type="button" @click="show=!show">过度效果</button>
    <transition 
        enter-active-class="zoomInLeft" 
        leave-active-class="bounceOutRight"
    >
        <p v-if="show" class="animated"></p>
    </transition>
</div>
```
```js
new Vue({
    el: '#app',
    data() {
        return {
            show: true
        }
    }
})
```
### 有多个运动元素使用transition-group标签,并且把运动元素绑定相对应的` key `值
```html
<div id="app">
    <button type="button" @click="show=!show">过度效果</button>
    <transition-group 
        enter-active-class="zoomInLeft" 
        leave-active-class="bounceOutRight"
    >
        <p v-if="show" class="animated" :key="0"></p>
        <p v-if="show" class="animated" :key="1"></p>
    </transition-group>
</div>
```
```js
new Vue({
    el: '#app',
    data() {
        return {
            show: true
        }
    }
})
```
#### 列表循环
computed 实时监听数据,必须要有返回值
```html
<div id="app">
    <input type="text" v-model="input">
    <transition-group enter-active-class="zoomInLeft" leave-active-class="bounceOutRight">
        <p class="animated" v-for="(item,index) in lists" :key="index" v-if="show">
            {{item}}
        </p>
    </transition-group>
</div>
```
```js
new Vue({
    el: '#app',
    data() {
        return {
            input: '',
            list: ['apple', 'banana', 'orange', 'pear']
        }
    },
    computed: {
        lists() {
            let arr = []
            this.list.forEach((el) => {
                if (el.includes(this.input)) {
                    arr.push(el)
                }
            })
            return arr
        },
        show(){
            return this.input ? this.show = true : this.show = false
        }
    }
})
```