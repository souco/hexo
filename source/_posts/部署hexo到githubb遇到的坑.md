---
title: 部署hexo到github遇到的坑
date: 2017-04-06 19:02:31
category: 编程
tags: Git
---
其实 Hexo 的文档非常非常的详细。
但是我一开始其实不是对着 Hexo 的文档部署，因为还有一些别的步骤，例如部分 Git 和 GitHub 的相关申请配置等等。
所以遇到坑了吧。如下
1. 项目`deploy`到 GitHub 后，访问总是`404`
查了半天也没查出为啥。参照了别人的项目，发现少个`CNAME`文件，于是在 GitHub 加上去，结果成功了。郁闷的是重新发布过后又`404`了。看了下，`CNAME`文件又消失了。才想到每次生成网页，`hexo/public`下的文件都会被覆盖。于是查了下，不想被覆盖的内容需要放在`hexo/resource`目录下，如`CNAME`、`favo.icon`等文件。