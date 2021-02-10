---
title: Java面试宝典
date: 2021-02-09 13:11:16
tags:
categories:
---

<meta name="referrer" content="no-referrer"/>
<!-- more -->

# Java SE

## Java基础（一）

### Java和PHP的区别？

PHP专注于Web开发，在Web后台开发PHP优于Java；Java比较全面，在数据库访问方面强于PHP。

Java适合于开发大型的应用系统，应用的前景比较广阔，系统易维护、可复用性较好。

### 简单描述一下正则表达式及其用途。

在编写处理字符串的程序时，经常需要**查找符合某些复杂规则的字符串**。正则表达式就是用于描述这些规则的工具。

### Java中是如何支持正则表达式操作的？

Java中的`String`类提供了支持正则表达式操作的方法，包括：matches()、replaceAll()、replaceFirst()、split()。此外，Java中可以用`Pattern`类表示正则表达式对象，它提供了丰富的API进行各种正则表达式操作，如compile。

### 比较一下Java和JavaSciprt？

Java与JavaScript是两个公司开发的不同的两个产品。

- 面向对象和基于对象

Java是一种真正的面向对象的语言，即使是开发简单的程序，必须设计对象；

JavaScript是基于对象（Object-Based）和事件驱动（Event-Driven）的编程语言，用来制作与网络无关的，与用户交互作用的复杂软件。

- 编译和解释

Java的源代码在执行之前，必须经过编译；

JavaScript无需编译，由浏览器解释执行。

- 强类型和弱类型变量

Java采用强类型变量检查，即所有变量在编译之前必须作声明；

JavaScript中变量是弱类型的，甚至在使用变量前可以不作声明，在运行时检查推断其数据类型。

### Java中如何跳出当前的多重嵌套循环？

在最外层循环前加一个标记如A，然后用`break A`，可以跳出多重循环，类似goto。

### &和&&的区别？

&运算符有两种用法：(1)按位与；(2)逻辑与。

&&运算符是**短路与**运算。如果&&左边的表达式的值是false，右边的表达式会被直接短路掉，不会进行运算。

### int和Integer有什么区别？

Java是一个近乎纯洁的面向对象编程语言，但是==为了编程的方便还是引入了基本数据类型==，但是为了能够将这些基本数据类型当成==对象==操作，Java为每一个基本数据类型都引入了对应的==包装类型==（wrapper class），**int的包装类就是Integer**，从Java 5开始引入了自动装箱/拆箱机制，使得二者可以**相互转换**。

### 在web应用开发过程中经常遇到输出某种编码的字符，如iso8859-1等，请你讲讲如何输出一个某种编码的字符串？

`String str = new String("字符串".getBytes("ISO-8859-1"), "GBK");`

### 说明String和StringBuffer的区别
