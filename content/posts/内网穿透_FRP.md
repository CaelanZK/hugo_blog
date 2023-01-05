---
title: "内网穿透 FRP"
subtitle: ""
date: 2020-03-02T21:40:50+08:00
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
- 内网穿透
- FRP
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

## 什么是FRP？  
`FRP`是一个可用于内网穿透的高性能的反向代理应用，支持 tcp, udp 协议，为 http 和 https 应用协议提供了额外的能力，且尝试性支持了点对点穿透，有了它就可以在本地搭建环境通过公网进行测试，是不是很棒。

<!--more-->

FRP架构如下  
<!-- ![frp-architecture.png](https://uss.useenet.cn/2020/03/22/5c915f8182b9d.png)   -->
{{< image src="https://uss.useenet.cn/2020/03/22/5c915f8182b9d.png" caption="frp-architecture" >}}
- frps为服务端，使用它的公网地址作为中转
- frpc为客户端，配置完成后可以使用公网访问内网资源


## FRP的部署
### 前期准备
- 带固定公网IP的VPS一台
- 如果没有的小伙伴可以自配一台，推荐[Vultr](https://www.vultr.com/?ref=8452616-6G)、[阿里云](https://www.aliyun.com/minisite/goods?userCode=ghpvyny5)、[腾讯云](https://url.cn/56NA2Et);活动力度比较大，Vultr为推广链接，新用户注册有赠送 100$；腾讯阿里云新用户购买最低1折起，所以需要的可以看一下。

> *PS：已有VPS接着步骤继续往下*
## 设置服务端
### 根据自己的系统下载`frp`，并进行解压缩  
<!-- - [官方Github链接](https://github.com/fatedier/frp/releases)
-->
{{< link href="https://github.com/fatedier/frp/releases" content="frp github release" card=true >}}
### 上传文件
- 通过XShell等将frps、frps.ini上传至有公网地址的服务器上；我这里使用的是MobaXterm，可以直接拖拽上传
### 直接最小配置启动  
``` shell
cd /usr/frps            #进入存放目录
./frps -c ./frps.ini    #最小执行
```
>若提示：`-bash: ./frps: No such file or directory`则表示无此文件或者执行权限不足
``` shell
chmod +x frps
```  
- 将frps注册为服务项，可以上传解压缩包中的`systemd/frps.server`至服务器`/lib/systemd/system/`文件夹中
``` shell
systemctl daemon-reload
```
### 设置服务自启动
``` shell
sudo systemctl enable frps.service
```
也可以通过修改`frps.ini`进行详细配置，通过 `reload` 重新加载  
``` shell
sudo systemctl reload frps.service
```

## 设置客户端
### 根据自己的系统下载frp，并进行解压缩；
<!-- - [官方Github链接](https://github.com/fatedier/frp/releases) -->
{{< link href="https://github.com/fatedier/frp/releases" content="frp github release" card=true >}}
### 将 frpc、frpc.ini 放置在内网设置目录中

### 修改配置文件  
``` shell
cd /usr/frpc    #进入存放目录
```
### 编辑配置文件：
``` shell
vim frpc.ini     #内容如下（此处以ssh为例）

[common]
server_addr = 服务器公网 IP
server_port = 7000
[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 7003
```
### 赋权执行
``` shell
chmod +x frpc
./frpc -c ./frpc.ini    
```
- 注册为服务项，上传解压缩包中 `systemd/frpc.server` 至内网设备 `/lib/systemd/system/` 文件夹
``` shell
systemctl daemon-reload
```
### 自启动
``` shell
sudo systemctl enable frpc.server
sudo systemctl start frpc.server
```
### 远程访问测试
SSH  
<!-- ![frp-ssh.png](https://uss.useenet.cn/2020/03/22/b180ccc33c8fe.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/b180ccc33c8fe.png" caption="frp-ssh" >}}
- 详细配置说明可以参考解压缩包中的 `frpc/s_full.ini`
<!-- - 另外也可以参考frp的官方[README](https://github.com/fatedier/frp/blob/master/README_zh.md) -->
- 另外也可以参考frp的官方README
{{< link href="https://github.com/fatedier/frp/blob/master/README_zh.md" content="FRP README" card=true >}}
