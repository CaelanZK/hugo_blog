---
title: "记一次OpenStack模板机安装"
subtitle: ""
date: 2020-02-25T19:22:29+08:00
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
- 云计算
- OpenStack
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

## 什么是云计算？  
- 云计算是通过虚拟化计算去实现的，他是一种按量付费的模式！！  
- ksm内存压缩技术，内存压缩、超卖  

### 云计算服务类型  
- IAAS：基础设施即服务（infrastructure） ESC云主机、自己部署环境，自己管理代码  
- PAAS：平台即服务（platform） 提供软件的运行环境php、java、python、go、c#、nodejs等；自己管理代码  
- SAAS：软件即服务（software） 企业邮箱、cdn、rds 
 
#### IAAS有哪些功能？  
- kvm虚拟化的管理平台，使用数据库来统计，统一管理资源和计费等。  
  
### 云计算相关架构  

- MVC（model view control）一个站点把所有的东西都运行起来  
- SOA（拆架构） 千万级用户同时访问；把各项功能拆分成一个独立web服务，每一个独立的web服务都拥有至少一个集群  
- 微服务： 亿级用户； 开源eg：阿里云dubbo、spring boot 
>openstack（SOA架构）：属于云计算IAAS，使用apache2.0开源协议  
>
>自动化代码上线：Jenkins + gitlab ci  
> 
>自动化代码质量检查：sonarqube  


## 安装模板机
- 在CentOS安装运行之前的界面`Tab`键修改内核
``` shell
quiet net.ifnames=0 biosdevname=0
```
- 简要安装过程  
网络-时间-语言-最小安装-手动分区-关闭内核备份
## 优化模板机
- 修改ip
``` shell
vi /etc/sysconfig/network-scripts/ifcfg-eth0

TYPE=Ethernet
BOOTPROTO=none
NAME=eth0
DEVICE=eth0
ONBOOT=yes
IPADDR=10.0.0.11
NETMASK=255.255.255.0
GATEWAY=10.0.0.254
DNS1=233.5.5.5
```
- 关闭防火墙
``` shell
systemctl stop firewalld
systemctl disable firewalld
```
- 关闭selinux
``` shell
setenforce 0                 #临时关闭
getenforce                   #查看

vi /etc/selinux/config       #永久关闭
=disable
```
- ssh优化
``` shell
vi /etc/ssh/sshd_config
/set number                  #显示行号
GSSAPIAuthentication no      # /79
UseDNS no                    # /115
systemctl restart sshd       #重启sshd
```
- hosts优化
``` shell
vi /etc/hosts

10.0.0.11 controller
10.0.0.31 compute1
```
- 配置本地yum源
``` shell
umount /mnt                  #取消光盘挂载
cd /etc/yum.repo.d/
mkdir bak -p                 #创建备份文件夹
mv *.repo test               #一键创建本地yum源；注意file后有三个`/`;在出错的时,`\`后的命令可以重新执行
\echo '[local]
> name=local
> baseurl=file:///mnt      
> gpgcheck=0'>local.repo

mount /dev/cdrom /mnt        #进行挂载
yum makecache
```
- 关闭网卡图形化设置管理，统一使用network管理，管理不一致容易造成冲突
``` shell
systemctl stop NetworkManager.service
systemctl disable NetworkManager.service
```
- 安装tab补全
``` shell
yum install -y bash-completion.noarch
```
- 安装常用命令
``` shell
yum install -y vim lrzsz wget tree screen lsof tcpdum
```
- 关闭邮件服务
``` shell
systemctl stop postfix.service
systemctl disable postfix.service
```
- 模板机优化完成，关机
``` shell
shutdown -h now
```
## 相关摘要
在一次老基友[`@阿Fei`](111.229.73.54)的带动下，初次接触此框架，根据B站[老男孩](https://www.bilibili.com/video/av80759575?p=12)相关视频进行学习整理的备忘。
