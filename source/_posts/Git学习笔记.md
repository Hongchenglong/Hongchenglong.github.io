---
title: Git学习笔记
date: 
tags: [Git]
---

Git的官方网站：http://git-scm.com
学习[廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)的Git教程所做笔记。
外国网友制作的[Git Cheat Sheet](https://gitee.com/liaoxuefeng/learn-java/raw/master/teach/git-cheatsheet.pdf)

<!-- more -->

# Git简介
Git是目前世界上最先进的**分布式版本控制系统**。由Linus使用C写成。
## 版本库
版本库又名仓库，英文名**repository**。
初始化一个Git仓库，使用`git init`命令。
添加文件到Git仓库，分两步：

1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
2. 使用命令`git commit -m "<message>"`，完成。(-m后面输入的是本次提交的说明)

注意：
- 目录名尽量不使用中文。
- 强烈建议使用标准的UTF-8编码。
- 版本控制系统是没法跟踪Word文件的改动。
- `.git`目录是Git来跟踪管理版本库的，尽量不要去改动。

# 时光机回溯
- 要随时掌握工作区的状态，使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

##版本回退
- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard <commit_id>`。
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

## 工作区和暂存区
工作区（Working Directory）：在电脑里能看到的目录。
版本库（Repository）：隐藏目录`.git`。
其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。
![](https://img2018.cnblogs.com/blog/1677222/202002/1677222-20200214213914797-1652178625.png)
文件往Git版本库里添加的时候，是分两步执行的：
第一步是用`git add`把文件添加进去，实际上就是<span style="color:red">把文件修改添加到暂存区</span>；
第二步是用`git commit`提交更改，实际上就是<span style="color:red">把暂存区的所有内容提交到当前分支</span>。
**需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。**

## 管理修改
为什么Git比其他版本控制系统设计得优秀，因为**Git跟踪并管理的是修改**，而非文件。
每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。

## 撤销修改
- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- <file>`。
- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。
- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，使用命令`git reset --hard <commit_id>`，不过前提是没有推送到远程库。

## 删除文件
想要在github上面删除，但又不想在本地删除
```bash
$ git rm -r --cached <file>  # --cached不会删除本地的file
$ git commit -m 'delete <file>'
$ git push -u origin master
```

### 小结
- `git checkout -- <file>`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
- 命令`git rm <file>`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

# 远程仓库
本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：
1. 创建SSH Key。`$ ssh-keygen -t rsa -C "youremail@example.com"`
2. 打开`git bash`，输入`cat ~/.ssh/id_rsa.pub`即可查看ssh公钥。
3. “Add SSH Key”，在Key文本框里粘贴id_rsa.pub文件的内容。

### 何谓公钥
1. 很多服务器都是需要认证的，ssh认证是其中的一种。在客户端生成公钥，把生成的公钥添加到服务器，你以后连接服务器就不用每次都输入用户名和密码了。
2. 很多git服务器都是用ssh认证方式，你需要把你生成的公钥发送给代码仓库管理员，让他给你添加到服务器上，你就可以通过ssh自由地拉取和提交代码了。

### 为什么GitHub需要SSH Key呢？
因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

## 添加远程库
- 要关联一个远程库，使用命令`git remote add origin git@github.com:<server-name>/<repo-name>.git`；
- 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；
- 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；(远程库的名字就是origin，这是Git默认的叫法)
- 分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作。

## 从远程库克隆
- 要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。
- Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快。

# 分支管理

## 创建于合并分支
![](https://img2018.cnblogs.com/blog/1677222/202002/1677222-20200215032332010-1516736742.png)

- 查看分支：`git branch`
- 创建分支：`git branch <name>`
- 切换分支：`git checkout <name>`或者`git switch <name>`
- 创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`
- 合并某分支到当前分支：`git merge <name>`
- 删除分支：`git branch -d <name>`

## 解决冲突
![](https://img2018.cnblogs.com/blog/1677222/202002/1677222-20200215033101385-1093798650.png)

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用`git log --graph`命令可以看到分支合并图。

## 分支管理策略
![](https://img2018.cnblogs.com/blog/1677222/202002/1677222-20200215033530403-1782330777.png)
Git分支十分强大，在团队开发中应该充分应用。
合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

## Bug分支
- 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
- 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；
- 在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

## Feature分支
- 开发一个新feature，最好新建一个分支；
- 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

## 多人协作
- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin <branch-name>`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。


## Rebase(变基)
- `git rebase`操作可以把本地未push的分叉提交历史整理成直线；
- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

# 标签管理
发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。
tag是一个让人容易记住的有意义的名字，如v1.0，它跟某个commit绑在一起。
## 创建标签
- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。

## 操作标签
- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

# 使用GitHub
点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己的账号下clone：
`git clone git@github.com:<username>/bootstrap.git`
一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地址git@github.com:twbs/bootstrap.git克隆，因为没有权限，你将不能推送修改。

### 小结
- 在GitHub上，可以任意Fork开源仓库；
- 自己拥有Fork后的仓库的读写权限；
- 可以推送pull request给官方仓库来贡献代码。


# 使用Gitee
如果我们希望体验Git飞一般的速度，可以使用国内的Git托管服务——Gitee（gitee.com）。
用`git remote -v`查看远程库信息。
由于远程库不能同名，要先删除已有的GitHub远程库。`git remote rm origin`
再分别关联GitHub和Gitee：
```bash
$ git remote add github git@github.com:<server-name>/<repo-name>.git
$ git remote add gitee git@gitee.com:<server-name>/<repo-name>.git
```
之后推送，使用命令：
```bash
$ git push github master
$ git push gitee master
```


# 自定义Git
`$ git config --global color.ui true`让Git显示颜色

## 忽略特殊文件
- 忽略某些文件时，需要编写`.gitignore`；
- `.gitignore`文件本身要放到版本库里，并且可以对`.gitignore`做版本管理！

## 配置别名
用st表示status：`$ git config --global alias.st status`
很多人都用co表示checkout，ci表示commit，br表示branch：
```
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
```
配置一个git last，让其显示最后一次提交信息：
`$ git config --global alias.last 'log -1'`
`--global`参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。

## 搭建Git服务器

# 使用Source Tree