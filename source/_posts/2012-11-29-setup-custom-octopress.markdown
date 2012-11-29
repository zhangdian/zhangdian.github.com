---
layout: post
title: "个性化octopress设置"
date: 2012-11-29 00:08
comments: true
categories: [octopress]
---
###1. Octopress个性化设置文件
主要文件都在source/_includes/文件夹中，其中
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

<!-- more -->

###2. sina相关
sina的开放平台上提供了很多可以作为插件到octopress中的元素，包括分享按钮、关注按钮等等，见链接：

1. [sina开放平台](http://open.weibo.com/)
2. [sina分享按钮界面](http://open.weibo.com/sharebutton)

####2.1 sina分享
要想在边框栏设置sina分享，要修改三个地方的内容：

* 添加文件/source/_includes/custom/asides/sina_weibo_sharing.html文件，其中内容如下：
{% include_code ruby sina_weibo_sharing.html %}
* 修改_config.yml，在最后添加下面的代码：
```
# Weibo 
weibo_uid: 1930318973
weibo_fansline: 0   # How many lines for the fan list
weibo_show: true    # Whether you want your weibo content to be shown
weibo_pic: true     # Whether you want the pictures in weibo to be shown
weibo_skin: 10      # Please refer to http://weibo.com/tool/weiboshow
weibo_share: true   # Whether show the sharing button
```
* 修改_config.yml，在defaule_asides数组中添加一项：
```
custom/asides/sina_weibo_sharing.html
```

####2.2 sina关注
要想在边框栏设置sina关注，要修改两个地方的内容：

* 添加文件/source/_includes/custom/asides/sina_weibo_follow.html文件，其中内容如下：
{% include_code sina_weibo_follow.html %}
* 修改_config.yml，在defaule_asides数组中添加一项：
```
custom/asides/sina_weibo_follow.html
```

###3. About.html
可以添加关于自己的介绍页面，同样，需要修改两个地方的数据：

* 添加文件/source/_includes/custom/asides/about.html的内容
* 修改_config.yml，在defaule_asides数组中添加一项：
```
custom/asides/about.html
```

###4. 遇到的问题
####4.1 undefined method `Py_IsInitialized' for RubyPython::Python:Module
在使用插件功能给博客添加边框栏项目的时候，提示上述错误，原因是没有安装python，解决办法是首先安装python，然后bundle update更新一下，就ok了。参考网站：

1. [Py_IsInitialized error](https://github.com/github/gollum/issues/225)
2. [Exception on generate codeblock with "lang:" on Windows](https://github.com/imathis/octopress/issues/262)