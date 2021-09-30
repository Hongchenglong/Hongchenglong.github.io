---
title: PHP笔记
date: 2020-03-15 9:0:0
tags: PHP
categories: PHP
---

> PHP is a popular general-purpose scripting language that is especially suited to web development.

<!-- more -->

# PHP基础
## PHP简介

PHP（全称：PHP：Hypertext Preprocessor，即"PHP：超文本预处理器"）是一种通用开源脚本语言。
PHP 代码在服务器上执行，结果以纯 HTML 形式返回给浏览器。

- [菜鸟教程](https://www.runoob.com/php/php-tutorial.html)
- https://www.php.net/

### PHP能做什么？
- PHP 可以生成动态页面内容
- PHP 可以收集表单数据
- PHP 可以添加、删除、修改您的数据库中的数据

## PHP语法
PHP 脚本以 <?php 开始，以 ?> 结束。
PHP 中的每个代码行都必须以分号结束。
```
<?php
echo "Hello World!";
?>
```
## PHP语法
1. 定义在函数外部的就是全局变量，它的作用域从定义处一直到文件结尾。
2. 函数内定义的变量就是局部变量，它的作用域为函数定义范围内。
3. 函数之间存在作用域互不影响。
4. 函数内访问全局变量需要 `global` 关键字或者使用 `$GLOBALS[index]` 数组
5. `static` 关键字使某个局部变量不被删除。

```
<?php
$x=5;
$y=10;
 
function myTest() {
    global $x,$y;
    $y=$x+$y;
}
 
myTest();
echo $y; // 输出 15
?>
```

## echo 和 print 语句
## EOF(heredoc) 使用说明
PHP 定界符`EOF` 中是会解析 html 格式内容的，并且在双引号内的内容也有转义效果。
```
<?php
$name="runoob";
$a= <<<EOF
		<h1>EOF</h1>
        "abc"$name
        "123"
EOF;
// 结束需要独立一行且前后不能空格
echo $a;
?>
```
## 数据类型
`var_dump()` 函数返回变量的数据类型和值
### 对象
```
<?php
$cars=array("Volvo","BMW","Toyota"); // 数组
class Car {
  var $color;
  function __construct($color="green") {
    $this->color = $color;
  }
  function what_color() {
    return $this->color;
  }
}
?>
```
## 类型比较
- 松散比较：使用两个等号 == 比较，只比较值，不比较类型。
- 严格比较：用三个等号 === 比较，除了比较值，也比较类型。

## 常量
常量值被定义后，在脚本的其他任何地方都不能被改变。
bool define ( string $name , mixed $value [, bool $case_insensitive = false ] )
```
<?php
// true 不区分大小写的常量名
define("GREETING", "欢迎", true);
echo greeting;  // 输出 "欢迎"
?>
```

## 字符串变量
**并置运算符 **(.) 用于把两个字符串值连接起来。
```
<?php
$txt1="Hello world!";
$txt2="What a nice day!";
echo $txt1 . " " . $txt2;
?>
```

strlen() 函数返回字符串的长度（字节数）。

strpos() 函数用于在字符串内查找一个字符或一段指定的文本。
`echo strpos("Hello world!","world");`

## 运算符
运算符优先级中，or 和 ||，&& 和 and 都是逻辑运算符，效果一样，但是其优先级却不一样。
```
<?php
// 优先级： &&  >  =  >  and
// 优先级： ||  >  =  >  or
 
$a = 3;
$b = false;
$c = $a or $b;
var_dump($c);          // 这里的 $c 为 int 值3，而不是 boolean 值 true
$d = $a || $b;
var_dump($d);          //这里的 $d 就是 boolean 值 true 
?>
```
## If...Else
## Switch 
## 数组
```
<?php
$cars=array("Volvo","BMW","Toyota");
echo "I like " . $cars[0] . ", " . $cars[1] . " and " . $cars[2] . ".<br>";
echo count($cars);	// 数组长度

// 关联数组
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
echo "<br>Peter is " . $age['Peter'] . " years old.";
?>
```

## 数组排序
sort() - 对数组进行升序排列
rsort() - 对数组进行降序排列
asort() - 根据关联数组的值，对数组进行升序排列
ksort() - 根据关联数组的键，对数组进行升序排列

## 超级全局变量
超级全局变量在PHP 4.1.0之后被启用, 是PHP系统中自带的变量，在一个脚本的全部作用域中都可用。
`$GLOBALS` 是PHP的一个超级全局变量组，在一个PHP脚本的全部作用域中都可以访问。
$_SERVER 是一个包含了诸如头信息(header)、路径(path)、以及脚本位置(script locations)等等信息的数组。

### $_REQUEST
`$_REQUEST` 用于收集HTML表单提交的数据。
当用户通过点击 "Submit" 按钮提交表单数据时, 表单数据将发送至<form>标签中 action 属性中指定的脚本文件。
```
<html>
<body>

<!-- $_SERVER['PHP_SELF'] 获取 当前执行脚本的文件名 -->
<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>"> 
Name: <input type="text" name="fname">
<input type="submit">
</form>
 
<?php 
$name = $_REQUEST['fname']; 
echo $name; 
?>
 
</body>
</html>
```

`$_POST`、`$_GET`同样被广泛应用于收集表单数据。


## While 循环

## For 循环

### foreach 循环
冒泡排序
```
<?php
	$arr = array(9,8,7,6,5,4,3,2,1);
	for ($i=count($arr)-1; $i>=0; $i--) {
		for ($j= 0; $j<$i; $j++) {
			if($arr[$j] > $arr[$j+1]) {
				$temp = $arr[$j];
				$arr[$j] = $arr[$j+1];
				$arr[$j+1] = $temp;
			}
		}
	}
	print_r($arr[4]);
```

## 函数
```
<?php
function add($x, $y) {
	return $x + $y;
}
echo '14 + 12 = ' . add(14, 12);	
```

## 魔法常量
```
<?php
echo '该文件位于 " '  . __FILE__ . ' " <br>';
class test {
    function _print() {
        echo '类名为：'  . __CLASS__ . "<br>";
        echo '函数名为：' . __FUNCTION__ ;
    }
}
$t = new test();
$t->_print();
?>
```

## 命名空间(namespace)
PHP 命名空间可以解决以下两类问题：
- 用户编写的代码与PHP内部的类/函数/常量或第三方类/函数/常量之间的名字冲突。
- 为很长的标识符名称(通常是为了缓解第一类问题而定义的)创建一个别名（或简短）的名称，提高源代码的可读性。

## 面向对象

# PHP表单

## 表单验证
`<form method="post" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">`
`$_SERVER["PHP_SELF"]`是超级全局变量，返回当前正在执行脚本的文件名，与 document root相关。所以，` $_SERVER["PHP_SELF"]` 会发送表单数据到当前页面，而不是跳转到不同的页面。
htmlspecialchars() 函数把一些预定义的字符转换为 HTML 实体。
预定义的字符是：
- & （和号） 成为 &amp;
- " （双引号） 成为 &quot;
- ' （单引号） 成为 &#039;
- < （小于） 成为 &lt;
- \> （大于） 成为 &gt;

`$_SERVER["PHP_SELF"]` 变量有可能会被黑客使用！可以通过 htmlspecialchars() 函数来避免被利用。

```
<?php
// 定义变量并默认设置为空值
$name = $email = $gender = $comment = $website = "";
// 通过$_SERVER["REQUEST_METHOD"]来检测表单是否被提交
if ($_SERVER["REQUEST_METHOD"] == "POST")
{
   $name = test_input($_POST["name"]);
   $gender = test_input($_POST["gender"]);
}

function test_input($data)
{
   $data = trim($data);  // 去除用户输入数据中不必要的字符 (如：空格，tab，换行)。
   $data = stripslashes($data);  // 去除用户输入数据中的反斜杠 (\)
   $data = htmlspecialchars($data);  // 把一些预定义的字符转换为 HTML 实体。
   return $data;
}
?>
```

## 必须字段
```
<?php
// 定义变量并默认设为空值
$nameErr = $name = "";
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  if (empty($_POST["name"])) {
    $nameErr = "名字是必需的。";
  } else {
    $name = test_input($_POST["name"]);
  }
}
?>
<form method="post" action="<?php echo htmlspecialchars($_SERVER['PHP_SELF']);?>"> 
   名字: <input type="text" name="name">
   <span class="error">* <?php echo $nameErr;?></span>
   <input type="submit" name="submit" value="Submit"> 
</form>
```
## 验证邮件和URL
```
if (empty($_POST["name"])) {
  $nameErr = "Name is required";
  } else {
	 $name = test_input($_POST["name"]);
	 // 检测名字是否只包含字母跟空格
	 if (!preg_match("/^[a-zA-Z ]*$/",$name)) {
	 $nameErr = "只允许字母和空格"; 
	 }
 }
```


## $\_GET 变量
预定义的` $_GET` 变量用于收集来自 `method="get"`的表单中的值。

从带有 GET 方法的表单发送的信息，对任何人都是可见的（会显示在浏览器的地址栏），并且对发送信息的量也有限制。

## $\_POST 变量
预定义的 `$_POST` 变量用于收集来自 `method="post"`的表单中的值。

从带有 POST 方法的表单发送的信息，对任何人都是不可见的（不会显示在浏览器的地址栏），并且对发送信息的量也没有限制。

# PHP高级教程

## 多维数组
```
$sites = array
(
    array("Volvo",100,96),
    "taobao"=>array
    (
        "淘宝",
        "http://www.taobao.com"
    )
);
```
## date() 函数
```
<?php
date_default_timezone_set('PRC'); 
echo date("Y/m/d") . "<br>";
echo date("Y.m.d") . "<br>";
echo date("Y-m-d H:i:s");
?>
```

## 包含文件
include 和 require 语句用于在执行流中插入写在其他文件中的有用的代码。
处理错误方式不同：
- require 生成一个致命错误（E_COMPILE_ERROR），在错误发生后脚本会停止执行。
- include 生成一个警告（E_WARNING），在错误发生后脚本会继续执行。
`<?php include 'header.php'; ?>`

## 文件处理
fopen()、fclose()、feof()

## 文件上传
允许用户上传文件是一个巨大的安全风险。请仅仅允许可信的用户执行文件上传操作。
https://www.cnblogs.com/54chensongxia/p/11662252.html#2409458956
### 上传限制
用户只能上传 .gif、.jpeg、.jpg、.png 文件，文件大小必须小于 200 kB
### 保存被上传的文件

```
<?php
// 允许上传的图片后缀
$allowedExts = array("gif", "jpeg", "jpg", "png");
$temp = explode(".", $_FILES["file"]["name"]);
echo $_FILES["file"]["size"];
$extension = end($temp);     // 获取文件后缀名
if ((($_FILES["file"]["type"] == "image/gif")
|| ($_FILES["file"]["type"] == "image/jpeg")
|| ($_FILES["file"]["type"] == "image/jpg")
|| ($_FILES["file"]["type"] == "image/pjpeg")
|| ($_FILES["file"]["type"] == "image/x-png")
|| ($_FILES["file"]["type"] == "image/png"))
&& ($_FILES["file"]["size"] < 204800)   // 小于 200 kb
&& in_array($extension, $allowedExts))
{
    if ($_FILES["file"]["error"] > 0)
    {
        echo "错误：: " . $_FILES["file"]["error"] . "<br>";
    }
    else
    {
        echo "上传文件名: " . $_FILES["file"]["name"] . "<br>";
        echo "文件类型: " . $_FILES["file"]["type"] . "<br>";
        echo "文件大小: " . ($_FILES["file"]["size"] / 1024) . " kB<br>";
        echo "文件临时存储的位置: " . $_FILES["file"]["tmp_name"] . "<br>";
        
        // 判断当期目录下的 upload 目录是否存在该文件
        // 如果没有 upload 目录，你需要创建它，upload 目录权限为 777
        if (file_exists("upload/" . $_FILES["file"]["name"]))
        {
            echo $_FILES["file"]["name"] . " 文件已经存在。 ";
        }
        else
        {
            // 如果 upload 目录不存在该文件则将文件上传到 upload 目录下
            move_uploaded_file($_FILES["file"]["tmp_name"], "upload/" . $_FILES["file"]["name"]);
            echo "文件存储在: " . "upload/" . $_FILES["file"]["name"];
        }
    }
}
else
{
    echo "非法的文件格式";
}
?>
```
## Cookie
cookie 常用于**识别用户**。cookie 是一种服务器留在用户计算机上的小文件。每当同一台计算机通过浏览器请求页面时，这台计算机将会发送 cookie。通过 PHP，您能够创建并取回 cookie 的值。

## Session
session 变量用于存储关于用户会话（session）的信息，或者更改用户会话（session）的设置。Session 变量存储单一用户的信息，并且对于应用程序中的所有页面都是可用的。

## Email
PHP 允许您从脚本直接发送电子邮件。
## 错误处理
在 PHP 中，默认的错误处理很简单。一条错误消息会被发送到浏览器，这条消息带有文件名、行号以及描述错误的消息。
```
<?php
if(!file_exists("welcome.txt")) {
    die("文件不存在");
} else {
    $file=fopen("welcome.txt","r");
}
?>
```

## 异常处理
异常用于在指定的错误发生时改变脚本的正常流程。

## 过滤器
PHP 过滤器用于验证和过滤来自非安全来源的数据，比如用户的输入。

## JSON
json_encode: 对变量进行 JSON 编码
json_decode: 对 JSON 格式的字符串进行解码，转换为 PHP 变量

# PHP数据库

## MySQL简介
MySQL 是一种在 Web、服务器 上使用的数据库系统。

## 连接MySQL
### 实例 (MySQLi - 面向对象)
```php
<?php
$servername = "localhost";
$username = "username";
$password = "password";
 
// 创建连接
$conn = new mysqli($servername, $username, $password);
 
// 检测连接
if ($conn->connect_error) {
    die("连接失败: " . $conn->connect_error);
} 
echo "连接成功";
?>
```

## 创建数据库
```php
// 创建数据库
$sql = "CREATE DATABASE myDB";
if ($conn->query($sql) === TRUE) {
    echo "数据库创建成功";
} else {
    echo "Error creating database: " . $conn->error;
}
 
$conn->close();
```

## 创建数据表
```php
// 使用 sql 创建数据表
$sql = "CREATE TABLE MyGuests (
id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY, 
firstname VARCHAR(30) NOT NULL,
lastname VARCHAR(30) NOT NULL,
email VARCHAR(50),
reg_date TIMESTAMP
)";
 
if ($conn->query($sql) === TRUE) {
    echo "Table MyGuests created successfully";
} else {
    echo "创建数据表错误: " . $conn->error;
}
 
$conn->close();
```

## 数据预处理
预处理语句对于防止 MySQL 注入是非常有用的。
预处理语句用于执行多个相同的 SQL 语句，并且执行效率更高。
```php
<?php
$servername = "localhost";
$username = "username";
$password = "password";
$dbname = "myDB";
 
// 创建连接
$conn = new mysqli($servername, $username, $password, $dbname);
 
// 检测连接
if ($conn->connect_error) {
    die("连接失败: " . $conn->connect_error);
}
 
// 预处理及绑定
$stmt = $conn->prepare("INSERT INTO MyGuests (firstname, lastname, email) VALUES (?, ?, ?)");
$stmt->bind_param("sss", $firstname, $lastname, $email);
 
// 设置参数并执行
$firstname = "John";
$lastname = "Doe";
$email = "john@example.com";
$stmt->execute();
 
$firstname = "Julie";
$lastname = "Dooley";
$email = "julie@example.com";
$stmt->execute();
 
echo "新记录插入成功";
 
$stmt->close();
$conn->close();
?>
```
`$stmt->bind_param("sss", $firstname, $lastname, $email);`
bind_param函数绑定了 SQL 的参数，且告诉数据库参数的值。 "sss" 参数列处理其余参数的数据类型。s 字符告诉数据库该参数为字符串。

参数有以下四种类型:

i - integer（整型）
d - double（双精度浮点型）
s - string（字符串）
b - BLOB（binary large object:二进制大对象）
每个参数都需要指定类型。通过告诉数据库参数的数据类型，可以降低 SQL 注入的风险。

## 读取数据
```php
<?php
$servername = "localhost";
$username = "username";
$password = "password";
$dbname = "myDB";
 
// 创建连接
$conn = new mysqli($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error) {
    die("连接失败: " . $conn->connect_error);
} 
 
$sql = "SELECT id, firstname, lastname FROM MyGuests";
$result = $conn->query($sql);
 
if ($result->num_rows > 0) {
    // 输出数据
    while($row = $result->fetch_assoc()) {
        echo "id: " . $row["id"]. " - Name: " . $row["firstname"]. " " . $row["lastname"]. "<br>";
    }
} else {
    echo "0 结果";
}
$conn->close();
?>
```