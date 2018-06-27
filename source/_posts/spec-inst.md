---
title: Spec2007 Install
date: 2018-06-22 18:07:26
tags: PMPI
categories: MPI
---

### Install

1. We need get latest SPEC2007 package; for now it is version 2.0. ISO and tar ball both work well. I have download them under following location.

```bash
> ls /scratch/dev9/lchen/spec2007/ -lh
total 4.6G
-rw-r--r-- 1 pmpibot lsf 2.4G Jan 17  2010 mpi2007-2.0.iso
-rw-r--r-- 1 pmpibot lsf 2.3G Jan 17  2010 mpi2007-2.0.tar.bz2
```

2. Mount ISO or untar the tar ball.

```bash
> sudo mount -o loop mpi2007-2.0.iso your_dir
```
or
```bash
> tar jxvf mpi2007-2.0.tar.bz2
```

3. Change to SPEC2007 source directory and run install.sh.

```bash
> cd your_dir
> ./install.sh -d dest_dir
```
<!--more-->
### Build

1. Before build SPEC2007, you need install PMPI7.x/8.0, OpenMPI and Scali-MPI(PMPI5.6.7). After install complete you need source the environment. In rest of "build" section we will use PMPI8.0 as an example.

2. Setup compile environment. Suppose you installed SPEC2007 at /pmpi/work/lchen/spec2007v2 and using Intel compiler on AMD64 platform, then you need go following steps.

```bash
> source /pcc/app/intel_compiler/11.1/bin/ifortvars.sh intel64 (suppose you're using bash)
> source /pcc/app/intel_compiler/11.1/bin/iccvars.sh intel64
> cd /pmpi/work/lchen/spec2007v2
> source shrc
```

3. Save following configuration files in $SPEC/config directory.

```bash
> cat pmpi8_amd64.cfg
action=build

%define CMD_PREFIX ulimit -s 326780;
absolutely_no_loecking=0

tune=base
env_vars=1
makeflags = -j 4
ext=pmpi8

FC = mpif90 -mpif90 ifort
CC = mpicc -mpicc icc
CXX= mpiCC -mpicxx icpc

medium=default=default=default: 
BOPTS= -O3 -ipo -IPF_fp_relaxed 

COPTIMIZE = ${BOPTS} 
FOPTIMIZE = ${BOPTS}
CXXOPTIMIZE = ${BOPTS}
EXTRA_LDFLAGS= -i-static

use_submit_for_speed=1

121.pop2:
CPORTABILITY= -DSPEC_MPI_CASE_FLAG

127.wrf2:
CPORTABILITY =  -DSPEC_MPI_CASE_FLAG  -DSPEC_MPI_LINUX 

include: app_pmpi8_amd64.cfg

> cat app_pmpi8_amd64.cfg

medium=base=default=default:

%if !defined(%{MPIRUN_OPTIONS})
%define MPIRUN_OPTIONS
%endif

%if !defined(%{CMD_PREFIX})
%define CMD_PREFIX
%endif

%warning using MPIRUN_OPTIONS %{MPIRUN_OPTIONS}


%ifdef %{appfile}

%warning using appfile mode
submit= \$SPEC/rungenappfile $command >appfile ; %{CMD_PREFIX} \$MPI_ROOT/bin/mpirun %{MPIRUN_OPTIONS}  -f appfile


%elif defined(%{hostfile})
%warning using hostfile mode
%if '%{hostfile}' eq '1'
%define machfile machinefile
%else
%define machfile %{hostfile}
%endif

submit= %{CMD_PREFIX} \$MPI_ROOT/bin/mpirun %{MPIRUN_OPTIONS} -np $ranks -hostfile \$SPEC/%{hostfile} $command

%elif defined(%{cmdline})

%warning using cmdline mode
submit= %{CMD_PREFIX} \$MPI_ROOT/bin/mpirun -np $ranks %{MPIRUN_OPTIONS} -lsb_mcpu_hosts $command

%else
%warning exit without run
%endif
```

4. Run following command in $SPEC and it will build medium dataset for SPEC2007.

```bash
> runspec --config=pmpi8_amd64 medium
```

### Run benchmark with PMPI

You can issue following commands to run SPEC2007.

```bash
> cd $SPEC
> runspec --config=pmpi8_amd64 --action=run -I --size mref --iterations=1 --ranks 16 --define hostfile=hosts medium
```

Above command suppose you're running medium suite 1 time with pmpi8_amd64.cfg as configuration file and using mtest data size. The benchmark will run 16 ranks on all hosts which your "hosts" defined. The "hosts" file must under $SPEC directory and with following format.

```bash
> cat hosts
host1
host2
host3
host4
```

### Run benchmark with OpenMPI

Please save following configuration in your config directory and then issue "runspec --config=openmpi_amd64 medium" to run benchmark with medium date suite.

```bash
> cat config/openmpi_amd64.cfg
%define CMD_PREFIX ulimit -s 326780;
absolutely_no_locking=0

tune=base
env_vars=1
makeflags = -j 4
ext=openmpi

FC = mpif90
CC = mpicc
CXX= mpiCC

medium=default=default=default: 
BOPTS= -O3 -ipo -IPF_fp_relaxed 

COPTIMIZE = ${BOPTS} 
FOPTIMIZE = ${BOPTS}
CXXOPTIMIZE = ${BOPTS}
EXTRA_LDFLAGS= -i-static

use_submit_for_speed=1

submit=mpirun --hostfile hosts -np $ranks $command 

> runspec --ranks 16 --size mref --config=openmpi_amd64 medium
```

### Run benchmark with ScaliMPI

Please save following configuration in your config directory and then issue.