---
title: "斐讯K2P的简要刷机"
subtitle: ""
date: 2019-12-28T01:15:50+08:00
draft: false
author: "CaelanZK"
authorLink: ""
authorEmail: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- 斐讯
- K2P
- 路由器
- 刷机
categories:
- 捣鼓

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

## 起因
>斐讯就不用和大家多介绍了，wuwuwuwu,
>
>请了一周假返校考试，顺便回了一趟家，看到那K2P，想着就有点来气，转念一想，罢了先更新一波固件，看看有啥好玩的。

<!--more-->
## 刷机步骤
1. 下载固件，可以前往自行前往恩山查找
2. 找好一根网线，一端笔记本一端LAN口（记得断WAN口，以免影响进breed）
3. 进不死`breed`模式
4. 路由断电
5. 按住复位键
6. 插上电源5-10秒，事先笔记本输好 192.168.1.1 ，随后便进入breed
7. 恢复出厂设置，选择config公区
8. 固件更新，选中新固件上传即可
9. 刷新进入固件后，等待进入


## 待解决小问题
1. 刷入@lede大佬的固件，怎么安装frp功能  
2. 安装其他大佬的固件，有Frp不会用，一直显示未运行  
![K2P-frperror.jpg](https://uss.useenet.cn/2020/03/22/5e9d35d837166.jpg)
3. DropBear配置找了，使用XShell无法telnet，ssh  
![K2P-dropbear.jpg](https://uss.useenet.cn/2020/03/22/8add48003064e.jpg)
----------
## 后续更新
- FRP参见[内网穿透FRP](https://useenet.cn/archives/14.html)


