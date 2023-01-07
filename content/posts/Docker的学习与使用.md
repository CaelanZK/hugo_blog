---
title: "Docker的学习与使用"
subtitle: ""
date: 2020-04-23T00:02:45+08:00
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
## 认识Docker

Docker 是一个开源的应用容器引擎，基于 Go语言 并遵从 Apache2.0 协议开源。  
Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。  
容器是完全使用沙箱机制，相互之间不会有任何接口，同时容器性能开销极低。

## 安装Docker

### CentOS

- 安装依赖

``` shell
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

- 添加阿里软件源

``` shell
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

- 更新并安装 Docker-CE

``` shell
sudo yum makecache fast
sudo yum -y install docker-ce
```

- 开启Docker服务

``` shell
sudo service docker start
```



### Ubuntu

- 更新并安装依赖

``` shell
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
```

- 安装GPG证书

``` shell
curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
```

- 添加阿里软件源

``` shell
sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable
```

- 更新并安装 Docker-CE

``` shell
sudo apt-get -y update
sudo apt-get -y install docker-ce
```



## 使用Docker

### Docker容器使用

1. 获取镜像

``` shell
docker pull ubuntu20.04
```

2. 启动容器（使用容器ubuntu中的bash）

``` shell
docker run -it ubuntu /bin/bash
exit								#退出终端
```

3. 查看所有容器 

``` shell
docker ps -a
```

4. 启动、停止、重启容器

``` shell
docekr start 容器ID
docker stop 容器ID
docekr restart 容器ID
```

5. 后台运行容器 

``` shell
docker run -itd --name ubuntu /bin/bash
```

6. 进入容器 

``` shell
docker attach 容器ID					#退出会导致容器停止 
docker exec -it 容器ID /bin/bash		#退出不会导致容器关闭
```

7. 导出容器 

``` shell
docker export 容器ID > ubuntu.tar
```

8. 导入容器

``` shell
cat docker/ubuntu.tar | docker import - test/ubuntu:v1
docker import http://example.com/exampleimage.tgz example/imagerepo
```

9. 删除容器 

``` shell
docker rm -f 容器ID
docker container prune				  #删除已停止容器
```



### Docker镜像使用

1. 查看所有镜像

``` shell
docker images

#选项说明：
REPOSITORY：镜像仓库源
TAG：镜像标签
IMAGE ID：镜像ID
CREATED：镜像创建时间
SIZE：镜像大小
```

2. 查找镜像 

```shell
docker search 镜像名
```

3. 拖取镜像 

``` shell
docker pull 镜像名
```

4. 删除镜像 

``` shell
docker rmi 镜像名
```

5. 创建镜像（更新现有镜像或重新构建）

- 创建更新镜像

``` shell
docker run -t -i ubuntu:20.04 /bin/bash
apt-get update
exit
docker commit -m="描述" -a="作者" 容器ID ubuntu:v2
```

- 构建镜像 

``` shell
docker build -t 需创建的镜像名
FROM ubuntu:20.04					    #指定使用的镜像源
MAINTAINER 维护人 “邮箱”			  #维护人员信息
RUN ······						      	#镜像内执行的操作
```

> PS：每一个指令都会在镜像上创建一个新的层，每一个指令的前缀都必须大写

- 设置镜像标签 

``` shell
docker tag 镜像ID tag名
```



### Docker容器连接

1. 网络端口映射 

``` shell
docker run -d -P training/webapp python app.py
docker run -d -p 8080:5000 training/webapp python app.py
docker run -d -p 127.0.0.1:8080:5000 training/webapp python app.py

#选项说明：
-P：容器内部端口 随机 映射到主机高端口
-p：容器内部端口绑定到 指定 的主机端口
```

2. 查看端口绑定 

``` shell
docker port training/webapp 5000
```

3. 创建网络

``` shell
docker network create -d bridge test-net			
docker network ls

#参数说明：
-d：参数指定Docker网络类型，bridge、overlay
```

