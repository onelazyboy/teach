---
layout:     post
title:      "Ubuntu环境下GithubPage+Jekyll部署"
subtitle:   "环境部署"
author:     "PYJ"
header-img: "static/img/post-bg-06.jpg"
catalog: true
tags:
    - jekyll
    - ubuntu
    - Github Page
---
##	Jekyll简介

简单: 无需数据库、无需评论功能，不需要不断更新版本，只需要关心博客内容。

静态: 只用 Markdown (或 Textile)、Liquid、HTML & CSS 就可以构建可部署的静态网站。

博客形态: 自定义地址、分类、页面、博客内容 以及 自定义的布局设计 都是系统中的一等公民.

##	Github Pages简介

Github Pages是Github提供给每个用户的，用来介绍和展示自己的项目。我们可以使用Jekyll生成静态网站，然后部署到Github pages上，利用Github的服务器，运行自己的网站。

Github Pages详细情况
##	安装环境

####	安装ruby环境

之所以要安装ruby，是因为jekyll是用ruby开发的。ubuntu14.04 LTS上默认是没有安装ruby环境的，需要自己安装。安装命令如下：

sudo apt-get install ruby1.9.1-dev
或者<code>sudo apt-get install ruby-dev</code>

（一定要用这个dev版本，不然用其他版本会出错，详细可查看最后面的异常1及其解决）

安装完成后，在终端中输入ruby -v，出现如下结果，则说明安装成功：

ruby 1.9.3p484 (2013-11-22 revision 43786) [x86_64-linux]

####	安装nodejs环境（貌似不安装也是可以，gem是ruby的包管理器，我们下面会通过这个管理器安装Jekyll）

sudo apt-get install nodejs

nodejs安装完成后，重新在终端中输入gem -v，出现如下结果，表明安装成功：

1.8.23
####	安装Jekyll环境

在终端中输入如下命令安装Jekyll，这个过程比较慢，和源有关：

sudo gem install jekyll

安装完成后，在终端中输入如下命令，验证jekyll安装是否成功：

jekyll new ttestblog

如果成功创建目录，则说明jekyll安装成功，可以进行之后的工作了。

原文地址: http://www.cnblogs.com/mo-wang/p/5115266.html