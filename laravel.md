---
title: laravel
date: 2017-08-31 22:26:30
tags: [laravel]
categories: [laravel]
---
php框架laravel的基本用法
<!-- more -->

启动：php artisan serve

### Migration
创建一个迁移数据表： ` php artisan make:migration create_name_table --create=name `
根据迁移生成数据表：` php artisan migrate `
撤销返回上一步： ` php artisan migrate:rollback `
Migration数据表：
```php
public function up()
{
    Schema::create('name', function (Blueprint $table) {
        $table->increments('id');
        $table->string('name');            
        $table->test('content');            
        $table->timestamps();
    });
}
```
### Elopuent
生成model: ` php artisan make:model Name `
创建的model与创建的表名相同，可以与表相关联
#### 插入数据：
打开一个命令行： ` php artisan tinker `
然后：` $name = new App\Name `
然后：` $name->name='zhiyu' `  // name来源于表结构
或者：` $name::create(['name'=>'zhiyu']); `
然后写入数据库：` $name->save();`
toArray():` $name->toArray(); ` //返回一个数组
find():` $name->find(1) ` //查找id为1的数据
更新数据：` $name->name='Anson' ` -> 再执行 ` $name->toArray(); `

#### 查找全部数据：
```php
public function index()
{
    $articles = Article::all();
    // return $articles;      
    return view('article',compact('articles'));
}
```
在blade中使用：
```html
@foreach($articles as $article)
    <h1>
        <a href="{{url('article',$article->id)}}">{{ $article->title }}</a>
    </h1>
@endforeach
```
### From
```js
composer require laravelcollective/html
```
更改config下的app.php
```php
Collective\Html\HtmlServiceProvider::class,
```

```php
'Form' => Collective\Html\FormFacade::class,
'Html' => Collective\Html\HtmlFacade::class,
```
在model中设置：
```php
protected $fillable = ['title', 'content','_token'];
```
定义路由：
```php
Route::post('/submitarticle','ArticleController@store');
```
数据提交：
```php
{!! Form::open(['url'=>'/submitarticle']) !!}
    <h1>创建一个新文章</h1>
    {!! Form::text('title',null,['placeholder'=>'文章标题']) !!}
    {!! Form::textarea('content',null,['placeholder'=>'文章内容']) !!}
    {!! Form::submit('发布文章') !!}
{!! Form::close() !!}
```
post数据接收：
```php
public function store(Request $request)
{
    //接收post数据 存入数据库 重定向
    $input = $request->all();
    Article::create($input);
    return redirect('/articles');
}
```
排序：以最新排序
```php
public function index()
{
    $articles = Article::latest()->get();
    return view('article',compact('articles'));
}
```



### 坑：
#### 注意MySQL端口号
```js
打开MySQL命令行
show global variables like 'port';
```
#### controller view 返回html文件
```php
public function login()
{
    \View::addExtension('html','php');       
    return view('login');
}
```
#### 使用多个数据库
1、配置.env文件
```php
 1 DB_CONNECTION=mysql
 2 DB_HOST=127.0.0.1
 3 DB_PORT=3306
 4 DB_DATABASE=database_name
 5 DB_USERNAME=root
 6 DB_PASSWORD=
 7 
 8 DB_HOST_CENTER=127.0.0.1
 9 DB_PORT_CENTER=3306
10 DB_DATABASE_CENTER=database_center
11 DB_USERNAME_CENTER=root
12 DB_PASSWORD_CENTER=
```
2、配置config/database.php
```php
'mysql' => [
    'driver' => 'mysql',
    'host' => env('DB_HOST', 'localhost'),
    'port' => env('DB_PORT', '3306'),
    'database' => env('DB_DATABASE', 'forge'),
    'username' => env('DB_USERNAME', 'forge'),
    'password' => env('DB_PASSWORD', ''),
    'charset' => 'utf8',
    'collation' => 'utf8_unicode_ci',
    'prefix' => '',
    'strict' => false,
    'engine' => null,
],
'mysql_center' => [
    'driver' => 'mysql',
    'host' => env('DB_HOST_CENTER', 'localhost'),
    'port' => env('DB_PORT_CENTER', '3306'),
    'database' => env('DB_DATABASE_CENTER', 'forge'),
    'username' => env('DB_USERNAME_CENTER', 'forge'),
    'password' => env('DB_PASSWORD_CENTER', ''),
    'charset' => 'utf8',
    'collation' => 'utf8_unicode_ci',
    'prefix' => '',
    'strict' => false,
    'engine' => null,
],
```
3、创建model
```php
// 这个model将采用默认的'mysql'连接
class UserModel extends Model
{
    // 数据库'database'中的users表
    protected $table = "users";
}
```
```php
// 这个model将使用mysql_center连接
class UserModel extends Model
{
　　// 数据库'dadtabase_center'中的users表
    protected $connection = 'mysql_center';
    protected $table = "users";
    protected $fillable = ['data','updated_at'];
}
```
#### 禁止updated_at和created_at
在模型中添加以下:
```php
public $timestamps = false;
```


Mysql乱码：
```php
mysql_query("set character set 'utf8'");//读库 
mysql_query("set names 'utf8'");//写库 
```