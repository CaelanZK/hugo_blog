---
title: "国内VPS安装ServerStatus探针"
subtitle: ""
date: 2020-03-05T19:36:52+08:00
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
- vps
- 探针
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

<!--more-->
## 概述
一直想为自己的vps安装状态监控，方便随时进行查看状态；经过一番查找，有以下几款比较优秀：
<!-- - [**NetDate**](https://github.com/netdata/netdata)   -->

- **NetDate**:一款特别炫酷的开源探针，经了解发现，占用资源比较高；能十分详细的了解到自己主机的各方面状态，但是不能为监控面板提供加密，导致任何人都能够进入查看，所以个人不推荐使用。 [Demo](https://singapore.my-netdata.io/default.html) 
{{< link href="https://github.com/netdata/netdata" content="NetData Github" card=true >}}
<!-- - [**SeverStatus**](https://github.com/BotoX/ServerStatus)、-->
- **SeverStatus**:非常轻便的一款探针，能够显示最基本的状态信息，我本人使用的是基于这个的多次改版的[Hotaru](https://github.com/CokeMine/ServerStatus-Hotaru),修改的更为美观。  [Demo](http://tz.useenet.cn/) 
{{< link href="https://github.com/BotoX/ServerStatus" content="SeverStatus Github" card=true >}}

<!-- - [**Linux Dash**](https://github.com/afaqurk/linux-dash)、 -->
- **Linux Dash**:功能齐全，面板直观，单VPS使用极佳。  [Demo](https://afaqurk.github.io/linux-dash/)  
{{< link href="https://github.com/afaqurk/linux-dash" content="Linux Dash Github" card=true >}}
<!-- - [**Vmstat**](https://github.com/walkor/workerman-vmstat)、 -->
- **Vmstat**:功能简洁直观，不过也是单VPS使用。  [Demo](http://www.workerman.net/demos/vmstat/)
{{< link href="https://github.com/walkor/workerman-vmstat" content="Vmstat" card=true >}}

<!--more-->

## 演示效果
<!-- ![tz-show.png](https://uss.useenet.cn/2020/03/22/8167ebeadd1b2.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/8167ebeadd1b2.png" caption="tz-show">}}

## 食用方式
- 有科学上网条件的可以直接使用以下脚本进行安装（会要求安装Caddy，与Nginx不能同时安装，有能力的自行DIY）
``` shell
wget https://raw.githubusercontent.com/CokeMine/ServerStatus-Hotaru/master/status.sh
bash status.sh 
```
- 国内VPS可以手动编译安装，可搭配宝塔使用Nginx提供服务
> PS：（以下使用方式二，方式一直接运行傻瓜安装即可）
## 开始安装
- 下载ServerStatus-USee
``` shell
git clone https://gitee.com/useenet/serverTZ.git
mv serverTZ /usr/serverTZ
```
## 安装服务端
- 使用宝塔创建一个空网页（PS：域名框使用域名或IP均可）  
<!-- ![tz-creatsite.png](https://uss.useenet.cn/2020/03/22/7fe3a0a4b3f9c.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/7fe3a0a4b3f9c.png" caption="tz-creatsite">}}
- 复制监控展示页到宝塔新建的网站目录中
``` shell
cp -r /usr/serverTZ/web/* /www/wwwroot/tz       #设置自己新建的web路径
```
- 进入服务端配置目录
``` shell
cd /usr/serverTZ/server
```
- 安装环境并进行编译
``` shell
apt-get install gcc gcc-c++ kernel-devel 
make
```
- 配置服务端信息
``` json
// vim config.json
{
	"servers": [
    {
			"username": "username",
			"password": "password",
			"name": "vpsname",
			"type": "type",
			"host": "No",
			"location": "China",
			"disabled": false,
			"region": "CN"
		},
		{
			//此模板可以添加多个VPS,自行添加即可
			"username": "连接用户名",
			"password": "连接密码",
			"name": "监控显示名称",
			"type": "监控显示类型",
			"host": "No",
			"location": "国家",
			"disabled": false,
			"region": "国旗"
		},  //注意此处的逗号（国旗后无需添加，在新增的括号后加即可）
	]
}
```
- 在宝塔中打开serverTZ默认端口：`35601`
- 编辑完成后，在`server`目下进行测试,webdir为web站点路径
``` shell
./sergate --config=config.json --web-dir=/www/wwwroot/tz        #设置自己新建的web路径
```
- 进入对应的监控站点查看是否有监控网页模板
### 将此进程注册为系统服务
> 关闭之前进程,进入`/usr/serverTZ/systemd/`
``` shell
ctrl + c
cd ../systemd
```
> 注册过程，系统服务文件我已经编辑好，直接使用即可
``` shell
chmod +x serverTZs.service                #赋权 
cp serverTZs.service /lib/systemd/system  #拷贝进系统服务目录 
systemctl daemon-reload                   #重新加载系统服务 
systemctl start serverTZs.service         #启动服务端并设置开机自启
systemctl enable serverTZs.service          

systemctl restart serverTZs.service       #在配置文件中增加vps后重启
```
## 安装客户端
**1）此处在服务端中部署客户端监控本机为例**
- 下载、更名、移动目录到指定文件夹
``` shell
git clone https://gitee.com/useenet/serverTZ.git
mv serverTZ /usr/serverTZ
```
- 进入客户端配置目录
``` shell
cd /usr/serverTZ/clients
```
- 检查已安装的python版本
``` shell
python -V                                 #版本需要2.7及以上
```
> 若无执行客户端运行环境
``` shell
apt-get install epel-release python-pip
apt-get update
apt-get install gcc python-devel
pip install psutil
```
- 修改客户端配置文件
``` shell
vim status-client.py

SERVER = "127.0.0.1"                      #修改为服务端地址
PORT = 35601      
USER = "USER"                             #客户端用户名
PASSWORD = "USER_PASSWORD"                #客户端密码
INTERVAL = 1                              #更新间隔
```
- 运行测试
``` shell
python status-client.py
```
**2）将此进程注册为系统服务**
- 关闭之前进程,进入`/usr/serverTZ/systemd/`
``` shell
ctrl + c
cd ../systemd
```
- 注册过程，系统服务文件我已经编辑好，直接使用即可
``` shell
chmod +x serverTZc.service                #赋权 
cp serverTZc.service /lib/systemd/system  #拷贝进系统服务目录 
systemctl daemon-reload                   #重新加载系统服务  
systemctl start serverTZc.service         #启动服务端并设置开机自启 
systemctl enable serverTZc.service 
 
systemctl restart serverTZc.service       #在配置文件中增加vps后重启
```
## 关于修改解压后的目录
> 可以自定义任何位置，记得修改`systemd/`中的注册系统服务文件即可