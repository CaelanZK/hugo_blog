---
title: "Windows服务定时刷新启动"
subtitle: ""
date: 2019-12-14T13:27:40+08:00
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
- 脚本
- bat
categories:
- Windows

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
## 手动修改

>  有时要使用Windows服务时，出于某些特殊情况，总是很容易自动停止的情况，这个时候我们可以通过修改服务策略为自动；
- 点击`Win+R`输入`services.msc`即可打开服务
- 找到想要自启动的服务进行修改。

## 自动修改
> 好了，重点来了，若服务策略无法达到目的

我们就可以编写如下bat命令脚本

``` shell
@echo off
rem 定义循环间隔时间和监测的服务：
set secs=60
set srvname="servername"
echo.
echo ========================================
echo == 查询计算机服务的状态， ==
echo == 每间隔%secs%秒种进行一次查询， ==
echo == 如发现其停止，则立即启动。 ==
echo ========================================
echo.
echo 此脚本监测的服务是：%srvname%
echo.
if %srvname%. == . goto end
:chkit
set svrst=0
for /F "tokens=1* delims= " %%a in ('net start') do if /I "%%a %%b" == %srvname% set svrst=1
if %svrst% == 0 net start %srvname%
set svrst=
rem 下面的命令用于延时，否则可能会导致cpu单个核心满载。
ping -n %secs% 127.0.0.1 > nul
goto chkit
:end
```
- 编辑完成后保存为bat文件<br>
- 右键管理员运行即可