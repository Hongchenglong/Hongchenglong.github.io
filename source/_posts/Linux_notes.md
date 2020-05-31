---
title: Linux学习笔记
date: 2020-02-26 18:08:33
tags: Linux
categories: Linux
top: true
---
整理了一些Linux的常用知识，方便之后使用时查阅。

<!-- more -->

`[root@localhost ~]#`的含义
1. 用户名：root
2. 主机名：localhost
3. 当前路径：~当前用户的home目录
4. 权限标志位：#代表root，$代表普通用户

## vi操作
- 可以编辑文件 `vi <file>  `
- 插入内容 `p、P`
- 复制 `[n]yy`
- 删除行，删除词 `[n]dd、dw、x`
- 撤销 `u`
- 跳转某一行 `[n]G`
- 跳转行的开头`0`、末尾`$`
- 通过:/xxx进行搜索定位，n键查找下一项
`vi /etc/hostname` 改主机名
`:wq`   强制性写入文件并退出。即使文件没有被修改也强制写入，并更新文件的修改时间。
`:x`    写入文件并退出。仅当文件被修改时才写入，并更新文件修改时间，否则不会更新文件修改时间。

## 文件和目录
文件和文件夹的创建删除
`mkdir -p <dir/subdir>`  创建多级目录
`rm -r <file>`   删除多级文件
`mv <old> <new>`  移动和文件更名
`pwd ` 查看当前绝对路径
`cp <file> <file>.bak`  复制、备份文件

## 常用操作
cat，more，less，grep，wc –l
cd - 返回上一次目录
more 命令类似 cat ，不过会以一页一页的形式显示，更方便使用者逐页阅读



文件的打包和解压： tar cvfz以及对应的tar xvfz 
c ：创建一个新归档；x ： 从归档中抽取文件。
v ：显示文件的归档进度；z ：使用 gzip 来压缩 tar 文件。
f ：当与 -c 选项一起使用时，创建的 tar 文件使用该选项指定的文件名；当与 -x 选项
一起使用时，则解除该选项指定的归档。
```
$ tar cvfz share.tar.gz /usr/local/share/
$ tar xvfz share.tar.gz -C ./tmp
```
打包指的是将多个文件和目录集中存储在一个文件中；
而压缩则指的是利用算法对文件进行处理，从而达到缩减占用磁盘空间的目的。

```
echo  // 用于字符串的输出
ls -l f*  // 查看虚拟机上以f开头的设备文件
find <dir> -name <文件名> 2>/dev/null  // 查找文件
grep <查找内容> <文件名>  // 搜索文件内容
find . | grep passwd
ls | grep *.txt
tail -n <file>	// 查看某一文件后n行
```

创建软链接 
`ln -s <source> <target>` 
如`ln -s /root/htdocs/cqcq/application/index/controller/ ~/controller`
注意，删除软链接用`rm -rf ~/controller`，而不是`rm -rf ~/controller/`

### 安装命令
Ubuntu用`apt-get`，Centos用`yum`。
加上`-y`遇到询问时自动yes。

## 重定向和管道

重定向的符号有两个：>或>>。
两者的区别是：
前者会先清空文件，然后再写入内容；
后者会将重定向的内容追加到现有文件的尾部。

能够将任意命令的运行结果重定向到文件中。例如`ls –l > tmp.txt`

**管道**：
- 把一个程序的输出直接连接到另一个程序的输入。
- 通过管道将两个命令拼接起来。

最典型的比如` ls –l | wc –l `计算数量。
`cat <file> | wc -l`统计file的行数，file的内容输出连接到wc -l的输入。

## 用户管理
创建用户，修改用户密码
```
sudo adduser <newuser>     
sudo passwd <newuser>
```
su — Switch User
切换到指定用户，并且在该用户的家目录中创建文件，再退出这个用户。
```
su newuser 
touch <file>
exit 
```

用su来切换root用户和普通用户，注意切换用户后还在原来的路径上
改主机名：`hostnamectl set-hostname <newname>`

可以使用chmod为文件增加可执行权限。
```
chmod +x <file>  // 加操作权限
chmod 777 <file>  // 8进制加满权限
```

`chown -R <user>:<group> *`
## 进程管理
编译.c程序，并且将其放在后台进程运行。
ps命令用于显示当前进程 (process) 的状态。
`ps -ef`   // 显示所有命令，连带命令行
`kill <id>`  // 杀死进程
后台进程的启动是用户在输入命令行后加上“&”字符，常用于进程耗时长、用户不着急得到结果的场合。
PPID：父进程的进程号。TTY：启动进程的终端号。
NI：nice的优先级。PRI：进程的优先级。
PRI -> 进程的优先级，大部分系统都是数字越低优先级越高，进程就优先运行 。

在shell上启动了两个test_loop程序（使用`test_loop &`），这两个程序都是shell（bash）“生”出来的，即属于shell的子进程。
BASH是SHELL的一种，是大多数LINUX发行版默认的SHELL。

## Shell
Shell俗称壳（用来区别于内核），是指“提供使用者使用界面”的软件，就是一个**命令行解释器**。

定义简单变量并且打印，可以运行脚本。
`chmod + x <file.sh>`
If条件判断，字符串是否相等的比较
```
result=$(…)
if [ “$result” = “$1” ]; then
elif [ “” = “” ]; then
else
fi
```
读入清单，批量创建清单上的文件目录

shell中，
== 可用于判断变量是否相等。
= 除了可用于判断变量是否相等外，还可以表示赋值。
= 与 == 在 [ ] 中表示判断(字符串比较)时是等价的。

## Linux目录
/boot：存放Linux内核、引导配置等**启动**文件。
/dev：存放硬盘、键盘、鼠标、光驱等各种**设备**文件。
/etc：存放各种**配置**文件、配置目录。
/home：存放普通用户的默认工作文件夹（即宿主目录、家目录）。
/var：存放日志文件、用户邮箱目录、进程运行数据等**变化**的文档。
/tmp：存放系统运行过程中使用的一些**临时**文件。

## QUESTION
1. 可执行文件前为什么要加`./`？
"./"表示当前目录下的可执行文件。
若要在任意目录下访问。
	1. `chmod +x xx.sh`加上写权限。
	2. 在`~/.bashrc`中将当前目录加入到`export PATH=$PATH:`后。
2. FTP是什么？
FTP就是文件传输协议。用于互联网双向传输，控制文件下载空间在服务器复制文件从本地计算机或本地上传文件复制到服务器上的空间。使用Xshell6中的Xftp6。
3. 如何将静态页面部署到服务器上？
在服务器中安装`nginx`，使用`/etc/init.d/nginx start`启动，把`index.html`放在`/usr/share/nginx/html/`之下。

4. `yum install`的`-y`参数是什么意思？
遇到询问时自动yes。

5. 如何看自己的Linux服务器是多少位的？
`getconf LONG_BIT`











