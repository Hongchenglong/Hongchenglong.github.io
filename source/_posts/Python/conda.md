---
title: conda
date: 2021-12-10 00:12:15
tags:
categories:
---

<meta name="referrer" content="no-referrer"/>
conda是一个通用的包管理器，即任何语言的包都可以用其进行管理，同时也是环境管理器。	

<!-- more -->

**conda是一个通用的包管理器**，即任何语言的包都可以用其进行管理，同时也是环境管理器。	

- https://conda.io/projects/conda/en/latest/user-guide/getting-started.html
- https://blog.csdn.net/weixin_34381687/article/details/92060466

## 管理conda

更新conda
`conda update conda`


## 管理环境

列出环境
`conda info -e`

创建环境
`conda create -n python27 python=2.7`

删除环境
`conda remove -n python27 --all`

切换环境

```
conda activate python27
conda deactivate
```

## 管理Python

切换环境，检查版本

```
activate python27
python --version
```

## 管理包

```
# 检查pip安装
conda list
# 安装
conda install numpy
pip install matplotlib==2.2.3 --trusted-host pypi.douban.com --user
```

更换Jupyter Notebook内核Python版本

- https://www.cnblogs.com/shanger/p/12006322.html
- https://blog.csdn.net/taijiedi13/article/details/59483763
- https://ipython.readthedocs.io/en/stable/install/kernel_install.html#kernel-install

当conda install找不到包时，可以使用该环境下的pip

```
(CertifiableBayesianInference) C:\Users\T470>D:\Users\T470\Anaconda3\envs\CertifiableBayesianInference\Scripts\pip install tensorflow-probability==0.15.0
```

指定豆瓣源

`-i https://pypi.douban.com/simple`

## FAQ

- pip与conda的区别？

pip是Python官方认可的包管理器。

**conda是一个通用的包管理器**，即任何语言的包都可以用其进行管理，同时也是环境管理器。	