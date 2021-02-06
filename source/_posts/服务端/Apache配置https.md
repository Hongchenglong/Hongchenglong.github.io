---
title: Apache配置https
date: 2021-01-19 19:32:07
tags: [HTTPS]
---

<meta name="referrer" content="no-referrer"/>

<!-- more -->

# 申请免费DV证书

[阿里云官方文档](https://help.aliyun.com/document_detail/156645.html?spm=a2c4g.11186623.6.606.39605b2eT9S1Na)
## 申请SSL证书
1. 访问[证书资源包](https://common-buy.aliyun.com/?spm=a2c4g.11186623.2.8.53e14802HoOdmn&commodityCode=cas_dv_public_cn&request={"ord_time":"1:Year","order_num":1,"product":"free_product","certCount":"20"})购买页，领取阿里云免费DV证书。

2. 申请免费版SSL证书。


## 下载证书并上传服务器
![](https://img2020.cnblogs.com/blog/1677222/202101/1677222-20210119194324937-2131771008.png)
重命名文件chain.crt --> ca.crt, public.crt --> server.key
通过XShell上传至服务器，并放在`/usr/local/apache2/conf/key`下
```shell
[root@ECS key]# pwd
/usr/local/apache2/conf/key
[root@ECS key]# ls
ca.crt  server.crt  server.key
```


# 在Apache服务器上安装SSL证书
[阿里云官方文档](https://help.aliyun.com/document_detail/98727.html?spm=a2c4g.11186623.6.636.53e14802HoOdmn)
## 配置httpd.conf
`# vim /usr/local/apache2/conf/httpd.conf`

```
LoadModule ssl_module modules/mod_ssl.so
Include conf/extra/httpd-ssl.conf
#Include conf/extra/httpd-ahssl.conf
```
## 配置httpd-ssl.conf
`# vim /usr/local/apache2/conf/extra/httpd-ssl.conf`

```
<VirtualHost _default_:443>
DocumentRoot "/usr/local/apache2/htdocs"
ServerName www.oeong.com:443 # 域名
ServerAdmin oeong@foxmail.com # 邮箱
ErrorLog "/usr/local/apache2/logs/error_log"
TransferLog "/usr/local/apache2/logs/access_log"

SSLCertificateFile "/usr/local/apache2/conf/key/server.crt"
SSLCertificateKeyFile "/usr/local/apache2/conf/key/server.key"
SSLCertificateChainFile "/usr/local/apache2/conf/key/ca.crt"

SSLEngine on
```

## 重启Apache
`[root@ECS conf]# /usr/local/apache2/bin/apachectl restart`
