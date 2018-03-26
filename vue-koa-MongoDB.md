---
title: Vue+Koa+MongoDB
date: 2017-05-31 13:51:11
tags: [Node.Js,mongoDB,Vue]
categories: [前端,Node.Js,MongoDB,Vue]
---
重写于17年7月7/8/10日
<!--more-->
[参考教程][1]
![Vue][3]
## 问题汇总
### Vue打包
```js
npm run build
```
打包之后是无法直接打开，需要放到服务器环境:
node服务器：
1.使用koa生成器： 
```js
koa2 demo && cd demo && npm i
```
2.将打包文件` index.html `复制到` views `下
  将` ststic `文件夹下的` 文件夹 `复制到` public `下
3.修改` index.html `的` js `和` css `文件路径，如：
```html
<link href=/static/css/app.813a0c4380ae8d8063d6247ed0985f66.css rel=stylesheet>
```
修改为：
```html
<link href=css/app.813a0c4380ae8d8063d6247ed0985f66.css rel=stylesheet>
```
4.运行命令，启动服务：
```js
npm start
```
5.如果开启` history `模式则不能正确跳转，需要服务端配置支持` HTML5 History Mode `
6.使用pm2：
```bash
npm prd
```
### Ajax
使用vue官方推荐的axios
1.下载axios和vue-axios
2.在main.js中注册使用
```js
// scr/main.js
import VueAxios from 'vue-axios'
import axios from 'axios'

Vue.use(VueAxios,axios)
```
3.使用方法：
```js
// 1.
this.$http.get().then().catch
// 2.
this.axios.get().then().catch
```
` 不推荐 `
```js
Vue.prototype.$http = Axios
```
### 跨域问题
由于页面使用vue-cli 端口默认为8080，而koa的端口为3000，所以存在跨域问题
` 解决办法: `
1.koa使用koa的跨域模块：
  koa1的为： koa-cors
  koa2的为： koa2-cors  
推荐使用koa2的跨域模块，koa1似乎不怎么好用
2.在vue项目中找到webpack配置文件夹` config `的` index.js `
  修改` proxyTable ` ,添加如下内容：
```js
'/user': {
  target: 'http://localhost:3000',
  changeOrigin: true
}
```
这样配置` /user ` 相当于` http://localhost:3000/user `
这样看起来像是同源的...在项目打包以后放到koa下面时就时同源的啦
### vue设置导航拦截
```js
import Vue from 'vue'
import Router from 'vue-router'
import Hello from '@/components/Hello'

import Login from '../components/Login.vue'
import TodoList from '../components/TodoList.vue'
import Register from '../components/register.vue'

Vue.use(Router)

const router = new Router({
  routes: [{
      path: '/',
      name: 'login',
      component: Login
    },
    {
      path: '/todolist',
      name: 'todolist',
      component: TodoList
    },
    {
      path: '/register',
      name: 'register',
      component: Register
    }
  ]
})
router.beforeEach((to, from, next) => {
  const token = sessionStorage.getItem('demo-token')
  //如果起始页时登录或注册则继续
  if (to.path == '/' || to.path == '/register') {
    //如果在登录界面token不为空则跳转todolist
    if (token != 'null' && token != null) {
      next('/todolist')
    }
    next()
  } else {
    //如果token不为空则继续，否则跳回登录界面
    if (token != 'null' && token != null) {
      Vue.prototype.$http.defaults.headers.common['Authorization'] = 'Bearer ' + token
      next()
    } else {
      next('/')
    }
  }
})
export default router
```
### JsonWebToken
[koa jwt demo][4]
#### 1.下载node.js的jsonwebtoken模块
```js
npm i jsonwebtoken -S
```
#### 2.生成token
```js
const content = {
  //通过数据库查找过来的数据
  id: userData[0]._id
}
//签名
const secret = 'vueAndKoa2-demo2'
//生成token密钥
const token = jwt.sign(content, secret, {
  expiresIn: 60 * 2 //过期时间
})
```
#### 3.使用koa-jwt验证签发密钥
```js
npm i koa-jwt -S
```
##### 3.0 koa-jwt需要检查请求的herder中的` Authorization `属性是否有` Bearer `
在vue导航钩子中定义(回看vue设置导航拦截)：
Bearer 后面有一个空格
```js
Vue.prototype.$http.defaults.headers.common['Authorization'] = 'Bearer ' + token
```
以下操作都在app.js
##### 3.1 自定义401
```js
app.use(async(ctx, next) => {
  const start = new Date()
  const ms = new Date() - start
  console.log(`${ctx.method} ${ctx.url} - ${ms}ms`)
  return await next().catch((err) => {
    if (401 == err.status) {
      ctx.state = 401
      ctx.body = {
        info: 'No-401',
        success: false
      }
    } else {
      throw err
    }
  })
})
```
##### 3.2 使用koa-jwt
签名要一致 unless不包含使用user的路由
```js
app.use(koaJwt({
  secret: 'vueAndKoa2-demo2'
}).unless({path:[/^\/user/]}))
```
##### 3.3 定义使用koa-jwt的路由
```js
app.use(async ctx => {
  console.log(`Url:::${ctx.url}`)
  if (ctx.url.match(/^\/api/)) {
    ctx.body = 'ok'
  }
})
```
##### 3.4 在` api `下的路由使用` ctx.state.user ` 接收数据
```js
const getStateUser = async(ctx, next) => {
  ctx.body = ctx.state.user
}
```
如果正常，数据如下
```js
{id: "595e0bacef26c9282c9f3c22", iat: 1499565654, exp: 1499565774}
```
如果token过期则返回401信息
##### 3.5 使用vue-auth
```js
npm i vue-auth -S
```
配置如下：
```js
Vue.use(VueAuth, {
  stroagePrefix: '_prefix',
  authPath:'/', //过期跳转
  redirectType: 'router'
})
```
##### 3.6 不完整前端验证token思路
1.在vue的登录页面中使用` created `钩子函数检查token
  如果token没有过期自动跳转todolist
  如果token过期则返回401信息，401信息为之前自定义的401信息 
