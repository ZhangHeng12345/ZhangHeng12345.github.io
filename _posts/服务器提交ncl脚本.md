---
layout: post
title:  "Vim命令"
categories: 
tags: Blog
author: Heng
mathjax: true
---

* content
{:toc}


#1. 新建run.sh任务脚本
```
#! /bin/bash
#SBATCH -p xahcnormal
#SBATCH -J ncl
#SBATCH -n 1
#SBATCH -o job.out

module load ncl_ncarg/6.5.0-gcc-4.8.5
module load mpi/openmpi/openmpi-3.1.6
mpirun -n 1 ncl ncl_amoc.ncl

`#SBATCH -p`,申请队列名   
`#SBATCH -J`,自定义任务名   
`#SBATCH -n`,申请核数   
`#SBATCH -o`，程序的运行输出保存在`job.out`
```
#2. 提交计算任务
```
[user@login01 tmp]$ sbatch run.sh
Submitted batch job 3656
```
3. 查看程序实时输出
```
[user@login01 tmp]$ tail -f job.out 
 Copyright (C) 1995-2019 - All Rights Reserved
 University Corporation for Atmospheric Research
 NCAR Command Language Version 6.6.2
 The use of this software is governed by a License Agreement.
 See http://www.ncl.ucar.edu/ for more details.
```
参考[国超无锡ncl 使用指南](http://doc.nsccwx.cn/ncl/)
