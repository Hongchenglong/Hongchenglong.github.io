---
title: PHP基础
date: 2020-03-15 9:0:0
tags: PHP
categories: PHP
---
学习[菜鸟教程](https://www.runoob.com/php/php-tutorial.html)所做的PHP基础笔记。
<!-- more -->

## PHP简介

PHP（全称：PHP：Hypertext Preprocessor，即"PHP：超文本预处理器"）是一种通用开源脚本语言。
PHP 代码在服务器上执行，结果以纯 HTML 形式返回给浏览器。
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