```js
created() {
  // 自定义的获取koa-jwt生成的ctx.state.user数据
  // 数据格式为：{id: "595e0bacef26c9282c9f3c22", iat: 1499565654, exp: 1499565774}
  // iat 生成的秒数时间戳 exp过期的秒数时间戳
  this.$http.post('/api/token')
    .then(res => {
      console.log(res.data)
      if (res.data.exp) {
        const exp = res.data.exp
        const now = Math.ceil(new Date().getTime() / 1000)
        if (now - exp >= 0) {
          console.log(now - exp)
          this.$router.push('/todolist')
        } else {
          this.$router.push('/')
        }
      } else if (res.data.success) {
        this.$router.push('/')
      }
    })
    .catch(err => console.log(err))
}
```
2.前端登录方法,密码使用md5加密
  发送数据，生成token，并使用` vue-auth `保存在localstorage
  跳转页面
```js
login() {
  localStorage.setItem('username', this.account)
  let data = {
    name: this.account,
    pass: md5(this.password)
  }
  this.$http.post('/user/find', data)
    .then(res => {
      if (res.data.success) {
        this.$auth.setToken(res.data.info)
        this.$router.push('/todolist')
        this.$message({
          type: 'success',
          message: '登录成功'
        })
      } else {
        this.$message({
          type: 'error',
          message: res.data.info
        })
        this.$auth.removeToken()
      }
    })
    .catch(err => {
      this.$message({
        type: 'error',
        message: '请求错误'
      })
    })
}
```
3.1在跳转过来的todolist页面使用` created `钩子函数检查token
```js
created() {
    this.$http.post('/api/token')
        .then(res => {
            if (res.data.success == false) {
                this.$auth.removeToken()
                this.$message.error('登录过期')
                this.$router.push('/')
            }
        })
        .catch(err => console.log(err))
}
```
3.2在todolist页面使用` updated `钩子函数
   只要用户有操作就更新token，使其保持登录状态(后端根据传过来的用户名检查用户是否合法)
   如果用户超过token有效时间，再操作就返回首页，提示用户信息
