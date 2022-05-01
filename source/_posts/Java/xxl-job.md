---
title: XXL-JOB
date: 2022-05-01 11:37:36
tags:
categories: Java
---

<meta name="referrer" content="no-referrer"/>
XXL-JOB是一个分布式任务调度平台。有2个角色，xxl-job-admin调度中心和xxl-job-executor执行器。调度中心统一管理调度任务，不承担业务逻辑，负责发起调度请求。执行器是我们的业务系统，负责接收调度请求并执行对应的JobHandler中的业务逻辑。

<!-- more -->

## 1. 基本概念

### 1.1 定时任务是什么？

定时任务是在约定时间内执行的一段程序。

- 批量处理数据：批量统计上个月的某个数据。
- 时间驱动的场景：某个时间点发送短信、邮件。
- 固定频率的场景：每隔5分钟需要执行一次。

### 1.2 用cron表示时间

cron表达式是一个字符串，以 5 或 6 个空格隔开，分为 6 或 7 个域，每一个域代表一个含义。

```
[秒] [分] [时] [日期] [月] [星期]
[秒] [分] [时] [日期] [月] [星期] [年]
*：表示任何时间触发任务
,：表示指定的时间触发任务
-：表示一段时间内触发任务
/：表示从哪一个时刻开始，每隔多长时间触发一次任务。
?：表示用于月中的天和周中的天两个子表达式，表示不指定值。
```

如：`0 30 8 * * ?`表示每天早上8点半

- crontab在线工具：https://tool.lu/crontab/

- cron表达式详解：https://tech.antfin.com/docs/2/62247

### 1.3 基于`Spring Task`实现定时任务

- 优点：
  - 不需要依赖外部框架。
  - 简单快速实现任务。`@EnableScheduling`、`@Scheduled` 注解
- 缺点：
  - 无法管理任务。要停止某个任务，必须重新发布。
  - 不支持动态调整。修改任务参数需要重启项目。
  - 不支持集群方式部署。集群模式下会出现**任务多次被调度执行**的情况，因为集群的节点之间是不会共享任务信息的，每个节点上的任务都会按时执行。
  
  > 单体，即一个项目部署在一台服务器上；
  >
  > 集群，即将单体复制多份部署在多台服务器，其中每个单体被称为一个节点。

## 2. XXL-JOB

XXL-JOB是一个**分布式任务调度平台**（XXL是作者徐雪里姓名拼音的首字母），其核心设计目标是开发迅速、学习简单、轻量级、易扩展。

源码仓库地址：https://github.com/xuxueli/xxl-job

源码结构：

