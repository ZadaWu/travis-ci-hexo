---
title: mysql
date: 2019-03-26 14:53:32
tags:
---

## [参考视频安装mysql](https://www.youtube.com/watch?v=jzvsotmNrK8)
    
    
## [如何找到mysql配置文件](https://stackoverflow.com/questions/2482234/how-do-i-find-the-mysql-my-cnf-location)
    
建议参考顺序：
    
```
    /etc/my.cnf 
    /etc/mysql/my.cnf 
    /usr/local/etc/my.cnf(我的是这个，找的时候已经快感动哭了) 
    ~/.my.cnf
```

## [无法重设置密码的解决方案](https://stackoverflow.com/questions/49992868/mysql-errorthe-user-specified-as-a-definer-mysql-infoschemalocalhost-doe/50117262)
    
    mysql_upgrade -u root

## 使用navicat连接报错

```
Can't connect to MySQL server on '127.0.0.1' (61 "Connection refused")
```

解决方案：
[注释掉my.cnf里面的bind-address的IP限制](https://stackoverflow.com/questions/1420839/cant-connect-to-mysql-server-error-111)


