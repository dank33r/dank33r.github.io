---
title: Github上fork出来的项目与上游分支同步
date: 2018-06-25 23:03:31
tags: 实用技巧
categories: 操作系统
---


对于在Github上fork出来的项目，与master同步时可以考虑使用以下步骤。

1. 查看自己的远程分支，如果还没有设置上游分支那么设置需要同步的master为upstream。这个例子中由于我们还没有配置上游分支，所以需要添加fork项目的master为upstream。
```bash
➜  opencc git:(master) git remote -v
origin	https://github.com/yourname/opencc.git (fetch)
origin	https://github.com/yourname/opencc.git (push)

➜  opencc git:(master) git remote add upstream https://github.com/opencc/opencc.git
```
<!--more-->
2. 从上游仓库获取到分支及相关的提交信息，并将它们保存在本地的upstream/master分支。
```bash
➜  opencc git:(master) git fetch upstream
```

3. 把upstream/master分支合并到本地的master，这时本地master分支便与上游仓库保持同步了，并且没有丢失本地的任何修改。
```bash
➜  opencc git:(master) git merge upstream/master
➜  opencc git:(master) git push
```