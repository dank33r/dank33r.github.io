---
title: PMPI Fortran 90
date: 2018-06-22 17:44:36
tags: PMPI
categories: MPI
---

### PMPI Fortran 90 for Linux

To use the 'mpi' Fortran 90 module, you must create the module file by compiling the module.F file in /opt/platform_mpi/include/64/module.F for 64-bit compilers. For 32-bit compilers, compile the module.F file in /opt/platform_mpi/include/32/module.F.
<!--more-->
### Notes:

Each vendor (e.g., PGI, Qlogic/Pathscale, Intel, Gfortran, etc.) has a different module file format. Because compiler implementations vary in their representation of a module file, a PGI module file is not usable with Intel and so on. Additionally, forward compatibility might not be the case from older to newer versions of a specific vendor's compiler. Because of compiler version compatibility and format issues, we do not build module files. In each case, you must build (just once) the module that corresponds to 'mpi' with the compiler you intend to use.

For example, with platform_mpi/bin and pgi/bin in path:
pgf90 -c /opt/platform_mpi/include/64/module.F

```bash
$ ls $MPI_ROOT/include/64/*.mod
/opt/ibm/platform_mpi/include/64/mpi_constants.mod
/opt/ibm/platform_mpi/include/64/mpi.mod
```
Example of hello_f90.f90

```
program main
use mpi
implicit none
integer :: ierr, rank, size
call MPI_INIT(ierr)
call MPI_COMM_RANK(MPI_COMM_WORLD, rank, ierr)
call MPI_COMM_SIZE(MPI_COMM_WORLD, size, ierr)
print *, "Hello, world, I am ", rank, " of ", size
call MPI_FINALIZE(ierr)
End
```

Run it:

```bash
$ mpif90 -mpif90 pgf90 hello_f90.f90
$ mpirun ./a.out
Hello, world, I am 0 of 1
```