```js
updated() {
    //检查token是否存在 不存在直接返回登录
    const token = localStorage.getItem('_auth.token')
    const username = localStorage.getItem('username')
    if (token != 'null' && token != null) {
        if (username) {
            this.$http.post('/api/uptoken', { name: username })
                .then(res => {
                    if (res.data.token) {
                        console.log(res.data)
                        this.$auth.setToken(res.data.token)
                    }
                })
        }
        console.log(this.$auth.isAuthenticated())
        if (this.$auth.isAuthenticated() == false) {
            this.$router.push('/')
            this.$message.error('登录过期')
        }
    } else {
        this.$router.push('/')
        this.$message.error('token无效')
    }
}
```
##### 3.7 完整的app.js
```js
const Koa = require('koa')
const app = new Koa()
const views = require('koa-views')
const json = require('koa-json')
const onerror = require('koa-onerror')
const bodyparser = require('koa-bodyparser')
const logger = require('koa-logger')
const cors = require('koa2-cors')
const koaJwt = require('koa-jwt')

const index = require('./routes/index')
const users = require('./routes/users')
const api = require('./routes/api')

// error handler
onerror(app)

// middlewares
app.use(bodyparser({
  enableTypes: ['json', 'form', 'text']
}))
app.use(cors())
app.use(json())
app.use(logger())
app.use(require('koa-static')(__dirname + '/public'))
app.use(views(__dirname + '/views', {
  extension: 'html'
}))

// logger
app.use(async(ctx, next) => {
  const start = new Date()
  const ms = new Date() - start
  console.log(`${ctx.method} ${ctx.url} - ${ms}ms`)
  return await next().catch((err) => {
    if (401 == err.status) {
      ctx.state = 401
      ctx.body = {
        info: 'No-401',
        success: false
      }
    } else {
      throw err
    }
  })
})

//koa-jwt
app.use(koaJwt({
  secret: 'vueAndKoa2-demo2'
}).unless({path:[/^\/user/]}))

// routers
app.use(index.routes(), index.allowedMethods())
app.use(users.routes(), users.allowedMethods())
app.use(api.routes(), api.allowedMethods())

//使用koa-jwt的路由
app.use(async ctx => {
  console.log(`Url:::${ctx.url}`)
  if (ctx.url.match(/^\/api/)) {
    ctx.body = 'ok'
  }
})

module.exports = app
```
似乎koa-jwt注册要在router注册之前 ，监察路由需要在router注册之后



` 以下内容为最初版部分... `
## Vue页面:
```html
<template>
  <div>
    <h1>{{info}}</h1>
    <input type="text" v-model="name">
    <input type="password" v-model="password" @keyup.enter.native="login()">
    <button type="submit" @click="login()">点击</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      password: '',
      info:''
    }
  },
  methods: {
    login() {
      let obj = {
        name: this.name,
        password: this.password
      }
      this.$http.post(`http://localhost:8889/user`, obj)
        .then(response => {
          if (response.data.success) {
            this.info = response.data.info
          }else{
            this.info = response.data.info            
          }
        })
        .catch(err => console.log(err));
    }
  }
}
</script>
```
## 后端程序:
```js
├── server // Koa后端，用于提供Api
    ├── app.js // 入口文件
    ├── db.js // 连接数据库 提供数据库api
    ├── controller.js // controller-控制器
    └── router.js // route-路由
```
### app.js
```js
const Koa = require('koa'),
  router = require('koa-router')(),
  auth = require('./server/router'),
  cors = require('koa-cors')//koa跨域模块

const app = new Koa()

app.use(cors())
app.use(require('koa-bodyparser')());//post解析
app.use(router.routes())
router.use(auth.routes());//注册router.js文件

app.listen(8888, () => {
  console.log('koa runing at 8888 port')
})
```
### db.js
```js
const db = require('monk')('localhost/mydb') 
db.then(() => console.log('Connected correctly to server'))
const users = db.get('document')

//查找账户api
const getUserByName = async user_name => {
  let info = await users.find({
    name: user_name
  }).then(res => res)
  return info
}

//添加账户api
const postAuth = async(user_name, user_password) => {
  await users.insert({
    name: user_name,
    password: user_password
  }).then(res => console.log('User OK')).cahct(err => console.log(err))
}

module.exports ={
  getUserByName,
  postAuth
}
```
### controller.js
```js
const user = require('./db')

const getUserInfo = async content => {
  const userInfo = content.request.body
  const userAuth = await user.getUserByName(userInfo.name)
  console.log(userAuth)
  //数据库在查找为空时返回空
  if (userAuth != "") {
    if (userAuth[0].password != userInfo.password) {
      content.body = {
        success: false,
        info: "密码错误"
      }
    } else {
      content.body = {
        success: true,
        info: "账户正确"
      }
    }
  } else {
    content.body = {
      success: false,
      info: "用户不存在"
    }
  }
}

module.exports = getUserInfo
```
### router.js
```js
const router = require('koa-router')()
const auth = require('./controller')

router.post('/user',auth.getUserInfo)

module.exports = router
```


  [1]: http://www.tuicool.com/articles/2Qbe6bU
  [2]: http://www.jianshu.com/p/d7fcd17d79a9
  [3]: http://i1.piimg.com/1949/bd44ab308862d587.png
  [4]: https://github.com/zhengzhiyuu/koa-jwt-demo