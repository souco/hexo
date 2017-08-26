---
title: IDEA内存参数配置
date: 2017-04-11 18:07:02
category: 编程
tags: [IDEA,IDEA内存]
---
#### IDEA内存参数配置
- `-Xms512m`：`JVM`起始内存
- `-Xmx1280m`：`JVM`分配最大内存
- `-XX:PermSize=300m`：虚拟机为`java`永久生成对象内存配置，起始内存
- `-XX:MaxPermSize=512m`：虚拟机为`java`永久生成对象内存配置，最大内存
- `Tomcat`：`-Xms512m -Xmx1280m -XX:PermSize=300m -XX:MaxPermSize=512m`
- `GWT`：`-Xms512m -Xmx1280m -XX:PermSize=256m -XX:MaxPermSize=512m`
- `GWT`大内存配置：`-Xms2048m -Xmx2048m -XX:PermSize=256m -XX:MaxPermSize=512m`

`IDEA`常用内存参数配置，每次配项目都是去查笔记，`ctrl+c,ctrl+v`...
