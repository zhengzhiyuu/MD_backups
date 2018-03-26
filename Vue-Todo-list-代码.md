---
title: Vue Todo list 代码
date: 2017-02-18 19:32:23
tags: Vue
categories: [前端,Vue]
---
Vue初学
<!--more-->
```html
<template>
  <div class="hello">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-text="item.label" v-bind:class="{items: item.isOk}" v-on:click="onclick(item)">
      </li> 
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'hello',
    data () {
      return {
        title: 'this is a todo list',
        items: [],
        newItem: ''
      }
    },
    methods: {
      onclick: function (item) {
        item.isOk = !item.isOk
      },
      addNew: function () {
        this.items.push({
          label: this.newItem,
          isOk: false
        })
        this.newItem = ''
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
  margin-top: 200px;
}
.items{
  text-decoration: line-through;  
}
ul,li{
  list-style-type: none;
}
</style>
```