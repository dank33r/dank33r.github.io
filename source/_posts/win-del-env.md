---
title: Windows操作系统下删除环境变量
date: 2018-06-22 18:53:35
tags: 实用技巧
categories: 操作系统
---

在cmd中输入set test= 那是临时的，不会影响系统全局变量的。 以下两条命令可以保存为批处理也可手动在cmd上执行。

```
@Echo Off
Reg Delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v "TEST" /f 2>nul
Reg Delete "HKEY_CURRENT_USER\Environment" /v "TEST" /f 2>nul
Pause
```