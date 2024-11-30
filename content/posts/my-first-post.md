---
date: '2024-11-30T12:46:50+08:00'
title: '使用hugo创建个人网站'
draft: false
tags: ["html","css"]
categories: ["test"]
cover:
    image: img/wukong.png
    alt: 'image'
    caption: 'caption'
---



# 个人站点



### 使用hugo



Hugo是流行的静态网站生成器，通过hugo能够快速将md文档生成静态网页，同时社区还有很多制作精良的主题可供选择，是创建轻量级个人网站的不二之选！

>官方文档：[Quick start | Hugo](https://gohugo.io/getting-started/quick-start/)



### 安装主题

主题使用的是PaperMod，同时在演示demo也有hugo安装步骤

[Features · adityatelange/hugo-PaperMod Wiki](https://github.com/adityatelange/hugo-PaperMod/wiki/Features)



### 部署

部署可以找静态网站托管，也可以自己部署在云服务器上面。

该站点部署在云服务器上，代码托管在gitea，同时使用gitea仓库的webhook实现自动化部署。



> 在window下hugo使用的配置文件为`hugo.toml`or`hugo.yml`，在ubuntu上使用的是config.toml or`hugo.yml`，注意区分

