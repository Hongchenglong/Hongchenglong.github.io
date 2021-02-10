---
title: JSP和JSTL
tags:
---

# JSP

JSP: Java Server Page

显式注释：能够在客户端查看的注释，继承HTML `<!-- -->`
隐式注释: `<%-- --%>`

Java脚本段`<% %>`



静态包含

`<%@include file=".jsp"%>`

直接替换，不可定义同名变量



动态包含 `<jsp:include page=""> </jsp:include>`

相对于调用方法、生成多个源码文件、可以定义同名变量、效率高


四大域对象

1. page：当前页面有效，跳转后无效
2. request：一次请求有效，服务端有效，客户端跳转失效
3. session：一次会话有效
4. application：整个应用有效

```
<jsp:forward page="06-get.jsp"></jsp:forward> // 服务端跳转
<a href="06-get.jsp">跳转</a> 				// 客户端跳转
```



# EL表达式

`${exp}`

操作域对象，不能操作局部变量

取值从小到大



List、Map、JavaBean



`${empty exp}`







# JavaScript

