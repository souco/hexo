---
title: 采用html的a标签，href链接文件名为中文时无法下载解决方案
date: 2017-08-28 18:20:28
category: Java
tags: java
---
采用`html`的`a`标签，`href`链接文件名为中文时无法下载解决方案    

最简单的下载文件的方式，大家都清楚，是采用`html`中的a标签的`href`连接形式进行下载。只需要将文件的全路径赋值给`href`即可。但是这样的话，有的文件默认可以下载，有的则浏览器在网页上直接打开，有时候还会是乱码。这跟客户端没有关系，客户端完全是被动的，他在接收到`html`流的时候，分析报头，如果报头中指定了文件的下载方式，比如，为`excel`，则他就会弹框，提示用户是在线打开，还是说保存下载，如果报头中没有指定，浏览器就直接打开，这样对于特殊文件，很容易会产生乱码。所以为了避免这一点，需要在服务器端进行指定。  
如果采用程序开发向客户端输出流进行下载的话，很容易指定，如下
```java
response.setContentType("application/x-msdownload; charset=utf-8");
    if (request.getHeader("User-Agent").toLowerCase().indexOf("firefox") > 0)
        response.setHeader("Content-Disposition", "attachment; filename="
                + new String(filename.getBytes("UTF-8"), "ISO8859-1"));//firefox浏览器  
    else if (request.getHeader("User-Agent").toUpperCase().indexOf("MSIE") > 0)
        response.setHeader("Content-Disposition", "attachment; filename="
                + URLEncoder.encode(filename, "UTF-8"));//IE浏览器  
```

如果用`<a>`的连接的话，需要修改服务的设置，对于`tomcat`而言，查看`conf/web.xml`，寻找所有的`mime`类型，如果存在你需要下载的文件的话，即不用进行修改，如果不存在的话，需要添加，然后重启服务器，给`<a>`标签赋值要下载文件的全路径即可（比如`xls`的文件就不用修改配置，而`rar`就需要配置，`zip`也不需要配置）；注意，如果路径中包含中文的话，还需要稍微改动，否则可能会无法下载，需要在`Server.xml`文件中，在`http`端口设置处，需要加上编码，如下：
```xml
<Connector port="8282" protocol="HTTP/1.1"   
               connectionTimeout="20000"   
               redirectPort="8443"   
               URIEncoding="utf-8" />  
```
注意`URIEncoding`，之所以加上，是因为，针对`tomcat`而言，`tomcat`对于`get`方式请求过来的编码，是在这里进行配置的，对于`post`请求过来的编码解析方式，可以用传统的`request.setContent**`方式进行配置，所以文件路径中存在中文名，你必须得告诉服务器怎么解析，以什么样编码进行解析即可！