4. 连接容器

``` shell
docker run -itd --name test1 --network test-net ubuntu /bin/bash			#运行一个容器并连接到新建的test-net网络
docker run -itd --name test2 --network test-net ubuntu /bin/bash			#打开新终端，再运行一个容器并加入到test-net网络
```

5. 配置docker全局DNS（重启后生效）

``` shell
vim /etc/docker/daemon.json

{
	“dns” : [
		“114.114.114.114”,
		“8.8.8.8”
		]
}
```



### Dockerfile

1. 什么是Dockerfile 

> Dockerfile是有个用来构建镜像的文本文件，文本中包含了一条条构建镜像所需要的指令和说明

2. Docker定制镜像

``` shell
mkdir Dockerfile
cd Dockerfile/
vim Dockerfile
FROM nginx
RUN echo ‘本地构建docker测试’ > /usr/share/nginx/html/index.html \
&& echo ‘使用&&在同一层镜像中添加内容’ >> /usr/share/nginx/html/index.html
```

3. 开始构建镜像

``` shell
docker build -t nginx:test .
# . 是上下文路径，指docker在构建进行，有时会想使用到本机的文件，docker build命令得知这个路径后，会将路径下的所有内容打包
```

4. 指令详解

 

 

### Docker Compose

1. 什么是Docker Compose

Docker Compose是一个用来定义和运行复杂应用的Docker工具。一个使用Docker容器的应用，通常由多个容器组成。使用Docker Compose不再需要使用Shell脚本来启动容器，而使用服务编排的方式来管理容器。  
Docker Compose通过一个配置文件来管理多个Docker容器，在配置文件中，所有的容器通过services来定义，然后使用docker-compose脚本来启动、停止和重启应用，和应用中的服务以及所有依赖服务的容器，非常适合组合使用多个容器进行开发的场景。  

2. 安装docker compose

``` shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

3. 创建软链

``` shell
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

4. 查看版本

``` shell
docker-compose --version
```

5. 启动应用程序

``` shell
docker compose up
```

6. 后台启动应用程序 

``` shell
docker compose up -d
```

7. 配置文件 

``` shell
docker-compose.yml
```



### Docker Machine

1. 什么是Docker Machine

Docker Machine是一种可以在虚拟主机上安装Docker的工具，并可以使用docker-machine命令来管理主机。Docker Machine也可以集中管理所有的docker主机，比如快速的给多台服务器安装上docker。Docker Machine管理的虚拟机可以是机上的，也可以是云供应商，OpenStack等，使用docker-machine命令，可以直接启动，检查，停止和重启托管主机，也可以升级Docker客户端和守护程序，以及配置Docker客户端与所在主机通信等。  

2. 安装Docker Machine

``` shell
base=https://github.com/docker/machine/releases/download/v0.16.0 &&
 curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
 sudo mv /tmp/docker-machine /usr/local/bin/docker-machine &&
 chmod +x /usr/local/bin/docker-machine
```

3. 检查是否安装成功

``` shell
docker-machine version
```

4. 编辑辅助脚本

``` shell
vim /etc/bash_completion.d/docker-machine-down.bash

base=https://raw.githubusercontent.com/docker/machine/v0.16.0
for i in docker-machine-prompt.bash docker-machine-wrapper.bash docker-machine.bash
do
 	sudo wget "$base/contrib/completion/bash/${i}" -P /etc/bash_completion.d
done

:wq!
```

5. 安装辅助脚本

``` shell
source /etc/bash_completion.d/docker-machine-down.bash			
```

6. 开启root账户登入

``` shell
vim /etc/ssh/sshd_config（PermitRootLogin YES）
```

7. 开启免密登入

``` shell
ssh-keygen ；ssh-copy-id [root@192.168.1.11](mailto:root@192.168.1.11)
```

8. 提高用户权限

``` shell
vim /etc/sudoers （visiblepw取消前面的“!”，运行所有tty登入）
```

9. 列出可用机器

