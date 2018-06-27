---
title: PMPI算法选择表
date: 2018-06-22 18:16:30
tags: PMPI
categories: MPI
---

### 生成算法选择表

```bash
$ mpirun -IBV -hostlist hb05b01:8,hb05b02:8,hb05b03:8,hb05b04:8,hb05b05:8,hb05b06:8,hb05b07:8,hb05b08:8 -aff=automatic:latency -e PCMPI_SYSTEM_CHECK=BM -e MPI_COLL_OUTPUT_FILE=scatter64r.dat -e MPI_COLL_OUTPUT_FILE_ASCII=scatter64r.imb -e MPI_COLL_OUTPUT_FILE_ORDER=scatter64r.c -e MPI_OPTIONAL=allow_ascii -e MPI_COLL_PRINT=1 sc
```
<!--more-->
### 使用生成的算法选择表

```bash
$MPI_ROOT/bin/mpirun –e PCMPI_COLL_BIN_FILE=<file> ./a.out
```

MPI_COLL_BM_TEST_COLL = only algorithm to test