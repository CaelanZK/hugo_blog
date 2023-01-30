---
title: "PVE安装OpenWrt"
subtitle: ""
date: 2023-01-29T22:47:47+08:00
authorLink: ""
authorEmail: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- PVE
- OpenWRT
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
## 创建虚拟机

1. 操作系统处选择`不使用任何介质`
   <!-- ![](https://uss.useenet.cn/picgo/note/202301292350186.png) -->
{{< image src="https://uss.useenet.cn/picgo/note/202301292350186.png" caption="选不使用任何介质">}}

2. 按需修改磁盘大小
   <!-- ![](https://uss.useenet.cn/picgo/note/202301292348448.png) -->
{{< image src="https://uss.useenet.cn/picgo/note/202301292348448.png" caption="按需修改磁盘大小">}}

3. 配置按需进行分配
   <!-- ![](https://uss.useenet.cn/picgo/note/202301292356744.png) -->
{{< image src="https://uss.useenet.cn/picgo/note/202301292356744.png" caption="配置按需进行分配">}}

4. 选中硬盘并分离
   <!-- ![](https://uss.useenet.cn/picgo/note/202301300003809.png) -->
{{< image src="https://uss.useenet.cn/picgo/note/202301300003809.png" caption="选中硬盘并分离">}}

5. 选中为使用磁盘并删除
   <!-- ![](https://uss.useenet.cn/picgo/note/202301300007882.png) -->
{{< image src="https://uss.useenet.cn/picgo/note/202301300007882.png" caption="选中为使用磁盘并删除">}}

6. 接下来就是`下载/上传`镜像到PVE上

## 镜像处理

1. 下载镜像

```bash
wget https://op.supes.top/releases/targets/x86/64/openwrt-01.10.2023-x86-64-generic-squashfs-combined.img.gz
```

2. 解压缩得到`.img`镜像文件

```bash
gunzip ./openwrt-01.10.2023-x86-64-generic-squashfs-combined.img.gz
```

3. 导入进刚新建的虚拟机中
  

```bash
# 重命名镜像，以便输入导入命令
mv ./openwrt-01.10.2023-x86-64-generic-squashfs-combined.img openwrt.img


# 导入镜像
qm importdisk 100 ./openwrt.img local
```

> 命令解析
> 
> - 100：表示`VM ID`，即虚拟机ID
>   
> - ./openwrt.img：表示当前所选镜像
>   
> - local：表示卷所导入的位置
>   

4. 选择好磁盘双击导入即可
  
   <!-- ![](https://uss.useenet.cn/picgo/note/202301300023736.png) -->
{{< image src="https://uss.useenet.cn/picgo/note/202301300023736.png" caption="选择好磁盘双击导入即可">}}

  
5. 完成后如下图
  
   <!-- ![](https://uss.useenet.cn/picgo/note/202301300102503.png) -->
{{< image src="https://uss.useenet.cn/picgo/note/202301300102503.png" caption="完成后如下图">}}

  

## 设置OpenWrt

1. 修改网络

```bash
vi /etc/config/network    # 修改IP
vi /etc/resolv.conf       # 修改DNS
```
2. 重启刷新配置
```bash
reboot
```