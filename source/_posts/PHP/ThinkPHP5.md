---
title: ThinkPHP5.0
date: 2020-04-02 11:57:42
tags: [PHP,ThinkPHP]
categories: PHP
---

ThinkPHP是一个免费开源的，快速、简单的面向对象的轻量级PHP开发框架，是为了敏捷WEB应用开发和简化企业应用开发而诞生的。

<!-- more -->

## 序言
ThinkPHP是一个免费开源的，快速、简单的面向对象的轻量级PHP开发框架，是为了敏捷WEB应用开发和简化企业应用开发而诞生的。

- [ThinkPHP5.0官方手册](https://www.kancloud.cn/manual/thinkphp5/118003)
## 基础
### 开发规范
函数和类、属性命名
- 类的命名采用驼峰法（首字母大写），例如 User、UserType，默认不需要添加后缀，例如UserController应该直接命名为User；
- 函数的命名使用小写字母和下划线（小写字母开头）的方式，例如 get_client_ip；
- 方法的命名使用驼峰法（首字母小写），例如 getUserName；
- 属性的命名使用驼峰法（首字母小写），例如 tableName、instance；
- 以双下划线“\_\_”打头的函数或方法作为魔术方法，例如 \_\_call 和 _\_autoload；

### 目录结构
如果是mac或者linux环境，请确保`runtime`目录有可写权限
目录结构和名称是可以改变的，尤其是应用的目录结构，这取决于你的入口文件和配置参数。

## 架构
### 架构总览
ThinkPHP5.0应用基于MVC（模型-视图-控制器）的方式来组织。
#### 入口文件
用户请求的PHP文件，负责处理一个请求（注意，不一定是URL请求）的生命周期，最常见的入口文件就是`index.php`
#### 应用
应用在ThinkPHP中是一个**管理系统架构及生命周期的对象**，由系统的 \think\App类完成，应用通常在入口文件中被调用和执行
#### 模块
#### 控制器
每个模块拥有独立的MVC类库及配置文件，一个模块下面有多个控制器负责响应请求，而每个控制器其实就是一个独立的控制器类。

控制器主要负责请求的接收，并调用相关的模型处理，并最终通过视图输出。

#### 模型
模型类通常完成实际的业务逻辑和数据封装，并返回和格式无关的数据。
#### 视图
控制器调用模型类后返回的数据通过视图组装成不同格式的输出。视图根据不同的需求，来决定调用模板引擎进行内容解析后输出还是直接输出。

### 生命周期
#### 入口文件
用户发起的请求都会经过应用的入口文件，通常是 public/index.php文件。
#### 引导文件

#### URL访问检测
应用初始化完成后，就会进行URL的访问检测，包括PATH_INFO检测和URL后缀检测。

### 入口文件
入口文件位置的设计是为了让应用部署更安全，public目录为web可访问目录，其他的文件都可以放到非WEB访问目录下面。

### URL访问
ThinkPHP5.0在没有启用路由的情况下典型的URL访问规则是：
`http://serverName/index.php（或者其它应用入口文件）/模块/控制器/操作/[参数名/参数值...]`

### 模块设计



## 路由
路由的作用是简化URL访问地址，并根据定义的路由类型做出正确的解析。

### 域名路由
ThinkPHP支持完整域名、子域名和IP部署的路由和绑定功能，同时还可以起到简化URL的作用。


## 控制器
### 控制器定义
```php
namespace app\index\controller;

class Index 
{
    public function index()
    {
        return 'index';
    }
}
```
控制器类文件的实际位置是`application\index\controller\Index.php`

### 控制器初始化
```php
namespace app\index\controller;

use think\Controller;

class Index extends Controller
{

    public function _initialize()
    {
        echo 'init<br/>';
    }
    
    public function hello()
    {
        return 'hello';
    }
}
```
如果访问`http://localhost/index.php/index/Index/hello`
会输出
```
init
hello
```
### 前置操作
### 跳转和重定向
> 重定向和跳转要继承Controller

#### 页面跳转

系统的\think\Controller类内置了两个跳转方法`success`和`error`，用于页面跳转提示。
```php
if ($result) {
    //设置成功后跳转页面的地址，默认的返回页面是$_SERVER['HTTP_REFERER']
    $this->success('新增成功', 'User/list');
} else {
    //错误页面的默认跳转页面是返回前一页，通常不需要设置
    $this->error('新增失败');
}
```
#### 重定向
\think\Controller类的redirect方法可以实现页面的重定向功能。
$this->redirect("http://localhost:8080/tp5/public/index.php");

## 请求
### 请求信息
如果要获取当前的请求信息，可以使用\think\Request类
`$request = Request::instance();`
或助手函数`$request = request();`

### 输入变量
#### 获取POST变量
```php
Request::instance()->post('name'); // 获取某个post变量
Request::instance()->post(); // 获取经过过滤的全部post变量
```
#### 获取SESSION变量
```php
Request::instance()->session('user_id'); // 获取某个session变量
Request::instance()->session(); // 获取全部的session变量
```
#### 获取Cookie变量
```php
Request::instance()->cookie('user_id'); // 获取某个cookie变量
Request::instance()->cookie(); // 获取全部的cookie变量
```

## 数据库
### 连接数据库
### 基本使用
支持query（查询操作）和execute（写入操作）方法
```php
Db::query('select * from think_user where id=?',[8]);
Db::execute('insert into think_user (id, name) values (?, ?)',[8,'thinkphp']);
```
### 查询构造器
#### 查询数据
查询一个数据使用：
```php
// table方法必须指定完整的数据表名
Db::table('think_user')->where('id',1)->find();
```
查询数据集使用：
```php
Db::table('think_user')->where('status',1)->select();
```
#### 添加数据
添加一条数据
```php
$data = ['foo' => 'bar', 'bar' => 'foo'];
Db::table('think_user')->insert($data);
```
添加多条数据
```php
$data = [
    ['foo' => 'bar', 'bar' => 'foo'],
    ['foo' => 'bar1', 'bar' => 'foo1'],
    ['foo' => 'bar2', 'bar' => 'foo2']
];
Db::name('user')->insertAll($data);
```
#### 更新数据
`Db::table('think_user')->where('id', 1)->update(['name' => 'thinkphp']);`
#### 删除数据
```php
// 根据主键删除
Db::table('think_user')->delete(1);
Db::table('think_user')->delete([1,2,3]);

// 条件删除    
Db::table('think_user')->where('id',1)->delete();
Db::table('think_user')->where('id','<',10)->delete();
```
## 视图
继承\think\Controller类
### 模板渲染
```php
// 不带任何参数 自动定位当前操作的模板文件
return $this->fetch();
```

## 模板
### 包含文件
{include file='模版文件1,模版文件2,...' /}

### 内置标签
volist标签通常用于查询数据集（select方法）的结果输出，通常模型的select方法返回的结果是一个二维数组，可以直接使用volist标签进行输出。

### 资源文件加载
传统方式的导入外部JS和CSS文件的方法是直接在模板文件使用：
```php
<script type='text/javascript' src='/static/js/common.js'>
<link rel="stylesheet" type="text/css" href="/static/css/style.css" />
```