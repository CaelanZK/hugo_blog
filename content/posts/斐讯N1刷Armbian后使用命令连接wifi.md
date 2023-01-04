---
title: "斐讯N1刷Armbian后使用命令连接wifi"
subtitle: ""
date: 2019-12-29T20:52:16+08:00
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
- N1
- Armbian
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

## 前言
>斐讯N1，断开网线后开机自启连接wifi使用
>
>*PS：连接WiFi时要在有线连接的情况下进行，在wifi下设置连接wif会导致当前wifi断线导致无法继续配置。*

<!--more-->

## 方法一：进入设置修改

``` shell
armbian-config        #依次选择network ——> wifi
```
- *详见下图选择对应连接即可*   
![N1-network.jpg](https://uss.useenet.cn/2020/03/22/ceb55ad312dab.jpg)  
![N1-wlan.jpg](https://uss.useenet.cn/2020/03/22/5eb69399d1d3e.jpg)  
![N1-wifi.jpg](https://uss.useenet.cn/2020/03/22/f29bbd6c1cc58.jpg)  

## 方法二：编辑配置文件

输入命令有三个选项，其中前两项可以连接wifi，命令如下：
``` shell
sudo nmtui
```
- Edit a connection 可以进行配置网络，可以手动添加，wifi以及以太网都可  
![N1-NetworkManager.jpg](https://uss.useenet.cn/2020/03/22/7364825ee88a2.jpg)  
![N1-wifiadd1.jpg](https://uss.useenet.cn/2020/03/22/b8ad7f37f37d8.jpg)  
![N1-wifiadd2.jpg](https://uss.useenet.cn/2020/03/22/5041db6d39ef4.jpg)  

- Activate a connection，选择连接即可  
![N1-wificonnected.jpg](https://uss.useenet.cn/2020/03/22/83b859b9c91cc.jpg)

