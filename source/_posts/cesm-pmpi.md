---
title: CESM Build
date: 2018-06-22 17:32:42
tags: PMPI
categories: MPI
---

### Create a new case

``` bash
create_newcase -case ../../test1 -res f45_g37 -compset X -mach platform -compiler intel
```

### Compiling with following options

```bash
cmake \
-D Trilinos_ENABLE_ALL_PACKAGES:BOOL=ON \
-D BUILD_SHARED_LIBS:BOOL=ON \
-D Trilinos_ENABLE_TESTS:BOOL=OFF \
-D CMAKE_C_FLAGS:STRING="-O3" \
-D CMAKE_CXX_FLAGS:STRING="-O3" \
-D CMAKE_INSTALL_PREFIX:PATH=/home/lchen/trilinos \
-D CMAKE_BUILD_TYPE:STRING=RELEASE \
-D BLAS_LIBRARY_DIRS=/home/lchen/lapack/lib \
-D LAPACK_LIBRARY_DIRS=/home/lchen/lapack/lib \
/pmpi2/lchen/cesm/trilinos-11.6.1-Source
```
<!--more-->
### No Fortran flags

```bash
CMAKE_Fortran_FLAGS:STRING=
```

### Compiling

```bash
./create_newcase -case ../../test1 -res f45_g37 -compset X -mach platform -compiler intel
./create_newcase -compset C -res T62_gx1v6 -mach 
platform -compiler intel -case ../../test2

FC=mpif90 CXX=mpiCC CC=mpicc CPPFLAGS='-DNDEBUG -Df2cFortran' CFLAGS=-O FFLAGS='-O -W' F90FLAGS="-I/pmpi/archive/9.1.2.0/Linux/RTM/exports/linux_amd64_gcc/include" ./configure --prefix=/home/lchen/pnetcdf --with-mpi=/pmpi/archive/9.1.2.0/Linux/RTM/exports/linux_amd64_gcc --host=ibmgpu05
```