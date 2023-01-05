---
title: "斐讯N1 Docker安装与卸载"
subtitle: ""
date: 2020-04-03T00:30:10+08:00
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
- 斐讯
- N1
- Docker
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

<!-- ![Docker.png](https://uss.useenet.cn/2020/04/03/5f95ad07151f5.png) -->
{{< image src="https://uss.useenet.cn/2020/04/03/5f95ad07151f5.png" caption="Docker">}}

## 阿里加速安装Docker

``` shell
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh --mirror Aliyun
```

- 如果遇到以下问题
``` shell
E: Could not get lock /var/lib/apt/lists/lock - open (11: Resource temporarily unavailable)
E: Unable to lock directory /var/lib/apt/lists/

# 解决
ps -A| grep apt
kill -9 进程ID
```
<!-- ![Docker-err.png](https://uss.useenet.cn/2020/04/08/55a702fc98478.png) -->
{{< image src="https://uss.useenet.cn/2020/04/08/55a702fc98478.png" caption="Docker报错">}}
## 配置阿里镜像加速器

<!-- [飞机直达](https://cr.console.aliyun.com/cn-shenzhen/instances/repositories) -->
{{< link href="https://cr.console.aliyun.com/cn-shenzhen/instances/repositories" content="阿里云镜像⏩" card=true >}}

> 页面如下  
<!-- ![Docker-ali.png](https://uss.useenet.cn/2020/04/03/ddf9f416d1229.png) -->
{{< image src="https://uss.useenet.cn/2020/04/03/ddf9f416d1229.png" caption="阿里Docker加速界面">}}

``` shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://系统分配前缀.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 安装Portainer管理界面
- 可以事先下载好汉化包，解压到`/public`
<!-- >> [飞机直达](https://uss.useenet.cn/2020/04/03/caa6746dc9e78.zip)-->
{{< link href="https://uss.useenet.cn/2020/04/03/caa6746dc9e78.zip" content="镜像下载" download="Portainer-CN.zip" card=true >}}
> [原作者主页](https://www.quchao.net/Portainer-CN.html) 

- 安装Portainer
``` shell
# 创建卷
docker volume create Portainer_data

# 新建汉化包文件夹,并自行上传汉化包到此文件夹
mkdir /public

# 运行
docker run -d \
    --name=Portainer \
    --restart always \
    -e TZ=Asia/Shanghai \
    -p 10000:9000 \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v Portainer_data:/data \
    -v /public:/public \
    portainer/portainer:linux-arm64
```
>命令解释
`-d`：后台运行
`--name Portainer`：容器名称
`--restart always`：开机自启
`-e TZ=Asia/Shanghai`：设定时区
`-p 10000:9000`：宿主机 10000 端口映射容器的 9000 端口
`-v /var/run/docker.sock:/var/run/docker.sock`：把宿主机的 Docker 守护进程 (Docker daemon) 默认监听的 Unix 域套接字挂载到容器中
`-v /public:/public`：Portainer汉化包目录
`-v Portainer_data:/data`：把宿主机 Portainer_data 数据卷挂载到容器 /data 目录


## 访问Portainer管理界面
>IP或域名`:10000`
PS：上方所涉及的目录地址与端口号了解相关操作的话均可自定义，注意创建好对应目录和开放端口即可

## Docker常用命令
``` shell
# 查看运行容器信息
docker ps

# 查看所有容器信息
docker ps -a

# 查看已安装镜像信息
docker images

# 启动、重启、停止
docker start xxx
docker restart xxx
docker stop xxx

# 卸载删除
docker rm 容器id
docker rmi 镜像id

# 查看Docker信息
docker info
```
## Docker 扩容
- U盘挂载
``` shell
fdisk -l                        # 查看磁盘情况
mkfs.ext4 /dev/sda              # u 盘是 sda，执行格式化 sda
mkdir /mnt/upan                 # 创建目录供挂载使用
mount -v /dev/sda /mnt/upan     # 挂载 U 盘
df -h                           # 查看挂载状态
umount -v /dev/sda              # 解除挂载
```
- 数据迁移
``` shell
# 停止Docker
service docker stop

# 创建目录
mkdir -p /mnt/upan/docker

# 拷贝数据
# -rpvb 递归/保留属性/覆盖/详细
cp -rpvb /var/lib/docker/* /mnt/upan/docker
mv /var/lib/docker /var/lib/docker.bak

# 软连接：实际 + 目标
ln -s /mnt/upan/docker /var/lib

# 恢复步骤，删除软连接（PS：尾部没有左斜杠 /）
#rm -rf /var/lib/docker

# 生效/启动
systemctl daemon-reload
service docker restart

# 验证
docker info | grep 'docker Root Dir'
#显示如下则迁移成功
Docker Root Dir: /mnt/upan/docker

# 重启自动挂载 U 盘，在 rc.local
sed -i '/exit 0/i\mount -v /dev/sda /mnt/upan' /etc/rc.local
```
## Docker玩法
<!-- > [恩山 - 四天](https://www.right.com.cn/forum/thread-911375-1-1.html) -->
{{< link href="https://www.right.com.cn/forum/thread-911375-1-1.html" content="N1玩法—————恩山@四天" card=true >}}

## 卸载
``` shell
sudo apt-get purge docker-*
sudo apt-get autoremove --purge docker-*
sudo rm -rf /var/lib/docker
sudo rm -rf /etc/docker

# 检查是否有遗留
whereis docker
```

## 参考文档：
{{< link href="https://leeyr.com/324.html" content="黎記 - N1 安装 Docker + GUI" card=true >}} 
<!-- >> [黎記 - N1 安装 Docker + GUI](https://leeyr.com/324.html) -->