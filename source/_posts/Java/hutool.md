---
title: Hutool
date: 2021-09-30 09:55:46
tags:
categories: Java
---

<meta name="referrer" content="no-referrer"/>
Hutool是一个小而全的Java工具类库，通过静态方法封装，降低相关API的学习成本，提高工作效率，使Java拥有函数式语言般的优雅，让Java语言也可以“甜甜的”。

<!-- more -->

# Hutool
> A set of tools that keep Java sweet.

Hutool是一个Java工具包类库，对文件、流、加密解密、转码、正则、线程、XML等JDK方法进行封装，组成各种Util工具类。

- [官网](https://www.hutool.cn/)
- [API](https://apidoc.gitee.com/dromara/hutool/)


## Validator

字段验证器（验证器），分两种类型的验证：

- isXXX：通过返回boolean值判断是否满足给定格式。
- validateXXX：通过抛出异常ValidateException检查是否满足给定格式。

主要验证字段非空、是否为满足指定格式等（如是否为Email、电话等）

| 方法                            |                          描述                           |
| ------------------------------- | :-----------------------------------------------------: |
| isCitizenId(CharSequence value) |  验证是否为身份证号码（支持18位、15位和港澳台的10位）   |
| isEmail(CharSequence value)     |                 验证是否为可用邮箱地址                  |
| isEmpty(Object value)           | 验证是否为空，对于String类型判定是否为empty(null 或 "") |
| isMobile(CharSequence value)    |               验证是否为手机号码（中国）                |

## PhoneUtil

电话号码工具类，包括：

- 手机号码
- 400、800号码
- 座机号码

| 方法                         | 描述                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| isMobile(CharSequence value) | 验证是否为手机号码（中国）                                   |
| isPhone(CharSequence value)  | 验证是否为座机号码+手机号码（CharUtil中国）+ 400 + 800电话 + 手机号号码（香港） |

## RSA

RSA公钥/私钥/签名加密解密

罗纳德·李维斯特（Ron [R]ivest）、阿迪·萨莫尔（Adi [S]hamir）和伦纳德·阿德曼（Leonard [A]dleman）

由于非对称加密速度极其缓慢，一般文件不使用它来加密而是使用对称加密，
非对称加密算法可以用来对对称加密的密钥加密，这样保证密钥的安全也就保证了数据的安全

| 方法 | 描述 |
| ---- | -------------------------------------------- |
| decrypt(byte[] bytes, KeyType keyType) | 解密 |
| encrypt(byte[] data, KeyType keyType) | 加密  |

byte[]转String，通过构造方法String(byte bytes[])