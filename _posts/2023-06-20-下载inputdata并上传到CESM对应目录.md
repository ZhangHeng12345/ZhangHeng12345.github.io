---
layout: post
title:  "下载inputdata并上传到CESM对应目录"
categories: CESM 
tags: CESM inputdata python
author: Heng
mathjax: true
---

* content
{:toc}

因为大部分的机器不能连外网，所以check_inputdata --download的功能一般用不了，需要自己去重新下载这些inputdata。<br>

转自[CESM笔记——porting-新机器移植](https://blog.csdn.net/qq_27984679/article/details/107118480)<br>
下载[inputdata](https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/)<br>




## 下载inputdata

`./case.build`之后，在`$case/Buildconf`下会生成各模块需要的inputdata文件<br>
- 首先, 将各文件合并<br>
```
cat *list >all_list
```

- 用python将all_list转成all_list-short(去掉`inputdata/`之前的字符并替换为`https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/`)<br>
```
   f = open('all_list', 'r')
   f1 = open('all_list-short','w')
   for (num,value) in enumerate(f):
       head,sq,tail=value.partition('inputdata/')
       print ("line number", num+1, "is:", tail)
       str0='https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/'
       directory=str0+tail
       print ("line number", num+1, "is:", directory)
       f1.write(directory)
  f1.close()
  f.close()
```

- 用wget下载
```
wget --no-check-certificate -c -i all_list-short
```

- 移动文件到正确目录
```
f  = open('all_list-short.txt', 'r')
for (num,value) in enumerate(f):
    print ("line number", num+1, "is:", value)
    head,sq,tail=value.partition('inputdata/')
    list0=tail.strip().split('/')
    list1=list0[0:-1]
    str0='/'
    directory='./'+str0.join(list1)
    print(directory)
    if not os.path.exists(directory):
        os.makedirs(directory)
    filename=list0[-1].strip()
    if not os.path.exists(filename):
        print(filename+' do not exist')
        continue
    print(filename+' do exist, begin move')
    os.popen('mv '+filename+' '+directory)
f.close()
```

