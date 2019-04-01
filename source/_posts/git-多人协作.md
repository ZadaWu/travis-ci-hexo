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
这种操作流程存在的问题：
1. 上一个需求在发布前，新需求代码不能合并到test上面测试
2. test合并到master上面，master自动发布，是有问题的，master应该是手动发布的
3. 多人协作可能会出现相互merge改了代码而且别人不知道的情况，这种情况应该暴露出来

但是，由于test分支的代码直接merge到master分支上是不可靠不靠谱的，因此之后老大定下来test分支永远不能合并到master分支上，具体可以看以下：

## 新的流程总结下：

 1.pull master 在本地master切开发分支feat1
 2.feat1开发
 3.切test，merge feat1 --squash 可能会有冲突，注意不要将test代码带入feat1
 4.在feat1 改bug , 切test merge feat1 --squash 
 5.切master ，merge feat1 --squash
 6.pull或fetch master，解决冲突
 7.push origin master
 8.预生产回归，发布正式



## ps
[git merge -squash 介绍 ](https://www.cnblogs.com/lookphp/p/5799533.html)

