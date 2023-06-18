---
layout: post
title:  "设置环境变量"
categories: Linux
tags: Linux Shell
author: Heng
---

* content
{:toc}

**基本语法**
1. export 变量名=变量值 (功能描述：将shell变量输出为环境变量/全局变量)
2. source 配置文件      (功能描述：让修改后的配置信息立即生效)
3. echo $变量名         (功能描述：查询环境变量的值)



   
```
vim /etc/profile
```
```
export TOMCAT_HOME=/opt/tomcat
echo "tomcat_home=$TOMCAT_HOME"
```
```
source /etc/profile
```
**Shell注释**
- 单行注释： `#`
- 多行注释：
```
:<<!
...注释内容...
！
