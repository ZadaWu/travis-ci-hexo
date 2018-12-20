---
title: node 升级后版本切换使用
date: 2018-12-20 11:56:17
tags: node
---

原因我就不说了，走了些弯路。新版本升级后，原来的angularjs项目完全不能跑，差点跪了，但是跑mpvue的小程序项目以及koa没问题，我想应该是版本的问题，这里讲一下如何在项目中选择使用的node版本。

## nvm，node，n的关系

### nvm与node
nvm是Mac下的node 的管理工具

### nvm与n的区别
node版本管理工具还有一个是TJ大神的n命令，n命令是作为一个node模块而存在，二nvm是一个独立与node／npm的外部shell脚本，因此n命令比nvm更佳局限。

由于npm安装的模块路径均为/usr/local/lib/node_modules,当使用n切换不同的node版本是，实际上会共用全局的node／npm目录，因此不能很好的满足『按不同 node 版本使用不同全局 node 模块』的需求。

## 升级
###  使用npm升级node.js
``` bash
sudo npm cache clean -f
sudo npm install -g n
sudo n stable
```

### 你可以查看你的版本好
``` bash
node -v
```

## 降级
### 先查看本机有几个npm版本
```bash
nvm list
```

结果如下:
```bash
        v7.10.1
->      v11.2.0
        v11.5.0
         system
default -> node (-> v11.5.0)
node -> stable (-> v11.5.0) (default)
stable -> 11.5 (-> v11.5.0) (default)
iojs -> N/A (default)
lts/* -> lts/dubnium (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.15.1 (-> N/A)
lts/carbon -> v8.14.1 (-> N/A)
lts/dubnium -> v10.14.2 (-> N/A)
```

### 切换到7.10.1
```bash
nvm use v7.10.1
```

结果如下：
```bash
Now using node v7.10.1 (npm v4.2.0)
```

## 其他命令

### 直接运行特定版本的 Node
```bash
nvm run 4.2.2 --version
```

### 在当前终端的子进程中运行特定版本的 Node
```bash
    nvm exec 4.2.2 node --version
```

### 确认某个版本Node的路径
```bash
nvm which 4.2.2
```

### 安装 Node 的其他实现，例如 iojs（一个基于 ES6 的 Node 实现，现在已经和 Node 合并）
```bash
nvm install iojs-v3.2.0
```


