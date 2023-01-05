---
title: "Docker OpenWrt的安装与使用"
subtitle: ""
date: 2020-01-04T13:37:00+08:00
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
- Docker
- OpenWRT
- 斐讯
- N1
categories:
- 捣鼓
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
## 前提条件：刷好`armbian`并安装好`docker`之后
> N1安装docker教程：[飞机直达](https://www.useenet.cn/archives/27/)
## 使用以下命令拉取镜像；或者手动导入
> 恩山Flippy大佬网盘地址：[飞机直达](https://pan.baidu.com/s/1a-nvQNCo8JWNbCnWZazOtw#f9ve)

<!--more-->

``` shell
# 拉取镜像
docker pull unifreq/openwrt-aarch64:latest

# 手动导入（命令对应下载的版本即可）
cd 上传所在目录
gzip -dc docker-img-openwrt-aarch64-r9.10.1.gz | docker load
```
## 开启网卡混杂模式`promisc`
``` shell
ifconfig eth0 promisc

# 查看是否开启
ifconfig eth0
eth网卡出现 PROMISC 表示开启成功

# 设置开机自启
sed -i '/exit 0/i\ifconfig eth0 promisc' /etc/rc.local
```
## 创建`macnet`网络
``` shell
# 一个eth0只能创建一个macvlan网络，清除原有的macnet，
docker network rm macnet

# 创建
docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 macnet

# 参数：
-d macvlan              # 创建类型为 macvlan 网络模式
--subnet                # 子网范围
--gateway               # 宿主机所在网关
-o parent=eth0          # option parent 为 eth0；继承 eth0
macvlan                 # 自定义网络名称
```
## 检查`macnet`网络
``` shell
docker network ls
docker network inspect macnet
```
## 创建`openwrt`容器并运行
``` shell
# 运行
docker run -d \
    --name=openwrt \
    --restart always \
    --privileged \
    --network macnet \
    --ip 192.168.1.100 \
    unifreq/openwrt-aarch64:latest

# 参数
-d                  # 后台运行
--name              # 设定该容器名字
--restart always    # 自启
--privileged        # 容器提权
--network           # 指定网络，此处使用自定义的名称 macnet
--ip                # 指定运行 ip，此处使用 192.168.1.100
```
## 修改`openwrt`网络配置
``` shell
# 运行openwrt的bash
docker exec -it openwrt bash

# 编辑openwrt的网络配置
vi /etc/config/network

# 在config interface 'lan'中
# 修改
option ipaddr '192.168.1.100'
#添加 
option gateway '192.168.1.1'    
option dns '192.168.1.1'

# 保存修改配置并重启网络
:wq
/etc/init.d/network restart

# 退出openwrt-bash
exit
```
![Docker-openwrt-network.png](https://uss.useenet.cn/2020/04/08/ffc09694980d5.png)
## 访问`docker-openwrt`
``` shell
浏览器访问：192.168.1.100
用户名：root
密码：password
```

> 参考文档：
>> [黎記 - N1 Docker 安装 OpenWrt](https://leeyr.com/326.html)
>> [恩山 - Flippy大佬docker发布页](https://www.right.com.cn/forum/thread-958173-1-1.html)