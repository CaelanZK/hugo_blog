---
title: "CentOS7最小安装基本配置"
subtitle: ""
date: 2019-12-28T00:55:09+08:00
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
- Centos
- Linux
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

<!--more-->

## 配置网络
修改路径
``` shell
vim /etc/sysconfig/network-scripts/ifcfg-ens33
``` 
修改内容
``` conf
PROTOCOL=dhcp          # dhcp为动态；static/none为静态
IPADDR= 
NETMASK= 
GATEWAY= 
ONBOOT=yes             # 开机启动
```

重启网络服务
``` shell
service network restart
```

## 配置SSH
检查是否安装ssh
``` shell
rpm -qa grep | ssh
```
安装SSH服务
``` shell
yum install -y openssh-server
```
修改配置文件
``` shell
# port 22     把前面#去掉，取消注释
```
重启ssh服务
``` shell
service sshd restart
```

## 一键更换阿里源
``` shell
sudo mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```
更换清华源：[清华源镜像文档](https://mirrors.tuna.tsinghua.edu.cn/help/centos/)

## 安装neofetch
___ps：方便查看配置___
``` shell
yum install dnf -y
yum install dnf-plugins-core -y
dnf -y copr enable konimex/neofetch
dnf install neofetch -y
```