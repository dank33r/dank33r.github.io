---
title: PMPI Connection closed by remote host issue
date: 2018-06-22 18:00:10
tags: PMPI
categories: MPI
---

### PMPI - "ssh exchange identification: Connection closed by remote host" issue

#### Description

Some time when we need start many mpid using ssh the system will complain 'ssh_exchange_identification: Connection closed by remote host' error. For example issues following command, on hpgpu01 and hpgpu02 there are 12 cores each.

```bash
$ mpirun -np 24 -hostlist hpgpu01,hpgpu02 hw
```
<!--more-->
#### Solutions

1) Change "MaxStartups" to values more than "10" in /etc/ssh/sshd_config.

```
MaxStartups 1000
```

2) Define a small value less than 20 of MPI_MAX_REMSH.