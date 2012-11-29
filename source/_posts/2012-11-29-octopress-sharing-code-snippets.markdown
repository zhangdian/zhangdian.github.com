---
layout: post
title: "octopress代码片段分享"
date: 2012-11-29 10:44
comments: true
categories: [octopress]
---
###1.介绍
octopress文档中提供了很多种的代码分享高亮方法，其中我用的最多的就是两种：

* Backtick Code Blocks
* Include Code Snippets

###2. Backtick Code Blocks
这种方式可以用于代码片段的分享，其格式如下
```
``` [language] [title] [url] [link text]
code snippet
```
```
其中带‘[]’的都是可选项。
#### 问题:

* 我把可选项都带上，但是不能正确显示，在后台一直提示“favicon.ico无法找到”。

###3. Include Code Snippets
这种方式可以将文件系统中的任何文件导入到博客的任何位置，并且还提供高亮和代码下载。
####3.1 语法
```
{% include_code [title] [lang:language] path/to/file %}
```
其中title是标题；lang是你的代码的语言，可以提供高亮的功能；

文件路径的默认根目录在_config.yml中的变量code_dir中，而其默认值是source/downloads/code，只需要把要include的代码放到这个文件夹里就行了。