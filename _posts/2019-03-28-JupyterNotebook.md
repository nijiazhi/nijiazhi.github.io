---
layout: post
title: Jupyter小技巧
categories: [编程必备]
tags: JupyterNotebook
---

## JupyterNotebook是什么？
Jupyter Notebook 是一款开放源代码的 Web 应用程序，可让我们创建并共享代码和文档。

简单来说，它就是可以在web端方便写代码的小神器，大概这样子：


## JupyterNotebook魔法命令
魔法命令是一些超酷的玩法，除了在Jupyter里面写代码以外，还可以在里面运行很多其他东西，比如我们常见的几个魔法命令：

- %%bash 或者 %%cmd，区别在于不同系统；
- %%time：cell的代码计时；
- %matplotline inline：在jupyter内打印图片；
- %load：将本地py文件代码导入进来到当前单元中；
- %run：运行本地代码，可以共同函数写在不同的notebook，用的时候运行；

想知道更多的命令可以用**%lsmagic**查看，Jupyter其实提供了两大类魔法命令：
1. line magics：通过在前面加%，表示magic只在本行有效；
2. cell magics：通过在前面加%%，表示magic在整个cell单元有效；


## JupyterNotebook里超级有用的插件

插件是Jupyter里必须要推荐的东西，有了牛X的插件才能体会到web写代码的爽，主要推荐下面这个插件：
``` conda
    conda install
```

## JupyterNotebook常用快捷键


## 相关引用
1. [jupyter官网](https://jupyter.org/)
2. [Jupyter的魔法命令](https://blog.csdn.net/sinat_22840937/article/details/80315378)


