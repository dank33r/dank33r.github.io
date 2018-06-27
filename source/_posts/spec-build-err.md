---
title: SPEC2007 127.wrf2 build error
date: 2018-06-22 18:38:54
tags: PMPI
categories: MPI
---

### SPEC2007 127.wrf2 gfortran build error

rsl_mpi_compat.c中第112行.
```
xargc = iargc_()+1;
```
改为
```
xagc = _gfortran_iargc()+1;
```