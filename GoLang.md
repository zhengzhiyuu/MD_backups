---
title: GoLang
date: 2017-10-18 14:00:32
tags: [GoLang]
---
golang图标超级萌
<!-- more -->
### golang web服务器
[参看0][1]
[参看1][2]
```go
package main

import (
	"fmt"
	"net/http"
	"log"
	"gopkg.in/mgo.v2"
	"gopkg.in/mgo.v2/bson"
	"encoding/json"
)

type Person struct {
	Name  string
	Phone string
}

func sayhelloName(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello astaxie!") //这个写入到w的是输出到客户端的
}

func sayLoveYou(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "love you!")
}

func getdata(w http.ResponseWriter,r *http.Request) {
	session, err := mgo.Dial("localhost:27017")
	if err != nil {
		panic(err)
	}
	session.SetMode(mgo.Monotonic, true)

	c := session.DB("test").C("people")

	resust := Person{}
	c.Find(bson.M{"name": "Anson"}).One(&resust)
	//fmt.Fprintf(w, resust.Name)

	// return json
	user := Person{
		resust.Name,
		resust.Phone,
	}
	json.NewEncoder(w).Encode(user)
}

func main() {
	http.HandleFunc("/", sayhelloName) //设置访问的路由
	http.HandleFunc("/love", sayLoveYou)
	http.HandleFunc("/get",getdata)
	err := http.ListenAndServe(":9090", nil) //设置监听的端口
	if err != nil {
		log.Fatal("ListenAndServe: ", err)
	}
}
```
### 连接mongodb数据库
1. 获取mgo，mgo是MongoDB的Go语言驱动
[mgo使用指南][3]
[官方文档][4]
[golang中使用MongoDB][5]    
```go
go get gopkg.in/mgo.v2
```
2. 连接mongodb
```go
session, err := mgo.Dial(url)
```
3. 使用数据库，没有会自行创建
```go
db := session.DB("test")
```
4. 使用数据库中的集合
```go
c := db.C("people")
// 或者
c := session.DB("test").C("people")
```
5. 建立数据模型
```go
type Person struct {
	Name  string
	Phone string
}
```
6. 插入数据
```go
c.Insert(&Person{"Anson", "1555555555"})
```
7. 查询数据
```go
result := Person{}
c.Find(bson.M{"name": "Anson"}).One(&result)
//result代理查询结果
fmt.Println("Phone:", result.Phone)
```
8. 查询所有数据
```go
//Person 为数据模型
var result []Person
c.Find(bson.M{}).All(&result)
fmt.Println("Phone:", result[0])
```
9. 更新数据
```go
c.Update(bson.M{"name":"Anson"}, &Person{"zhiyu","1666666666"})
```
10. 更新所有数据
```go
暂无
```
11. 删除数据
```go
c.Remove(bson.M{"name":"Anson2"})
```
完整版：
```go
package main

import (
	"gopkg.in/mgo.v2"
	"log"
	"gopkg.in/mgo.v2/bson"
	"fmt"
)

func main() {
	session, err := mgo.Dial("localhost:27017")
	if err != nil {
		panic(err)
	}

	session.SetMode(mgo.Monotonic, true)

	type Person struct {
		Name  string
		Phone string
	}
	// Connect to the database
	c := session.DB("test").C("people")

	// insert data
	err = c.Insert(&Person{"Anson", "1555555555"})
	if err != nil {
		log.Fatal(err)
	}
	
	// find data
	//result := Person{}
	//err = c.Find(bson.M{"name": "Anson"}).One(&result)
	
	// up data
	//err = c.Update(bson.M{"name":"Anson"}, &Person{"zhiyu","1666666666"})
	
	// delete data
	//err = c.Remove(bson.M{"name": "Anson"})

	// find data all
	var result []Person
	err = c.Find(bson.M{}).All(&result)
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println("Phone:", result[0])
}

```


  [1]: http://blog.csdn.net/chenxun_2010/article/details/52076482
  [2]: http://blog.csdn.net/xingwangc2014/article/details/51623157
  [3]: https://my.oschina.net/ffs/blog/300148
  [4]: https://godoc.org/gopkg.in/mgo.v2
  [5]: http://blog.csdn.net/wangshubo1989/article/details/75105397?locationNum=4&fps=1