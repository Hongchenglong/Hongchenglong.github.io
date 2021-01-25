---
title: Hexo学习笔记
date: 2020-02-16 14:50:14
tags: [Hexo]
categories: Hexo
top: true
---
记录我在使用Hexo时遇到的问题和解决方法。

> Hexo is a fast, simple & powerful blog framework.

<!-- more -->

## 如何上传文章

在你博客站点文件夹下右键空白处，选择`Git Bash Here`

1. `hexo new post ""`然后在`./source/_posts`里找到并编辑。
2. `hexo g` (hexo generate)，用于生成静态文件
3. `hexo s` (hexo server)，用于启动服务器，主要用来本地预览；完成后打开浏览器输入 `localhost:4000`
4. `hexo d` (hexo deploy)，用于将本地文件发布到github等git仓库上
5. 2、4步简写 `hexo g -d`
6. `hexo clean && hexo g && hexo d`

## 显示不出分类、标签问题

在`./source/tags/index.md`中添加`type: tags`字段。
`categories`同理。
参考博客：https://blog.csdn.net/Wonz5130/article/details/84666519

## npm

npm 出现 `operation not permitted, mkdir...`问题
解决办法：以管理员身份运行cmd输入`npm -v`，然后在git bash中就没问题了。

## 主题加载不出

我是因为配置文件url配错了，改成原有的配置就OK了。

```
url: http://yoursite.com
root: /
```

## 图片加载不出

我是引用cnblog的图片链接，刚刚上传那会还能显示图片，过几天就发现图片加载不出。
解决方法：
在文章头部加上`<meta name="referrer" content="no-referrer"/>`，解决防盗链问题。

```
---
title: Hexo学习笔记
---
<meta name="referrer" content="no-referrer"/>
```

参考博客：

- https://qsh5.cn/595.html
- https://blog.csdn.net/mqdxiaoxiao/article/details/96770756

## hexo同时部署到码云Gitee

如何创建一个首页访问地址不带二级目录的 pages，如hongchenglong.gitee.io？
**需要建立一个与自己个性地址同名的项目**，
我的**个性地址**就是`https://gitee.com/hongchenglong`里的`hongchenglong`
参考码云帮助文档：http://git.mydoc.io/?t=154714&tdsourcetag=s_pctim_aiomsg
码云的速度很快，缺点是每次部署都要去码云Pages手动**更新**

## 设置网站的图标Favicon

https://www.jianshu.com/p/82c1d33420ba

## NOTE

1. 语句含义
   `home: / || home`中的`|| home`表示会到自带库里找到home这个图标并展示。
2. 改成中文
   主目录下的配置文件`_config.yml`中修改language的值，改成`language: zh-CN`
3. 如果修改过文件内容，需要通过如下命令清除已经生成的静态文件，重新生成！
   `hexo clean`
4. 部署到Gitee上，每次修改都要去码云Pages手动**更新**master分支
5. 初始化一个Hexo，`hexo init blog`
6. 多标签，`tags: [标签1,标签2,标签3]`
7. 写新博客前记得加上`<!-- more -->`