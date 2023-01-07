---
title: "使用python批量将xls转换xlsx"
subtitle: ""
date: 2020-07-30T23:23:30+08:00
draft: false
author: ""
authorLink: ""
authorEmail: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- Python
- 格式转换
- 脚本
categories:
- 编程

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []


# See details front matter: https://fixit.lruihao.cn/theme-documentation-content/#front-matter
---

<!--more-->
## 转换脚本如下
``` py
#coding=utf-8

import os
import os.path
import win32com.client as win32

#根目录
rootdir = 'D:\\AFile\\Document\\数据'
#三个参数：父目录；所有文件夹名（不含路径）；所有文件名
for parent, dirnames, filenames in os.walk(rootdir):
    for fn in filenames:
        if fn.endswith('xls'):
            filedir = os.path.join(parent, fn)
            print(filedir)
            print('xlsx转换中')
            excel = win32.gencache.EnsureDispatch('Excel.Application')
            wb = excel.Workbooks.Open(filedir)
            # xlsx: FileFormat=51
            # xls:  FileFormat=56
            wb.SaveAs(filedir + "x", FileFormat=51)
            wb.Close()
            excel.Application.Quit()
            print('xls-xlsx转换完成')
            print('='*100)

```

