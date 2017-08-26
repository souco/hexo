---
title: 常用Git命令
date: 2017-04-12 17:15:03
category: Git
tags: Git
---
- `git init` 初始化 `Git`
- `git add README.md` 将文件添加到暂存区域
- `git add .` 将当前目录下的所有文件添加到暂存区域
- `git commit -m "add a readme file"` 将文件提交到`Git`仓库
- `git clone https://github.com/n0tr00t/Sreg` 克隆`GitHub`上别人的项目
- `git commit -am "change the license file"` 一步实现`add`和`commit`
- `git reset HEAD~` 把`Git`仓库的文件还原到暂存区域
- `git checkout` 把暂存区域的文件还原到工作目录
- `git log` 查看历史提交记录
- `git reset 11c2929` 回滚到特定`ID`的快照
- `git reset --hard 31f46be` 根据快照`ID`往前滚
- `git reflog` 查看每次执行完命令，`HEAD`指向的版本号
- `git commit --amend -m "新的提交说明"` 修改最后一次提交
- `git rm test.py` 删除工作目录和暂存区域的文件（取消跟踪）
- `git checkout -- README.md` `checkout`单个文件
- `git mv game.py wordgame.py`  重命名文件
- `git branch feature` 创建分支
- `git log --decorate [--oneline]` 查看当前分支情况[`oneline`单行查看]
- `git log --oneline --decorate --graph --all` 查看系统分支情况[`graph`绘制分支图,`all`显示所有分支]
- `git checkout feature` 切换分支
- `git merge feature` 合并`feature`分支
- `git checkout -b feature2` 创建一个新的分支`feature2`并`checkout`出来
- `git branch -d feature2` 删除`feature2`分支
- `git branch -D feature` 当`feature`分支当中有未合并的内容，也强行删除`feature`分支
- `git checkout HEAD~` 切换到匿名分支（当前版本上一个版本）

### 关于提交代码到`GitHub`
- `git remote add origin git@github.com:yourName/yourRepo.git` 添加远程地址到当前仓库

### 详谈`checkout`命令
- `git checkout HEAD~ README.md` 当给定某个文件名时，Git 会从指定的提交中拷贝文件到暂存区域和工作目录
- `git checkout README.md` 如果命令中没有给定具体的快照 ID ，则从暂存区域回复指定文件到工作目录
- `git checkout --README.md` 如果存在`README.md`分支的话，指定恢复文件，而不是切换分支


### 其他说明
- `git status`命令时显示`On branch master`说明我们位于一个叫做`master`的分支里，这是默认的分支。
- `git reset HEAD~`命令中的`HEAD~`表示`HEAD`的上一个版本，如`HEAD~~`表示`HEAD`的上上个版本，`HEAD~~~`表示`HEAD`的上上个版本，`HEAD~10`表示`HEAD`之前第10个版本。
- `git reset --soft HEAD~`表示只移动`HEAD`的指向，但并不会将快照回滚到暂存区域。（相当于撤销上一次的提交）
- `git reset [--mixed(默认，可省略)] HEAD~`将快照回滚到暂存区域。
- `git reset --hard HEAD~`表示不仅移动`HEAD`的指向，将快照回滚到暂时区域，它还将暂存区域的文件还原到工作目录。
- `git commit --amend`如果后面不附加提交说明的话，会进入修改说明的页面。可以使用快捷键`Shift + z + z`或者`：q！`退出。
- `git rm -f test.py`要删除的文件在当前工作目录和暂存区域的内容不一致时，删除会跳出提示，此时添加`-f`参数即可。
- `git rm --cache test.py`删除暂存区域的文件（保留工作目录的）。
- `echo *.temp > .gitignore` 创建一个`.gitignore`文件，并让 `Git` 忽略所有的`.temp`后缀的文件。
- `develop`开发分支，`feature`功能分支，`release`预发布分支，`hotfix`维护分支。
- `reset`会移动`HEAD`所在分支的指向，而`checkout`命令只会移动`HEAD`自身来指向另一个分支。所以，`checkout`命令更加安全。

