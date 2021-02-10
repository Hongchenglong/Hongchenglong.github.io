---
title: JavaWeb
tags:
---

# IDEA

psvm

sout

"hello".out

ALT+INSERT  生成代码(如GET,SET方法,构造函数等) 

ctrl+o 重写方法

alt+enter 导入包，自动修正

# HTTP协议

请求行、请求头、请求体



**请求头**

Referer：请求从哪来

**响应头**

Location

Refresh `<meta http-equiv='refresh' content='3'>`

# Tomcat

请求：客户端发送数据给服务端

响应：服务端返回数据给客户端

Socket通信

tomcat 性能稳定、免费的Web服务器

# Servlet

```
@WebServlet("/s01")
```



# HttpServletRequest

```
String uname = req.getParameter("uname");
```

## 请求乱码

get请求    不会乱码

post请求   无论什么版本的tomcat，都会乱码 
```
request.setCharacterEncoding("UTF-8");
response.setContentType("text/html; charset=UTF-8");
```

`
String name = new String(req.getParameter("uname").getBytes("ISO-8859-1"), "UTF-8");` 

## 请求转发

`req.getRequestDispatcher(url).forward(req, resp);`
让请求从服务端跳转到客服端（或指定servlet）
特点：

1. 服务端行为
2. 地址栏不发生改变
3. 从始至终1个请求
4. request数据共享

## request作用域



# HttpServletResponce

乱码解决：
`resp.setContentType("text/html; charset=utf-8");`



重定向与请求转发区别

|             | 重定向     | 请求转发     |
| ----------- | ---------- | ------------ |
| 地址栏      | 变         | 不变         |
| 请求        | 2次        | 1次          |
| request对象 | 不共享     | 共享         |
| 行为        | 客户端行为 | 服务端行为   |
| 地址        | 任何地址   | 当前项目资源 |

# Cookie

cookie是浏览器的技术，与服务器无关，数据存在本地，

如记住密码，通过cookie实现

```java
Cookie cookie = new Cookie("uname1", "zhangsan");
cookie.setMaxAge(-1);
resp.addCookie(cookie);
```

到期时间：负整数，关闭浏览器失效
到期时间：正整数，存活在磁盘的时间
到期时间：0，删除



注意点：

1. 只在当前浏览器有效
2. 中文问题
3. 同名覆盖
4. 数量有限



访问路径`cookie1.setPath("/");`

只有访问的路径中包含Cookie对象的path值，才可以获取到cookie对象

# HttpSession

session标识一次会话，底层依赖cookie



当获取session对象是，判断是否存在，不存在则创建

JSESSIONID



默认30min，30min内无操作失效

# ServletContext

Servlet域对象：

request：一次请求，请求转发有效，重定向失效

session：一次会话，session销毁后失效

ServletContext：整个应用程序，服务器重启失效

# 文件上传和下载

设置表单类型 上传表单 enctype="multipart/form-data"

`@MultipartConfig` // 文件上传，必须设置该注解

button 默认 type="submit"
设置表单name，否则后台无法接收数据



超链接下载
`<a href="download/4star.png" download>图片文件</a>`



`action="ds"` 对应 `@WebServlet("/ds")`