---
title: "Hello Github&Hexo"
subtitle: "利用github+Hexo搭建的静态博客"
date: 2020-02-29T03:39:22+08:00
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
- Github
- Hexo
- Blog
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

> 展示Demo：[愛吃柚子的熊](https://usee-net.github.io)
  ![gitpage with hexo.png](https://uss.useenet.cn/2020/03/22/a035c3aab91ab.png)
  ## 创建专用仓库  
新建git代码库命名为`ID.github.io`  
成功后可得域名`https://ID.github.in`  
使用私有域名进行解析  
>`ping id.github.io`     解析出该域名的ip地址
>> 购买域名后使用免费域名（通过域名提供商或CF）解析到该ip即可

## 准备本地Git环境
### SSH配置
1、首先查看设备是否已经有ssh密钥对  
- Windows
``` shell
C:\用户\Username\ .ssh  
```
- WSL & Linux
``` shell
cd C:\Users\USee\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\home\usee\.ssh  
cd ~/.ssh
```
2、若没有ssh密钥对，则手动生成  
``` shell
ssh-keygen -t rsa -C "admin@123.com"    #回车默认即可
```
>进入.ssh文件夹中，使用notepad++或者`cat`等命令获取公钥**id_rsa.pub**  
>复制到github公钥栏中

### 下载Git
- Windows  
  推荐使用[Cmder终端](https://github.com/cmderdev/cmder/releases)，集成了Git并可以在win环境中使用常用的shell命令

- WSL & Linux
``` shell
# 一般默认自带

# 安装
yum install git -y  
sudo apt-get install git  
```
- 查看git版本
``` shell
git --version     
```

### 配置基本git信息
- 配置git
``` shell
git config --global user.name "USee"
git config --global user.email "邮箱"
```

## 开始建站
### 克隆仓库到本地

``` shell
git clone git@github.com:XXX:XXX.github.io.git
```
### 安装Nodejs
- Windows  
[**下载**](https://nodejs.org/en)安装即可

- WSL & Linux
``` shell
wget https://nodejs.org/dist/v13.9.0/node-v13.9.0-linux-x64.tar.xz       #自行选择对应版本  
tar xf node....tar.xz -C /usr/local/
cd /usr/local/  
mv node....  nodejs  
ln -s /usr/local/nodejs/bin/node /usr/local/bin  
ln -s /usr/local/nodejs/bin/npm /usr/local/bin  
    
# 查看版本
node -v        
npm -v

# 更换npm淘宝源  
npm config set registry https://registry.npm.taobao.org  
# 检测是否更换
npm config get registry
```

### 安装Hexo  
``` shell
# 下载并安装
npm install -g hexo-cli
hexo init 
npm install
hexo -v         //查看版本

hexo new XX     //新建XX
hexo generate   //生成静态网站
hexo server     //开启服务    
hexo clean      //清理缓存
hexo deploy     //更新上传，首次使用时安装以下插件
npm install hexo-deployer-git --save

# 修改配置文件
vim _config.yml 
```
### NEXT主题
``` shell
# 下载next主题
git clone git@github.com:theme-next/hexo-theme-next.git themes/next  

# 修改配置文件
vim themes/next/_config.yml
```

## 编辑内容
### 新建侧栏菜单
``` shell
# 添加菜单主页项,查找`menu`选项按格式添加即可
vim theme/next/_config.yml   

hexo new page about  	//tags、categroies 类似
vim source/about/index.md	//修改主页

hexo new page about  --path about/me "自述"      #可直接生成 /shouce/about/me.md 文件，内容标题为 自述 
```

### 新建文章
``` shell
hexo new test
vim source/_posts/test.md

显示部分
<!--more-->
隐藏部分
```

### 添加标签
``` shell
vim source/_posts/test.md
tags: 标签                #单个标签
tags: ["Hexo","Github","Nodejs"]        #多标签
```

### 添加分类
``` shell
vim source/_posts/test.md
categroies: 前端
```
---
## 更新博客
``` shell
hexo clean	    #清除  
hexo n XX       #新建XX
hexo g		      #生成  
hexo s		      #本地测试  

# 更新上传
hexo d  

# 生成并更新
hexo g -d  
hexo d -g  
```

## 日后更新

***3月2日更新***

1、如何在Github&Hexo网页中插入图片

- 新建文件夹
``` shell
mkdir /source/images
```  
- 插入方式
``` markdown
![内容说明](/images/XXX.png)

或 ||

<img src="/images/XXX.png">
```
