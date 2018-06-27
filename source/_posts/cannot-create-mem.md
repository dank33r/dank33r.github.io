---
title: Cannot create shared memory segment of N bytes problem
date: 2018-06-22 18:22:21
tags: PMPI
categories: MPI
---

### MPID: Cannot create shared memory segment of N bytes problem

To increase the shared memory size to 256 MB, for example, as root, edit the /etc/sysctl.conf file by modifying or adding the line:
```
kernel.shmmax=268435456
```

To increase the shared memory size without rebooting, use:
```
% /sbin/sysctl -w kernel.shmmax=1684354560
```
<!--more-->
If you have your kernel configured with the /proc file system and it is mounted, then the current maximum shared memory segment size (in bytes) can be viewed by the following command:
```
% cat /proc/sys/kernel/shmmax
```