---
layout: post
title: Jupyter小技巧
categories: [编程必备]
tags: JupyterNotebook
---

## JupyterNotebook是什么？
Jupyter Notebook 是一款开放源代码的 Web 应用程序，可让我们创建并共享代码和文档。

简单来说，它就是可以在web端方便写代码的小神器，大概这样子：
![jupyter](/assets/images/blog/jupyter/jupyter.png)


## 魔法命令
魔法命令是一些超酷的玩法，可以完成除了写代码以外很有用的功能，比如我们常见的几个魔法命令：

```
1. %%bash 或者 %%cmd，区别在于不同系统；
2. %%time：cell的代码计时；
3. %matplotline inline：在jupyter内打印图片；
4. %load：将本地py文件代码导入进来到当前单元中；
5. %run：运行本地代码，可以共同函数写在不同的notebook，用的时候运行；
```

想知道更多的命令可以用**%lsmagic**查看，Jupyter其实提供了两大类魔法命令：
```
1. line magics：通过在前面加%，表示magic只在本行有效；
2. cell magics：通过在前面加%%，表示magic在整个cell单元有效；
```

## 超牛X的插件

插件是Jupyter里必须要推荐的东西，有了牛X的插件才能体会到web写代码的爽，主要推荐下面这个插件：
``` 
    conda安装
    conda install -c conda-forge jupyter_contrib_nbextensions
    conda install -c conda-forge jupyter_nbextensions_configurator

    pip安装
    pip install jupyter_nbextensions_configurator jupyter_contrib_nbextensions 
    jupyter contrib nbextension install --user
    jupyter nbextensions_configurator enable --user
```

可以在插件界面勾选一些配置项（下面有详细介绍），体会下插件的强大，比如下面几个靠谱的功能：
![jupyter_chajian_config](/assets/images/blog/jupyter/jupyter_chajian.png)

### 插件1 - 代码目录
![jupyter_chajian_table](/assets/images/blog/jupyter/jupyter_chajian_1.png)

### 插件2 - 折叠代码块
![jupyter_chajian_table](/assets/images/blog/jupyter/jupyter_chajian_2.png)



## 常用快捷键

```
Esc： 退出编辑模式
Ctrl+enter： 执行本cell
shift+enter： 执行本cell，向下建立一个新cell
a： 向上建立一个cell
b： 向下建立一个cell
m： 把cell切换至markdown模式
y： 把cell切换至code模式
l： 显示行数
```


## 启动目录设置

Jupyter有两种启动方式比较常用：

- **在默认目录启动Jupyter**

    修改默认启动目录，在cmd中启动Jupyter时，就会跳到设置的默认目录。在cmd中执行命令，得到jupyter配置文件（注意文件路径），`jupyter notebook --generate-config`

    ![jupyter config](/assets/images/blog/jupyter/jupyter_config.png "jupyter_config")
    <!-- <div style="align: left"><img src="/assets/images/blog/jupyter/jupyter_config.png"/></div> -->

    修改配置文件中的默认启动目录即可（注意去掉#注释）
    ![jupyter config default dir](/assets/images/blog/jupyter/jupyter_config_dir.png "jupyter_config_default_dir")

- **在指定目录启动Jupyter**
        
    在启动命令后加入指定目录，即可在那个目录启动Jupyter，`jupyter notebook c:\\`

    ![jupyter dir](/assets/images/blog/jupyter/jupyter_dir.png "jupyter_dir")


## 用户密码

- cmd中生成jupyter的配置文件：jupyter notebook --generate-config
- cmd继续输入：jupyter notebook password （会输入两次密码）
- 密码设置成功，登录服务器： jupyter notebook
![jupyter password](/assets/images/blog/jupyter/jupyter_password.png)


---

## 相关引用
1. [Jupyter官网](https://jupyter.org/)
2. [Jupyter魔法命令](https://blog.csdn.net/sinat_22840937/article/details/80315378)
3. [Jupyter插件jupyter_contrib_nbextensions](https://github.com/jcb91/jupyter_contrib_nbextensions)


