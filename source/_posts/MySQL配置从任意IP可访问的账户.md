---
title: MySQL配置从任意IP可访问的账户
date: 2017-05-16 13:09:16
category: 编程
tags: MySQL
---
MySQL 配置从任意IP可访问的账户：
`user`表中用户名`@`后面是`%`百分号的都是任意地址可连接的
如：`'souco'@'%'`

另外：
查看 MySQL 数据库中所有用户
```
mysql> SELECT DISTINCT CONCAT('User: ''',user,'''@''',host,''';') AS query FROM mysql.user;
```

查看数据库中具体某个用户的权限
```
mysql> show grants for 'cactiuser'@'%';   
mysql> select * from mysql.user where user='cactiuser' \G   
```

查看 user表结构，需要具体的项可结合表结构来查询
```
mysql> desc mysql.user;
```