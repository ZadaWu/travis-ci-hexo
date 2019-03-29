---
title: sails + redis
date: 2019-03-29 14:59:27
tags:
---

之所以这两个一起写，是因为项目中有用到，而我也是新手接触，因此做一个简单的记录。
你可以参考我的git项目[sails-test](https://github.com/ZadaWu/sails-test)

[参考文档](https://sailsjs.com/documentation/concepts/actions-and-controllers)
[1-2视频](https://www.youtube.com/watch?v=AmjiDC_JUt4)
[3-4视频](https://www.youtube.com/watch?v=qAQWBfnO6n0)

## sails
1. [入门地址](https://sailsjs.com/get-started)

```
npm install sails -g
sails new test-project
cd test-project
sails lift（会有提示，1. FOR DEV:alter）
```


2. 新建一个restful的API

```
sails genenrate api hello
```

至此，你目前可以在磁盘缓存数据的基础上调用hello这个api接口
新增用户=>PUSH http://localhost:1337/hello/Create?userId=13&userName=san
修改用户=>PATCH http://localhost:1337/hello/1?userId=11&userName=wu
删除用户=>DEL http://localhost:1337/hello?id=1 (id为创建后返回的id)
查找所有用户=>GET http://localhost:1337/hello
通过主键查找一个用户=>GET http://localhost:1337/hello/1

3. 使用mongoDB存储
 * 首先你需要安装一个mongoDB,这里我自己创建了一个数据库 hello
 * 安装 sails-mysql : npm install -g sails-mysql
 * 修改models/Hello.js 配置你的表以及字段的属性
 
        ```
        
        module.exports = {
        
          tableName: 'hello',
          primaryKey: 'id',
        
          attributes: {
            userId: {
              type: 'string',
              required: true,
              unique: true,
              columnName: 'user_id',
            },
            userName: {
              type: 'string',
              columnName: 'user_name',
              defaultsTo: '',
            },
          },
        
          async beforeCreate(data, next) {
            return await next()
          },
        
          async afterCreate(data, next) {
            return await next()
          },
        
        };
        
        
        ```
    
    * config中的datastores.js里面配置mysql的用户名/密码/IP/端口号/数据库
    
        ```
        module.exports.datastores = {
          default: {
            adapter: 'sails-mysql',
            url: 'mysql://root:password@localhost:3306/hello',
          },
        };
        ```
4. 至此，你可以重启项目，调用你的接口，数据库里面就能看到了

ps： 你可以全局安装nodeman, nodeman app.js 能帮你监控app.js是否改动，改动则更新配置

## redis

1. [nodejs使用redis文档](http://redis.js.org/)