``` shell
docker-machine ls
```

10. 创建机器

``` shell
docker-machine create --driver generic --generic-ip-address=192.168.1.11 host1

#参数说明：
--driver：创建机器的驱动类型
vitualbox：Windows平台虚拟化
generic：Linux平台
--generic-ip-address：指定需要安装docker的机器
host1：主机名
```

11. 使用变量进入host1主机bash

``` shell
docker-machine env host1
eval $(docker-machine env host1)
bash				#进入bash
exit				#退出host1
```

12. 更新

``` shell
docker-machine upgrade host1 host2
```

13. 查看配置

``` shell
docker-machine config host1  
```

14. 拷贝文件

``` shell
docker-machine scp host1:/tmp/a host2:/tmp/b
```




### Docker Swarm

1. 什么是Docker Swarm

Swarm是Docker的集群管理工具。他将Docker主机池转变为单个虚拟Docker主机。Docker Swarm提供了标准的Docker API，所有任何已经与Docker守护进程通信的工具都可以使用Swarm轻松地扩展到多个主机。  

2. 构成

管理节点（swarm manager）、工作节点（work node）  

3. 使用
- 保证各台机器能够免密登入，可以将ssh密钥发送到其他机器上

``` shell
ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.1.11
```

- 确定时间（设置相同）

``` shell
date
```
- 初始化集群节点，此节点为管理节点

``` shell
docker swarm init --advertise-addr 192.168.1.10
```
- 获取以manager加入集群的命令，在机器3中输入获得的token命令，可将其作为manager加入集群

``` shell
docker swarm join-token manager/worker
```
- 复制获得的token命令，在机器2中输入，可将机器2作为manager/worker加入集群

``` shell
docker swarm join --token ******
```
- 检测进程（结果docker 都以独立的进程运行）

``` shell
netstat -anput | grep docker
```
- 查看docker信息

``` shell
docker info
Is Manager：true/false
```
- 查看现有节点（只能在manager节点上查看）

``` shell
docker node ls
```
- Manager与worker节点转化

``` shell
docker node promote node2				#提升为manager
docker node demote node3				#降级为worker
```

- 开启路由转发

``` shell
vim /etc/sysctl.conf

net.ipv4.ip_forward = 1				

:wq!
```

- 发送到其他主机

``` shell
scp /etc/sysctl.conf root@192.168.1.11:/etc
```

- 搭建本地私有仓库

``` shell
docker pull registry:2
```

- 运行私有仓库

``` shell
mkdir -p /opt/data/registry
docker run -itd -p 5000:5000 --restart always -v /opt/data/registry/:/var/lib/registry --name registry registry:2
```

- 修改服务项使用私有仓库

``` shell
vim /usr/lib/systemd/system/docker.service

ExecStart ****** --insecure-registry 192.168.1.10:5000

:wq!

systemctl daemon-reload
systemctl restart docker.service
```

- 打包现有镜像并上传到私有仓库

``` shell
docker tag openwrt:latest 192.168.1.10:5000/opewrt
docekr push 192.168.1.10:5000/openwrt
```

- 使用本地其他机器测试私有仓库

``` shell
docker pull 192.168.1.10:5000/openwrt
docker images
```

- 准备overlay网络

``` shell
docker network create --driver overlay docker
docker network ls
```

- 安装swarm管理面板并上传供其他机器使用

``` shell
docker search visualizer
docker pull dockersamples/visualizer

docker tag visualizer:latest 192.168.1.10:5000/visualizer
docekr push 192.168.1.10:5000/visualizer

docker pull 192.168.1.10:5000/visualizer			#其他机器也进行安装，方便操作
```

- 运行管理界面

``` shell
docker run -itd -p 8888:8080 -e HOST=192.168.1.10 -e PORT=8080 -v /var/run/docker.sock:/var/run/docker.sock --name visualizer 192.168.1.10:5000 visualizer
```

- 浏览器打开管理界面：`192.168.1.10:8888`

 

 