---
title: Vue+Codrova混合App开发
date: 2017-10-25 15:08:37
tags: [Vue,Cordova,App]
---
### Cordova插件在Vue中使用：
1. 安装Cordova插件
[(手机状态栏-沉浸模式)][1]
[参考][2]
```bash
cordova plugin add cordova-plugin-statusbar
```
2. 安装Vue-Cordova插件
```bash
npm install --save vue-cordova
```
```js
import Vue from 'vue'
import VueCordova from 'vue-cordova'
Vue.use(VueCordova)
Vue.cordova.on('deviceready', () => {
  // Cordova插件使用
  if (cordova.platformId == 'android') {
    StatusBar.backgroundColorByHexString("#333");
    }
});
```
如果插件不好用 需要在index.html中加上：
```html
<script type=text/javascript src="cordova.js"></script>  
```
### backbutton事件,app退出
消息弹出框插件：
[文档][3]
[app][4]
```bash
cordova plugin add cordova-plugin-x-toast
```
```js
Vue.cordova.on('deviceready', () => {
  Vue.cordova.on('backbutton', eventBackButton)

  let backEventCount = 0
  
  function eventBackButton() {
    if (backEventCount === 0) {
      backEventCount += 1
      window.plugins.toast.showLongCenter('再点击一次退出')
      document.removeEventListener('backbutton', eventBackButton)
      setTimeout(() => {
        backEventCount = 0
      }, 2000)
    } else if (backEventCount === 1) {
      navigator.app.exitApp()
    }
  }
})
```


  [1]: http://cordova.apache.org/docs/en/latest/reference/cordova-plugin-statusbar/index.html
  [2]: http://blog.csdn.net/u011127019/article/details/58104056
  [3]: https://www.npmjs.com/package/cordova-plugin-x-toast
  [4]: http://www.cnblogs.com/suiyueshentou/p/6600449.html