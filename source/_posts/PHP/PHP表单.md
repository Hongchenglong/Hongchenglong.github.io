---
title: PHP表单
date: 2020-03-15 19:0:0
tags: PHP
categories: PHP
---
学习[菜鸟教程](https://www.runoob.com/php/php-forms.html)所做的PHP表单笔记。
<!-- more -->
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