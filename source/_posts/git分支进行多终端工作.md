---
title: Git分支进行多终端工作
date: 2020-02-18 15:42:15
tags: [Hexo,Git]
categories: Hexo
---
<meta name="referrer" content="no-referrer"/>
最近把原本部署在GitHub上的hexo同时部署到码云上，速度快到飞起。
可做对比，我的[GitHub Pages](https://hongchenglong.github.io)像乌龟一样慢吞吞，我的[Gitee Pages](https://hongchenglong.gitee.io)像兔子一样敏捷。

<!-- more -->

> 使用hexo，如果换了电脑怎么更新博客？

一个分支hexo用来存放Hexo生成的网站原始的文件，另一个分支master用来存放生成的静态网页。

我以操作码云为例。

1. 上传分支
新建一个hexo分支，点击**管理**，并设为**默认**分支。
![](https://img2018.cnblogs.com/blog/1677222/202002/1677222-20200218154619708-1227810824.png)

![](https://img2018.cnblogs.com/blog/1677222/202002/1677222-20200218154951236-1568229660.png)




2. 克隆仓库到本地
`git clone git@gitee.com:hongchenglong/Hongchenglong.git`

3. 将博客源文件全部复制过来，除了`.deploy_git`。
注意，如果之前克隆过theme中的主题文件，那么应该把主题文件中的`.git`文件夹删掉，因为**git不能嵌套上传**。


4. 上传源文件到码云上
    ```
    git add .
    git commit –m "xxxx"
    git push 
    ```

5. 发布博客`hexo g -d`

6. 最后手动更新部署<span style="color:red">master</span>分支

![](https://img2018.cnblogs.com/blog/1677222/202002/1677222-20200218161451693-906408523.png)





参考知乎回答：https://www.zhihu.com/question/21193762/answer/489124966
