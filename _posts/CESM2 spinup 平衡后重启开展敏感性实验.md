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
```sh
./create_newcase --case /work/home/dhszh/cesm/cesm_case/box-sensit/PD-0Du1C-G1850ECO_T62_g37 --res T62_g37 --compset G1850ECO --mach sugon --compiler intel --run-unsupported
```
