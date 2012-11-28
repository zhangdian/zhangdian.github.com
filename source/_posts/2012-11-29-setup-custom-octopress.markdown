---
layout: post
title: "个性化octopress设置"
date: 2012-11-29 00:08
comments: true
categories: [octopress]
---
###1. Octopress个性化设置文件
主要文件都在source/_includes/文件夹中，其中其中
```
/asides/ #包含侧边栏的项目
/custom/ #包含个性化头部、导航栏，footer以及侧边栏等
```
/custom中包含的都是个性化的页面，其中也包含
```
/asides/ #包含个性化的侧边栏项目
/*.html  #个性化的页面，可以在这里设置自己个性化的页面
```
那么，设置自己个性化的页面，主要修改的是source/_incledes/中的内容。
此外，修改了文件内容之后，还需要修改_config.yml中的部分内容才能生效，具体见后面的设置。

###2. sina相关
####2.1 sina分享
要想在边框栏设置sina分享，要修改两个地方的内容：

* 添加文件/source/_includes/custom/asides/sina_weibo_sharing.html文件，其中内容如下：
{% include_code sina_weibo_sharing.html %}