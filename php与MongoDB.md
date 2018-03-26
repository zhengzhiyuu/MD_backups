---
title: php与MongoDB
date: 2017-06-01 13:43:50
tags: [mongoDB]
categories: [MongoDB]
---
启动mongoDB数据库 : mongod --dbpath D:mongo\data\db(数据库文件路径)
<!--more-->
### 基本操作：
```php
<?php
$m = new MongoClient(); // 连接默认主机和端口为：mongodb://localhost:27017
$db = $m->anson; // 获取名称为 "anson" 的数据库,没有则创建

$collection = $db->anson; // 选择集合,没有则创建

//获取提交数据
$userName = $_POST['username'];
$userPassword = $_POST['password'];

//插入数据
$document = array( 
	"name" => "$userName",
    "passwords" => "$userPassword"
);
$collection->insert($document);
echo "数据插入成功 <br>";

//查询数据
$query = array( "name" => "$userName" );
if($cursor = $collection->find($query)){
    echo $document["name"]."<br>";
    echo $document["passwords"];    
}

?>
```

### 补充：
#### 提交数据
```php
<?php
$m = new MongoClient(); // 连接默认主机和端口为：mongodb://localhost:27017
$db = $m->anson; // 获取名称为 "anson" 的数据库,没有则创建

$collection = $db->anson; // 选择集合,没有则创建

//获取提交数据
$userName = $_POST['name'];
$userPassword = $_POST['pas'];

//插入数据
$document = array( 
	"name" => "$userName",
    "passwords" => "$userPassword"
);
//向数据库提交账号信息
$collection->insert($document);
echo "账号注册成功  ";
?>
```
#### 查询数据
```php
<?php
$m = new MongoClient(); // 连接默认主机和端口为：mongodb://localhost:27017
$db = $m->anson; // 获取名称为 "anson" 的数据库,没有则创建

$collection = $db->anson; // 选择anson集合,没有则创建

$name = $_POST['name']; // 获取form表单的用户名
$password = $_POST['pas']; // 获取form表单的密码

//查询格式
$document = array( 
	"name" => $name
);
//向数据库提交查找
$cursor = $collection->find($document);
//查找数据总数 如果为0则用户不存在
$cursor2 = $collection->find($document)->count();
//条件判断 如果不等于0则：
if($cursor2 != 0){
    //遍历循环查找过来数据
    foreach ($cursor as $documents) {
    //如果名字等于用户的名字
    if($documents["name"] == $name){
        //并且密码也等于 则账号正确
        if($documents["passwords"] == $password){
            echo "账号正确";
        }else{
            //否则密码错误
            echo "密码错误";
        }
    }
  }
}else{
    //如果等于0用户不存在
    echo "用户名不存在";    
}

?>
```