---
title: 上传本地分支到github项目分支
date: 2018-06-27 20:25:31
tags: 实用技巧
categories: 操作系统
---

```
$ mkdir blog
$ cd blog
$ git init
$ git add .
$ git commit -a -m "The first commit."
$ git branch new_branch
$ git checkout new_branch
$ git remote add origin git@github.com:userid/project.git
$ git push origin new_branch
```