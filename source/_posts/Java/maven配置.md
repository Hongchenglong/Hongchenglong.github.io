---
title: Maven配置
date: 2021-02-04 23:32:11
tags: [Maven]
categories: Java
---

<meta name="referrer" content="no-referrer"/>
<!-- more -->

## Maven是什么

- Maven 翻译为"专家"、"内行"，是 Apache 下的一个纯 Java 开发的开源项目。基于项目对象模型（缩写：POM）概念，Maven利用一个中央信息片断能管理一个项目的构建、报告和文档等步骤。
- Maven 是一个**项目管理工具**，可以对 Java 项目进行构建、依赖管理。

[Maven 环境配置](https://www.runoob.com/maven/maven-setup.html)



## 配置MAVEN_HOME报错

```
The JAVA_HOME environment variable is not defined correctly
This environment variable is needed to run this program
NB: JAVA_HOME should point to a JDK not a JRE
```


原因是我安装了两个jdk版本，并同时将路径写在JAVA_HOME中。于是分别为两个jdk设置JAVA_HOME。设置`JAVA_HOME = %JAVA_HOME8%`，当需要另一版本则切换为`JAVA_HOME = %JAVA_HOME15%`。

![image-20210204235019615](http://cdn.oeong.com/niu20210204235021.png)



学习博客：[同一个电脑安装两个jdk版本](https://blog.csdn.net/yuruixin_china/article/details/53607248?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.baidujs&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.baidujs)

