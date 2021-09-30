---
title: crontab定时任务
date: 2020-03-13 10:06:16
tags: Linux
categories: Linux
---

Linux的crond定时任务是周期性执行任务的守护进程。

<!-- more -->
1. 安装
    `yum -y install crontab`

2. 启动crond服务
    `service crond start`
    查看状态`service crond status`

3. 使用`crontab -e`进行定时任务的编辑
    格式: `分 时 日 月 周 [用户] command`
    这里我写入`0 * * * * /root/anaconda3/bin/python3 /root/*.py`, 表示每天每小时0分时自动执行`python3 /root/*.py`命令。
    注意: 设置好运行命令的**绝对路径**和被执行文件的**绝对路径**，因为crontab本身不具备平时运行的环境变量。

4. 使用`crontab -l`查看设置好的定时任务


