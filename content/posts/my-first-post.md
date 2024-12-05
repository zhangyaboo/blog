---
date: '2024-11-30T12:46:50+08:00'
title: '使用hugo创建个人网站'
draft: false
tags: ["html","css"]
categories: ["test"]

---


> 该站点使用hugo进行的搭建，并且实现了自动化部署，在搭建过程当中也踩了不少的坑，这里记录一些。

### 站点搭建简介

### 框架选取

市面上有很多不用写代码就可以建站的工具，比如worldpress,hexo等等。

大致可以分为两类，一类是静态网站生成器，比如hexo, hugo等, 是将写作对应的markdown文件渲染成静态网页，因为是静态文件，速度会比较快，并且搭建简单，尤其适合个人网站的搭建。

另一类是动态网站，比如worldpress、Halo等，这些需要涉及到数据库的交互，更适合企业，比如一些电商之类的，搭建会略微比前者复杂一丢丢（都是个人网站其实也没复杂多少啦，多了数据库交互而已）。因为存在数据库，后期维护以及拓展其他功能会比静态网站强大很多，对应更多的学习成本。

为什么选择hugo?

感觉它star比较多（算理由吗？）。。。

之前用过worldpress,Halo又要php又要MySQL，本就弱鸡的服务器勉强能够带起来，访问的速度非常的慢，体验糟糕。

因此还是选用了静态网站生成器，hugo和hexo中选择了前者，hugo的star多一点。

国内存在一些非官方的文档，这里仍然推荐官方文档，大陆可能会访问的慢一点。

>官方文档：[Quick start | Hugo](https://gohugo.io/getting-started/quick-start/)



### 安装主题

主题使用的是PaperMod，同时在演示demo也有hugo安装步骤。

[Features · adityatelange/hugo-PaperMod Wiki](https://github.com/adityatelange/hugo-PaperMod/wiki/Features)



### 部署

部署一是静态网站托管，二是部署在云服务器上。

该站点部署在云服务器上，代码托管在gitea，同时使用gitea仓库的webhook实现自动化部署。

一般都是在windows下进行写作，写好把静态网站传到服务器就好了，我这里是把对应的写作的md以及配置文件上传保存到仓库，这样可以实现在其他电脑上也可以写作。这就要求服务器要有对应的hugo来生成静态网页。

## 踩到的坑

### 版本保证一致

在本地hugo能够正常生成静态文件，到了服务器上使用hugo命令就不行了。原因如下

1. hugo版本对不上
2. hugo在windows下和Linux的配置文件不同

hugo在云服务上的版本要和本地的版本保持一致，使用`hugo version`命令可以查看

hugo是windows下的配置文件是hugo开头的，但是在Linux上的config开头的，顺便也可以把它当中开发和生成对应的配置文件。:dog2:



## 要补的坑

自动化部署使用git hooks，原理是git仓库在内容在更新后会向某个地址或IP（服务器地址）推送一个POST请求，服务器上使用python脚本一直监听该请求，在收到请求后执行git pull的操作，触发本地git hooks，在执行hugo部署的命令。

这个过程第一次配置还是蛮麻烦的，我省略了python脚本对密钥的判断，以及执行git pull的权限判断（仓库设为了共有的。。）后面再慢慢搞。
