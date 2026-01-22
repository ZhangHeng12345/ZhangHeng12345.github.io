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
## 坐标轴数值
```
 cnres@sfXArray=lat_aux_grid
 cnres@sfYArray=moc_z/100
 cnres@gsnYAxisIrregular2Linear=True ;Most vertical axis are irregular. We can display them as a linear axis by setting gsnYAxisIrregular2Linear = True
 cnres@trYReverse=True               ;倒转Y轴
```
```
 ;cnres@tmYLMode              = "Explicit"
 ;cnres@tmYLValues            = (/0,1000,2000,3000,4000,5000/)
 ;cnres@tmYLLabels            = "" + cnres@tmYLValues
```
