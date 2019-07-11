---
layout: post
title: GithubIO+Jekyll搭建个人网站
categories: [Programming Tools]
tags: GithubIO-Jekyll
---

>欢迎大家[star本站源码](https://github.com/nijiazhi/nijiazhi.github.io)改造成属于你自己喜欢的个人网站~
>本文部分内容引用了[leach_chen的博客](https://www.jianshu.com/p/9f71e260925d)

## GithubIO
GithubIO其实是GitHub Pages，它是GitHub提供的一个免费的项目介绍网站，在项目的Settings里可以进行配置。
![GitHub Pages](/assets/images/blog/githubIO/githubIO.png)

这个强大GitHub Pages刚好可以用于搭建个人网站，目前基于jekyll或者hexo的网站居多，选择哪个就看个人喜好了，我这里选择的是jekyll，主要是因为网上相关的资料比较多，遇到问题比较好解决。主要的步骤如下：

1. 首先你要到GitHub上注册一个账号，例如我注册的用户名为：nijiazhi（用户名可以在设置里改）
2. 点击New repository–>输入仓库名称格式为：用户名.github.io(如：nijiazhi.github.io)->点击Create repository
3. 浏览器里访问 https://nijiazhi.github.io ，可以发现这个url可以被访问了
4. 把仓库代码拉取到本地，然后在里面新建一个index.html的文件，在里面输入任意内容，然后再把代码推送到git上，然后再访问改链接，可以发现index.html里面的内容被访问到了

到这里，一个免费且无限流量的github代码托管仓库就创建完成了，剩余的部分就是如何写这个静态的网站。


## Jekyll是什么？
Jekyll是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 Markdown）和我们的 Liquid 渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上（比如 GithubIO）。这个是[Jekyll的中文主页](http://jekyllcn.com/)，写的很清晰。
![jekyll](/assets/images/blog/githubIO/jekyll.png)


## Jekyll安装
1. 首先点击下载安装[Ruby installer](https://rubyinstaller.org/)
2. 点击下载[RubyGems](https://rubygems.org/pages/download)，下载完成后解压至你想放的位置，打开命令行执行：
```
cd D:\rubygems-2.7.4  # 你的解压目录
ruby setup.rb
```
3. 在命令行执行`gem install jekyll`
4. 安装完成，用jekyll命令创建一个博客模板,打开命令行执行：
```
cd d:/
jekyll new testblog
cd testblog
jekyll server
```
在浏览器输入 http://127.0.0.1:4000/ 即可浏览刚刚创建的blog

## Jekyll目录结构
Jekyll目录结构主要包含如下目录：
- assets 辅助资源 css布局 js脚本 图片等
- _posts 博客内容
- _pages 其他需要生成的网页，如About页
- _layouts 网页排版模板
- _includes 被模板包含的HTML片段，可在_config.yml中修改位置
- _data 动态数据
- _sites 最终生成的静态网页
- _config.yml 网站的一些配置信息
- index.html 网站的入口


---
# 相关引用
1. [GitHub Pages(GithubIO)](https://pages.github.com/)
2. [Jekyll官网](http://jekyllcn.com/)
3. [Jekyll主题](http://jekyllthemes.org/)
4. [GithubIO+Jekyll搭建详细教程](https://www.jianshu.com/p/9f71e260925d)
