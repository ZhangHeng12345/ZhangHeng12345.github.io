---
layout: post
title:  "NCL等值线图(contour)笔记"
categories: NCL
tags: NCL
author: Heng
---

* content
{:toc}



## 设置地理范围
```
res@mpLimitMode = "LatLon"
res@mpMinLatF               = 0.
res@mpMaxLatF               = 30.
res@mpMinLonF               = 110.
res@mpMaxLonF               = 230.
```
## 马赛克填充
```
res@cnFillMode        ="RasterFill"
res@cnRasterSmoothingOn = True
```
