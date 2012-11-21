---
layout: post
title: "git_operation_with_octopress"
date: 2012-11-21 15:34
comments: true
categories: octopress,git
---

* 默认情况下，octopress在本地只有一个source分支。我另外建立一个dev分支，开始的时候，设置dev分支和source分支一致，在source分支，执行命令(1)就可以新建一个和source内容一样的分支，并且自动checkout到dev分支；

    git checkout source -b dev (1)

* 以后在编辑博客的时候，在dev分支编辑，编辑完之后在source文件夹中，执行命令(2)就可以将该表提交；

    git add *
    git commit -m'msg' (2)

* 然后切换到source分支，pull远程的代码下来，然后merge dev分支的代码，然后将source的代码push上去就完成代码的更新了；

    git checkout source
    git pull origin source
    git merge dev
    git push origin source

* 最后生成，部署新的博客内容就ok了；
    
    rake generate
    rake deploy

此外，以后每次编辑博客之前，最好首先将远程的代码pull下来，然后编辑，编辑完之后最后马上push，这样可以防止冲突的产生。
