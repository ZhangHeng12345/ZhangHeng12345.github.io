---
layout: post
title:  "CESM2 spinup 平衡后重启(开始敏感性实验)"
categories: CESM
tags: CESM 重启
author: Heng
mathjax: true
---

* content
{:toc}





## 创建新的算例

```bash
./create_newcase --case /work/home/dhszh/cesm/cesm_case/box-sensit/PD-0Du1C-G1850ECO_T62_g37 --res T62_g37 --compset G1850ECO --mach sugon --compiler intel --run-unsupported
```

更改相关输出和inputdata路径
```bash
./xmlchange CIME_OUTPUT_ROOT=/work/home/dhszh/cesm/scratch/box-sensit
./xmlchange DOUT_S_ROOT=/work/home/dhszh/cesm/scratch/box-sensit/PD-0Du1C-G1850ECO_T62_g37
./xmlchange DIN_LOC_ROOT=/work/home/dhszh/CESM2-release-2.2.0/inputdata
./xmlchange DIN_LOC_ROOT_CLMFORC=/work/home/dhszh/CESM2-release-2.2.0/inputdata/atm/datm7
```

设置算例运行时间
```bash
./xmlchange STOP_OPTION=nyears,STOP_N=300,REST_OPTION=nyears,REST_N=300
```

为算例配置计算资源
```bash
./xmlchange NTASKS=144,NTASKS_OCN=288,ROOTPE_OCN=144
```



重启设置
```bash
./xmlchange RUN_TYPE=branch,RUN_REFCASE=PD-Control-G1850ECO-T62_g37-box_spinup,RUN_REFDATE=3800-01-01
```

## 模式设置

生成 user_nl_datm, $RUN目录等文件
```bash
./case.setup
```

修改user_nl_datm,设置读取的沙尘文件的时间为2000年
```bash
&shr_strdata_nml
  streams = "datm.streams.txt.CORE2_NYF.GISS 1 1 1",
      "datm.streams.txt.CORE2_NYF.GXGXS 1 1 1",
      "datm.streams.txt.CORE2_NYF.NCEP 1 1 1",
      "datm.streams.txt.presaero.clim_1850 2000 2000 2000"
/
```

修改读取的沙尘文件为0Dust1BC文件(0沙尘1黑炭)
```bash
# 生成需要用到的大气模块stream.txt文件
./preview_namelists
# 拷贝后修改需要读取到的气溶胶文件
cp CaseDocs/datm.streams.txt.presaero.clim_1850 user_datm.streams.txt.presaero.clim_1850
```

拷贝spinup的重启文件到$RUN目录
```bash
cp ~/cesm/scratch/box-initialization/PD-Control-G1850ECO-T62_g37-box_spinup/rest/3800-01-01-00000/* .
```

## 编译模式

```bash
./case.build
```

## 提交作业

```bash
./case.submit
```


