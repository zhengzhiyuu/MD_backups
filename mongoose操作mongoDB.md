---
title: MongoDB的基本使用方法
date: 2017-09-30 09:09:00
tags: [Node.Js,mongoDB]
categories: [前端,Node.Js,Koa]
---
Mongodb一些基本使用方法总结
<!--more-->
## Ubuntu安装mongodb
[相关连接][1]
### 1. 安装
```bash
sudo apt-get install mongodb
```
### 查看版本
```bash
mongo -version
```
### 开启和关闭
```bash
service mongodb start
service mongodb stop
```
默认设置MongoDB是随Ubuntu启动自动启动的。 
### 查看是否启动成功
```bash
pgrep mongo -l
```
### 卸载MongoDB
```bash
sudo apt-get --purge remove mongodb mongodb-clients mongodb-server
```
## Mongodb数据迁移
[参考][2]
### 备份
```bash
mongodump -h dbhost  -d dbname -o dbdirectory
```
**-h:**  mongodb所在服务器地址，例如127.0.0.1，也可以指定端口:127.0.0.1:8080 

**-d:**  需要备份的数据库名称，例如：test_data

**-o:**  备份的数据存放的位置，例如：/home/bak

**-u:**  用户名称，使用权限验证的mongodb服务，需要指明导出账号

**-p：** 用户密码，使用权限验证的mongodb服务，需要指明导出账号密码
### 恢复
```bash
mongorestore -d test --drop dbdirectory
```
**-d:**  需要恢复备份的数据库名称，例如：test_data，可以跟原来备份的数据库名称不一样

**dbdirectory:** 备份数据所在位置，例如：/home/bak/test

**-drop:** 加上这个参数的时候，会在恢复数据之前删除当前数据

## [MongoDB可视化工具][3]
使用` Node工具 `操作 MongoDB 数据库

[monk][4]
## Monk模块基本用法
```js
npm i monk
```
```js
//连接mydb数据库
const db = require('monk')('localhost/mydb')
db.then(() => console.log('Connected correctly to server'))
//获取数据表
const users = db.get('document')

//添加数据
users.insert({
  name: "zhiyu",
  password: '123'
}).then((res) => console.log('Yes')).catch((err)=>console.log(err))

//更新数据
let old_date = {name: "zhiyu",password: '123'},
    up_date= {name: "zhiyu",password: '789'}
  users.update(old_date,up_date)
       .then((res)=>console.log('OK'))
       .catch((err)=>console.log(err))

//删除数据
let del_date = {name: "anson",password: '789'}
  users.remove(del_date)
       .then((res)=>console.log('OK'))
       .catch((err)=>console.log(err))

//查找数据
let find_date = {password: '789'}
  users.find(find_date)
       .then((res)=>console.log(res))
       .catch((err)=>console.log(err))
```
## Mongoose
```js
npm i mongoose
```
[mongoose官网][5]
[mongoose教程-1][6]
[mongoose教程-2][7]
[mongoose教程-3][8]
```
server
│      mongodb.js
│      
├─controllers
│      test.js
│      
├─module
│      test.js
```

### mongodb.js - 连接数据库
```js
const mongoose = require('mongoose')
mongoose.Promise = global.Promise
const config = require('./../config/index')

mongoose.connect('127.0.0.1', {
    useMongoClient: true,
    promiseLibrary: global.Promise
})

module.exports = mongoose
```
### 定义数据模型 - model/test.js
```js
const mongoose = require('./../server/mongodb')

const testSchema = new mongoose.Schema({
    hidden: Boolean,
    title: String,
    createTime: Date,
    content: String
})

testSchema.set('toJSON', {
    getters: true,
    virtuals: true
})
testSchema.set('toObject', {
    getters: true,
    virtuals: true
})

const test = mongoose.model('test', testSchema)
module.exports = test
```
### 控制器获取数据 - controller/test.js
#### 引入test数据模型
```js
const Test = require('./../module/test')
```
#### 插入数据
1. 先` new 引入的模型` ， 并赋值给变量
2. 再对变量进行` save() ` , 并返回结果
****
```js
const create = async ctx => {
        const test = new Test({
            hidden: ctx.request.body.hidden,
            title: ctx.request.body.title,
            createTime: new Date(),
            content: ctx.request.body.content
        })
        let result = await test.save().catch(error => console.log(error))
        ctx.body = {
            success: true,
            data: result
        }
    } 
}
```
#### 查找数据,并排序
1. Model.find({})
2. sort({})
***
```js
const testList = async ctx => {
    let result = await Test.find({}).sort({
        createTime: -1
        //按创建时间倒排序
    }).exec()
    ctx.body = {
        success: true,
        data: result
    }
}
```
#### 更新数据
Model.update({1},{2})
1:查找的条件
2：修改的选项
```js
const update = async ctx => {
    let result = await Test.update({
        _id: ctx.request.body.id
    }, {
        title: ctx.request.body.title,
        content: ctx.request.body.content,
        createTime: new Date()
    })
    ctx.body = {
        success: true,
        data: result
    }
}
```


### upUser.js - 更新数据
```js
function update(){
    let name = {name:'zhyu'};
    let uppassword = {password:"123"};
    //直接作用在引入的User
    User.update(name,uppassword,(err,res)=>{
        if(res){
            console.log('OK:' + res);
        }else{
            console.log('ERR:'+ err);
        }
    })
}

update();
```
### delUser.js - 删除数据
```js
function deldate() {
    let del_name = {name: 'zhyu'};
    //直接作用在引入的User    
    User.remove(del_name, (err, res) => {
      if (res) {
        console.log('OK:' + res);
      } else {
        console.log('ERR:' + err);
      }
    })
}
deldate();
```
### getUser.js -查找数据
```js
function getName(){
    let get_name  = {'name' : 'zhyu'};
    //直接作用在引入的User        
    User.find(get_name, function(err, res){
        if (res) {
            if(res === get_name.name){
                console.log('Yes')
            }else{
                console.log('No')
            }
        }
        else {
            console.log("Error:" + err);            
        }
    })
}

getName();
```


  [1]: http://blog.csdn.net/flyfish111222/article/details/51886787
  [2]: http://blog.csdn.net/huwei2003/article/details/41122169
  [3]: https://robomongo.org/download
  [4]: https://automattic.github.io/monk/
  [5]: http://www.nodeclass.com/api/mongoose.html#quick_start
  [6]: http://www.cnblogs.com/zhongweiv/p/mongoose.html#mg_op
  [7]: http://www.tuicool.com/articles/BBnYR3B
  [8]: http://cnodejs.org/topic/504b4924e2b84515770103dd