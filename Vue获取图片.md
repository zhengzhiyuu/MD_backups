---
title: Vue获取图片
date: 2017-11-15 09:08:26
tags: [Vue]
---
```html
<input type="file" ref="file">
<button @click="getFile()">获取</button>
```
```js
getImg(){      
    //获取文件
    let file = this.$refs.file.files[0]
    //创建读取文件
    let reader = new FileReader()
    let img
    //读文件
    reader.onload = e => {
    img = e.target.result
    console.log(img)
    }
    reader.readAsDataURL(file)
}
```