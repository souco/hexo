---
title: 基于GithubPage的hexo博客搭建简明教程
date: 2017-08-26 17:25:23
tags: hexo
---
### 0.相关文档
hexo文档(https://hexo.io/zh-cn/docs/deployment.html)
NexT文档(http://theme-next.iissnan.com/)
### 1.安装 Node（必须）  
- 官网下载安装即可。
### 2.安装 Git（必须）  
- 官网下载安装即可。
### 3.申请 GitHub（必须）  
- 已有。
### 4.正式安装 HEXO
Node 和 Git 都安装好后执行如下命令安装 hexo ：
```
$ sudo npm install -g hexo
```
### 5.初始化
创建一个文件夹，如：Blog ，下文统称此目录为`/`，未提及则默认为此目录
在博客根目录下里执行 hexo init 的。命令：
```
hexo init
```
### 6.生成静态页面
```
hexo generate //（hexo g  简写）   
```
### 7.本地启动
```
hexo server () //（hexo s 简写）
```
### 8. 配置 NexT 主题
#### 8.1 下载主题
```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
#### 8.2 修改站点配置文件
打开站点配置文件（`config.yml`）,找到 theme 字段，并将其值更改为 next ,如：Blog
```
theme: next
```
#### 8.3 主题设定
##### 8.3.0 设置主题外观
```
#scheme: Muse
#scheme: Mist
scheme: Pisces
```
##### 8.3.1 设置侧栏
```
sidebar:
  position: left
  display: hide
```
##### 8.3.2 设置头像
将头像文件放置在`/themes/next/source/images/`下。修改主题配置文件
```
avatar: /images/filename.png //此处为你的文件名
```
#### 8.4 设置菜单及菜单页面
##### 8.4.1 在主题配置文件设置要显示的菜单:
```
menu:
  home: /
  categories: /categories/
  about: /about/
  archives: /archives/
  tags: /tags/
  sitemap: /sitemap.xml
  commonweal: /404/
```
##### 8.4.2 添加标签页
新建页面：
```
hexo new page tags
```
将生成的页面（`/source/tags/index.md`）的类型设置为 tags :
```
title: 标签
date: 2014-12-22 12:39:04
type: "tags"
---
```
##### 8.4.3 添加分类页
新建页面：
```
hexo new page categories
```
将生成的页面（`/source/categories/index.md`）的类型设置为 categories :
```
title: 标签
date: 2014-12-22 12:39:04
type: "categories"
---
```
##### 8.5 配置友情链接
在主题配置文件中：
```
links:
  baidu: https://www.baidu.com
```
### 配置搜索
安装 `hexo-generator-searchdb`，在站点的根目录下执行以下命令：
```
$ npm install hexo-generator-searchdb --save
```
编辑站点配置文件，新增以下内容到任意位置：
```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```
编辑 主题配置文件，启用本地搜索功能：
```
# Local search
local_search:
  enable: true
```

### 站点配置
以下都是基于站点配置文件（`config.yml`）
- 配置语言为简体中文
```
language: zh-Hans
```

###配置提交到 github 的信息
在站点配置文件下：
```
deploy:
  type: git
  repo: git@github.com:***/***.github.io.git
  branch: master
  message: article update {{ now('YYYY-MM-DD HH:mm:ss') }}
```