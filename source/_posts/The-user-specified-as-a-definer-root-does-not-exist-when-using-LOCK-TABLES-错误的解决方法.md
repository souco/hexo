---
title: >-
  The user specified as a definer ('root'@'%') does not exist when using LOCK
  TABLES 错误的解决方法
date: 2017-04-28 13:38:20
category: 编程
tags: MySQL
---
执行数据库导出语句：
```
mysqldump -uroot -p qyw > E:/sql/20170428125848qyw.sql
```
报错：
```
mysqldump: Got error: 1449: The user specified as a definer ('root'@'%') does not exist when using LOCK TABLES
```
权限问题，授权给`root`所有`sql`权限
```
mysql> grant all privileges on *.* to root@"%" identified by ".";
Query OK, 0 rows affected (0.00 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)
```
再次执行`mysqldump -uroot -p qyw > E:/sql/20170428125848qyw.sql`成功。

另外附上今天发现的数据导出导出的问题。 
因为平常都是使用`sqlyog`导入导出数据，最近一个项目的数据库比较大，转而使用命令行的导入。 
今天突然发现命令行导入一个数据库非常慢，然后研究了下原因，发现`sqlyog`导出的数据库`sql`文件，使用命令导入时非常慢，导入速度还没有`sqlyog`导入的快。 
比较了下`sqlyog`导出的`sql`文件与`mysqldump`导出的sql文件，发现两者还是有些区别的。当然，也可能是`sqlyog`导出的时候有些选项没有勾选。 
尝试后发现，与`sqlyog`导出的`sql`文件相比，`mysqldump`导出的`sql`文件在使用命令导入时非常快。
因此，使用上来说，如果数据比较小，用`sqlyog`导出导入就可以。如果数据比较大，用`mysqldump`导出然后用命令导入就比较快。
