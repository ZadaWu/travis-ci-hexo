---
title: git 多人协作
date: 2019-03-13 18:41:13
tags:
---

## 现状
video分支用来开发提交代码，
test分支是用来测试环境的，
interaction是别的团队的开发提交代码分支，
master是用来生产环境发布,我现在想新开发个功能：
A.合并test和master分支代码到video分支，并且拉最新的video代码

```*     git checkout video
*     git pull origin video
*     git rebase test
*     git rebase master
```

B.新功能操作在本地分支上进行

```*     git branch dev
*     git checkout dev
*     git add '1.file'
*     git commit -m '测试修改'
```

C.切到video分支上，合并最新的test和master代码,拉最新的video代码，merge本地分支代码，并且提交

```*     git checkout video
*     git pull origin video
*     git rebase test
*     git rebase master
*     git merge dev
*     git branch -d dev
*     git push origin video
```

## 正确的做法



