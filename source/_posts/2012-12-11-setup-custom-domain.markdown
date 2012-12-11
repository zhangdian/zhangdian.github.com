---
layout: post
title: 设置个性化域名
date: 2012-12-11 10:05
comments: true
categories: [octopress]
---
假设你拥有自己的域名，而且又不想使用github的域名，那么可以使用github的custom domain功能，设置自己的域名。
####1. 在自己的代码库中进行设置
在source分支中，进入source文件夹，添加一个文件“CNAME”，然后再文件中填入你的域名：

```
youdomain.com
```

比如我的是：

```
blog.bd17kaka.net
```

然后commit，push到代码库即可。

####2. 设置DNS
这里分为两种情况，也就是顶级域名（Top-level domain）和子域名（SubDomain）。
#####2.1 顶级域名
对于一个顶级域名，设置一个A记录到地址204.232.175.78。这里不要使用CNAME记录，因为这样会影响你的顶级域名上的其他服务，比如邮件服务等。

#####2.2 子域名
使用子域名的话，设置一个CNAME记录到，比如我的记录是：

```
blog.bd17kaka.net   zhangdian.bd17kaka.net
```

####3. 等待
dns设置和github的设置需要一段时间的等待。

####4. 参考
* [官网资料：Setting up a custom domain with Pages](https://help.github.com/articles/setting-up-a-custom-domain-with-pages)
* [Custom Domain With Octopress and Github Pages](http://robdodson.me/blog/2012/04/30/custom-domain-with-octopress-and-github-pages/)
