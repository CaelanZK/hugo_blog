---
title: "Ubuntu apt upgrade报错"
subtitle: ""
date: 2020-02-29T18:01:09+08:00
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
- Linux
- Ubuntu
categories:
- 运维

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

## 报错情况
再使用`sudo apt-get update && apt-get upgrade`更新时最后出现两个Error

``` shell
E: Could not get lock /var/lib/dpkg/lock - open (13: Resource temporarily unavailable)   
E: Unable to lock the administration directory (/var/lib/dpkg/), are you root ? 
```


## 解决办法：
``` shell
sudo rm -rf /var/lib/dpkg/lock-frontend  
sudo rm -rf /var/cache/apt/archives/lock  
sudo apt-get update  
sudo dpkg --configure -a
```