![image-20220418165151470](http://cdn.oeong.com/niu20220429111202.png)

### 2.1 系统架构
在xxl-job中，有2个角色：

- xxl-job-admin调度中心
  统一管理任务调度平台上的调度任务，负责触发调度执行，并且提供任务管理平台。
  
- xxl-job-executor执行器
  执行器通常是我们的业务系统，如示例中的springboot项目。

#### 2.1.1 设计思想

将调度行为抽象形成“调度中心”公共平台，而平台自身并不承担业务逻辑，“调度中心”负责发起调度请求。

将任务抽象成分散的JobHandler，交由“执行器”统一管理，“执行器”负责接收调度请求并执行对应的JobHandler中业务逻辑。

因此，“调度”和“任务”两部分可以相互解耦，提高系统整体稳定性和扩展性。

#### 2.1.2 架构图

![img](http://cdn.oeong.com/niu20220422070956.png)

xxl-job就是一个中心化管理系统，系统主要通过MySQL管理各种定时任务信息，当到了定时任务的触发时间，就把任务信息从数据库中拉进内存，对任务执行器发起调度请求。

### 2.2 快速入门
整个调度任务执行流程如下：

- 启动xxl-job-admin工程。若无定制化开发，直接启动即可。
- 在xxl-job-excutor中需要引入xxl-job-core依赖，实现excutor的业务代码，配置xxl-job-admin的地址，主动向Xxl-job-admin注册，并建立netty连接。

#### 2.2.1 配置调度中心

1. 初始化数据库

`/xxl-job/doc/db/tables_xxl_job.sql`

| 表名               | 作用                                                         |
| ------------------ | ------------------------------------------------------------ |
| xxl_job_group      | 执行器信息表：维护任务执行器信息                             |
| xxl_job_info       | 调度扩展信息表：用于保存xxl-job调度任务的扩展信息，如任务分组、任务名、机器地址、执行器、执行入参和报警邮件等等 |
| xxl_job_lock       | 任务调度锁表                                                 |
| xxl_job_log        | 调度日志表：用于保存xxl-job调度任务的历史信息，如调度结果、执行结果、调度入参、调度机器和执行器等等 |
| xxl_job_log_report | 调度日志报表：用户存储xxl-job任务调度日志的报表，调度中心报表功能页面会用到 |
| xxl_job_logglue    | 任务GLUE日志：用于保存GLUE更新历史，用于支持GLUE的版本回溯功能 |
| xxl_job_registry   | 执行器注册表：维护在线的执行器和调度中心机器地址信息         |
| xxl_job_user       | 系统用户表                                                   |

> 调度中心支持集群部署，集群情况下各节点务必连接同一个mysql实例；如果mysql做主从，调度中心集群节点务必强制走主库。

2. 配置application文件

`/xxl-job/xxl-job-admin/src/main/resources/application.properties`

- 调度中心1

```properties
### web
server.port=8080
server.servlet.context-path=/xxl-job-admin

### xxl-job, datasource
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/xxl_job?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&serverTimezone=Asia/Shanghai
spring.datasource.username=
spring.datasource.password=
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

### xxl-job, email
spring.mail.host=smtp.qq.com
spring.mail.port=25
spring.mail.username=
spring.mail.from=
spring.mail.password=
```

- 调度中心2

```properties
### web
server.port=8180
server.servlet.context-path=/xxl-job-admin

### xxl-job, datasource
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/xxl_job?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&serverTimezone=Asia/Shanghai
spring.datasource.username=
spring.datasource.password=
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

### xxl-job, email
spring.mail.host=smtp.qq.com
spring.mail.port=25
spring.mail.username=
spring.mail.from=
spring.mail.password=
```

3. 启动

修改之后，启动`XxlJobAdminApplication`的main函数。
在浏览器上访问http://localhost:8081/xxl-job-admin/ ，初始登陆用户名为admin，密码为123456（在初始化数据时导入xxl_job_user）。

![image-20220428104655332](http://cdn.oeong.com/niu20220428105059.png)

4. 调度中心集群：

   调度中心支持集群部署，提升调度系统容灾和可用性。

   调度中心集群部署时，几点要求和建议：

   - **DB配置保持一致**；
   - **集群机器时钟保持一致**；
   - 建议：**推荐通过Nginx为调度中心集群做负载均衡**，分配域名。调度中心访问、执行器回调配置、调用API服务等操作均通过该域名进行。

#### 2.2.2 配置执行器项目

xxl-job-excutor是任务的执行单元，需要在业务系统中实现。

1. 在工程的pom.xml文件中引入xxl-job-core的依赖

```xml
<dependency>
    <groupId>com.xuxueli</groupId>
    <artifactId>xxl-job-core</artifactId>
    <version>2.3.0</version>
</dependency>
```

2. 配置application文件

web和执行器端口号不同，调度中心地址addresses和执行器应用名appname保持一致

- 执行器1

```properties
# web port
server.port=8081

### xxl-job admin address list, such as "http://address" or "http://address01,http://address02"
xxl.job.admin.addresses=http://127.0.0.1:8080/xxl-job-admin,http://127.0.0.1:8180/xxl-job-admin

### xxl-job executor appname
xxl.job.executor.appname=xxl-job-executor-sample

### xxl-job executor server-info
xxl.job.executor.ip=
xxl.job.executor.port=9999
```

- 执行器2

```properties
# web port
server.port=8181

### xxl-job admin address list, such as "http://address" or "http://address01,http://address02"
xxl.job.admin.addresses=http://127.0.0.1:8080/xxl-job-admin,http://127.0.0.1:8180/xxl-job-admin

### xxl-job executor appname
xxl.job.executor.appname=xxl-job-executor-sample

### xxl-job executor server-info
xxl.job.executor.ip=
xxl.job.executor.port=9998
```
3. 在`XxljobConfig`中初始化一个XxlJobSpringExecutor，该类用于处理xxl-job-admin和xxl-job-excutor之间的通讯以及任务的处理。

```java
@Configuration
public class XxlJobConfig {
    @Bean
    public XxlJobSpringExecutor xxlJobExecutor() {
        logger.info(">>>>>>>>>>> xxl-job config init.");
        XxlJobSpringExecutor xxlJobSpringExecutor = new XxlJobSpringExecutor();
        xxlJobSpringExecutor.setAdminAddresses(adminAddresses);
        xxlJobSpringExecutor.setAppname(appname);
        xxlJobSpringExecutor.setAddress(address);
        xxlJobSpringExecutor.setIp(ip);
        xxlJobSpringExecutor.setPort(port);
        xxlJobSpringExecutor.setAccessToken(accessToken);
        xxlJobSpringExecutor.setLogPath(logPath);
        xxlJobSpringExecutor.setLogRetentionDays(logRetentionDays);

        return xxlJobSpringExecutor;
    }
}
```

4. 注册一个任务，任务名为demoJobHandler。

```java
@Component
public class SampleXxlJob {
    @XxlJob(value = "demoJobHandler", init = "", destroy = "")
    public void demoJobHandler() throws Exception {
        XxlJobHelper.log("XXL-JOB, Hello World.");

        for (int i = 0; i < 10; i++) {
            XxlJobHelper.log("beat at:" + i);
            TimeUnit.SECONDS.sleep(2);
        }
    }
}
```

5. 启动执行器，在调度中心的执行器管理查看

调度中心**自动注册**了应用名为`xxl-job-executor-sample`的执行器，有两个注册节点，分别是9998和9999。

![image-20220428112959321](http://cdn.oeong.com/niu20220428113000.png)

6. 在调度中心的任务管理中配置相应的任务。

<img src="http://cdn.oeong.com/niu20220428160815.png" alt="image-20220428160803219" style="zoom:60%;" />

运行模式：

- BEAN模式：支持基于类的开发方式，每个任务对应一个Java类。

- GLUE模式：任务以源码方式维护在调度中心，支持通过`Web IDE`在线更新，实时编译和生效，因此不需要指定JobHandler。

  <img src="http://cdn.oeong.com/niu20220428113912.png" alt="image-20220428113910692" style="zoom:75%;" />

路由策略：集群模式下某个任务选择由哪个执行器完成的策略。

<img src="http://cdn.oeong.com/niu20220428151844.png" alt="image-20220428151842499" style="zoom:60%;" />

7. 执行任务后，在调度中心可以查看调度日志。

![image-20220428152842346](http://cdn.oeong.com/niu20220428152843.png)

![](http://cdn.oeong.com/niu20220428152818.png)

查看两个临近的调度结果，可以发现任务是由两个执行器轮询执行的。

![image-20220428153208183](http://cdn.oeong.com/niu20220428153210.png)

![image-20220428153133536](http://cdn.oeong.com/niu20220428153134.png)

8. 执行器集群：

执行器支持集群部署，提升调度系统可用性，同时提升任务处理能力。

执行器集群部署时，几点要求和建议：

- 执行器**回调地址（xxl.job.admin.addresses）需要保持一致**；执行器根据该配置进行执行器自动注册等操作。 
- 同一个执行器集群内**AppName（xxl.job.executor.appname）需要保持一致**；调度中心根据该配置动态发现不同集群的在线执行器列表。

## 3. 总结
XXL-JOB是一个分布式任务调度平台。有2个角色，xxl-job-admin调度中心和xxl-job-executor执行器。调度中心统一管理调度任务，不承担业务逻辑，负责发起调度请求。执行器是我们的业务系统，负责接收调度请求并执行对应的JobHandler中的业务逻辑。

特性：

1. 简单：有界面维护定时任务和触发规则，方便管理；

2. 动态：支持动态修改任务状态、启动/停止任务，以及终止运行中任务，即时生效；

3. 调度中心（中心式）：调度采用中心式设计，“调度中心”自研调度组件并**支持集群部署**，可保证调度中心；

4. 执行器（分布式）：任务分布式执行，任务”执行器”**支持集群部署**，可保证任务执行；

5. 邮件报警：任务失败时支持邮件报警，支持配置多邮件地址群发报警邮件。

6. Rolling实时日志：支持**在线查看**调度结果，并且支持以Rolling方式实时查看执行器输出的完整的执行日志；

   

