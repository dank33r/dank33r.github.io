---
title: Unpack RPM package
date: 2018-06-22 19:08:43
tags: 实用技巧
categories: 操作系统
---

To extract RPM file using rpm2cpio and cpio command, type:

```bash
$ rpm2cpio your_rpm.x86_64.rpm | cpio -idmv
```