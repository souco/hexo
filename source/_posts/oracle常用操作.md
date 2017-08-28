---
title: oracle常用操作
date: 2017-08-28 18:25:44
category: 数据库
tags: oracle
---
#### 建立表空间和用户的步骤：  
```sql
-- 用户建立：
create user 用户名 identified by "密码";
-- 授权：
grant create session to 用户名;
grant create table to  用户名;
grant create tablespace to  用户名;
grant create view to  用户名;

-- 表空间
-- 建立表空间(一般建N个存数据的表空间和一个索引空间)：
create tablespace 表空间名
datafile ' 路径(要先建好路径)\***.dbf  ' size *M
tempfile ' 路径\***.dbf ' size *M
autoextend on  --自动增长
-- 还有一些定义大小的命令，看需要
 default storage(
 initial 100K,
 next 100k,
);

-- 例子：创建表空间
create tablespace DEMOSPACE
datafile 'E:/oracle_tablespaces/DEMOSPACE_TBSPACE.dbf'
size 1500M
autoextend on next 5M maxsize 3000M;
-- 删除表空间
drop tablespace DEMOSPACE including contents and datafiles

-- 用户权限
-- 授予用户使用表空间的权限：
alter user 用户名 quota unlimited on 表空间;
-- 或 alter user 用户名 quota *M on 表空间;

-- 表空间
CREATE TABLESPACE sdt
DATAFILE 'F:\tablespace\demo' size 800M
         EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
-- 索引表空间
CREATE TABLESPACE sdt_Index
DATAFILE 'F:\tablespace\demo' size 512M
         EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;

--2.建用户
create user demo identified by demo
default tablespace std;

-- 在11G中有个新特性，当表无数据时，不分配segment，以节省空间，导致不能导出空表
-- 建立了空的数据库后，马上执行以下关闭此特性
alter system set deferred_segment_creation=flase sscope=spfile;

--3.赋权
grant connect,resource to demo;
grant create session to demo
grant create any sequence to demo;
grant create any table to demo;
grant delete any table to demo;
grant insert any table to demo;
grant select any table to demo;
grant unlimited tablespace to demo;
grant execute any procedure to demo;
grant update any table to demo;
grant create any view to demo;

--4.导入导出相关权限
grant exp_full_database to demo;
grant imp_full_database to demo;
grant dba to demo;

-- 导入导出命令
-- ip导出方式：
exp demo/demo@127.0.0.1:1521/orcl file=f:/f.dmp full=y
exp demo/demo@orcl file=f:/f.dmp full=y
imp demo/demo@orcl file=f:/f.dmp full=y ignore=y
```
