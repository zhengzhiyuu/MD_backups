---
title: vue组件
date: 2017-07-02 15:56:40
tags: Vue
categories: [前端,Vue]
---
必须在vue实例之前创建
<!--more-->
### 全局组件
```html
<div id="example">
    <my-conponent></my-conponent>
</div>
```
```js
<script>
    Vue.component("my-conponent", {
        template: `<div>这是一个全局组件</div>`
    })

    new Vue({
        el:'#example',
    })
```
### 局部组件
```html
<div id="example">
    <my-conponent-b></my-conponent-b>
</div>
```
```js
<script>
const Child = { template: `<div>这是一个局部组件</div>` }

new Vue({
    el: '#example',
    components: {
        'my-conponent-b': Child
    }
})
</script>
```
### 动态组件
```html
<div id="example">
    <button type="botton" @click="isa()">组件a</button>
    <button type="botton" @click="isb()">组件b</button>
    <component :is="isis"></component>
</div>
```
```js
Vue.component("my-conponent-a", {
    template: `<div">组件a</div>`
})
Vue.component("my-conponent-b", {
    template: `<div">组件b</div>`
})

new Vue({
    el: '#example',
    data() {
        return {
            isis: 'my-conponent-a'
        }
    },
    methods: {
        isa() {
            this.isis = 'my-conponent-a'
        },
        isb() {
            this.isis = 'my-conponent-b'
        }
    }
})
```
### x-template
vue似乎不推荐这莫使用
```html
<div id="example">
    <my-conponent-a></my-conponent-a>
</div>

<template id="my-conponent-a">
    <div>这是一个组件</div>
</template>
```
```js
Vue.component("my-conponent-a", {
    template: '#my-conponent-a'
})

new Vue({
    el: '#example'
})
```
### 组件通信
#### 父组件向子组件传值
1.在父组件中给子组件标签绑定父组件数据
```html
<my-conponent-a-b  :data="counter"></my-conponent-a-b>
```
2.在子组件中使用`props: [String]`接受值
3.在子组件中使用绑定的属性名称
```html
<div id="example">
    <my-conponent-a></my-conponent-a>
</div>
```
```js
Vue.component("my-conponent-a", {
    template: `
        <div @click="counter+=1">
            <p>这是一个父组件 -> {{counter}}</p>
            <my-conponent-a-b  :data="counter"></my-conponent-a-b>
        </div>
    `,
    components: {
        'my-conponent-a-b': {
            props: ['data'],
            template: `
                <p>这是一个子组件 -> {{data}}</p>
            `
        }
    },
    data() {
        return {
            counter: 0
        }
    }
})

new Vue({
    el: '#example'
})
```
#### 子组件向父组件通信
由子组件主动发送数据
1.在子组件使用点击事件发送数据
vm.$emit(事件名,数据)
2.在父组件使用子组件发送的事件名为自定义事件
@...  在方法中使用参数接收数据
```html
<div id="example">
    <my-conponent-a></my-conponent-a>
</div>
```
```js
Vue.component("my-conponent-a", {
    template: `
        <div>
            <p>父组件 -> {{msg}}</p>
            <my-conponent-a-b @childMsg="getData"></my-conponent-a-b>
        </div>
    `,
    data() {
        return {
            msg: ' 我是父组件数据'
        }
    },
    methods: {
        getData(data) {
            this.msg = data
        }
    },
    components: {
        'my-conponent-a-b': {
            template: `
                <div>
                    <p>子组件 -> {{msg}}</p>
                    <button  @click="sendMsg()">发送数据</button>
                </div>
            `,
            data() {
                return {
                    msg: '我是子组件数据'
                }
            },
            methods: {
                sendMsg() {
                    this.$emit('childMsg', this.msg)
                }
            }
        }
    }
})
new Vue({
    el: '#example',
    data() {
        return {}
    }
})
```
#### 子组件更改数据父组件同步更改
1.使用` .sync `修饰符 vue版本最低为2.3
```html
<div id="app">
    <h2>父组件 -> {{msg}}</h2>
    <my-component :data.sync="msg"></my-component>
</div>
```
```js
const myCom = {
    template: `<div>
                    子组件 -> {{data}}
                    <button @click="change">改变数据</button>
                </div>`,
    props: ['data'],
    data() {
        return {
            msg: '改变数据'
        }
    },
    methods: {
        change() {
            this.$emit('update:data',this.msg)
        }
    }
}
const app = new Vue({
    data() {
        return {
            msg: '父组件数据'
        }
    },
    components: {
        'my-component': myCom
    }
}).$mount('#app')
```
2.父级传递给子集的为一个对象，改变对象的引用即可
```html
<div id="app">
    <h2>父组件 -> {{msg.a}}</h2>
    <my-component :data.sync="msg"></my-component>
</div>
```
```js
const myCom = {
    template: `<div>
                    子组件 -> {{data.a}}
                    <button @click="change">改变数据</button>
                </div>`,
    props: ['data'],
    methods: {
        change() {
            this.data.a = 'aaa'
        }
    }
}
const app = new Vue({
    data() {
        return {
            msg: {
                a: '父组件数据'
            }
        }
    },
    components: {
        'my-component': myCom
    }
}).$mount('#app')
```
#### 非父子组件通信
用一个空的vue实例来作为中央数据总线:
```js
const bus = new Vue()
```
```js
//在需要发送数据的组件触发事件
bus.$emit('data', this.data)
```
```js
//在接收的组件中创建钩子中的监听事件
bus.$on('data', (data) => {
    this.data = data
})
```
示例：
```html
<div id="app">
    <component-a></component-a>
    <component-b></component-b>
    <component-c></component-c>
</div>
```
```js
const bus = new Vue()
const componentA = {
    template: `
        <div>
            组件a -> {{dataA}}
            <button @click="seng">向C发送数据</button>
        </div>
    `,
    data() {
        return {
            dataA: '数据-a'
        }
    },
    methods: {
        seng() {
            bus.$emit('a-data', this.dataA)
        }
    }
}
const componentB = {
    template: `
        <div>
            组件b -> {{dataB}}
            <button @click="seng">向C发送数据</button>
        </div>
    `,
    data() {
        return {
            dataB: '数据-b'
        }
    },
    methods: {
        seng() {
            bus.$emit('b-data', this.dataB)
        }
    }
}
const componentC = {
    template: `
        <div>
            组件c -> 接收的数据：
            a:{{dataA}}
            b:{{dataB}}
        </div>
    `,
    data() {
        return {
            dataA: '',
            dataB: ''
        }
    },
    mounted() {
        //this指向 
        //1.使用箭头函数绑定this
        bus.$on('a-data', (data) => {
            console.log(data)
            this.dataA = data
        })
        //2.使用bind绑定this
        bus.$on('b-data', function (data) {
            console.log(data)
            this.dataB = data
        }.bind(this))
        //3.使用 let _this = this
    }
}
new Vue({
    components: {
        'component-a': componentA,
        'component-b': componentB,
        'component-c': componentC
    }
}).$mount('#app')
```