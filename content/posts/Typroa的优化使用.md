---
title: "Typroa的优化使用"
subtitle: ""
date: 2020-04-14T12:05:48+08:00
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
- 图床
- Picgo
- Typroa
- Markdown
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
<!-- ![Typroa](https://uss.useenet.cn/picgo/20200414123428.png) -->
{{< image src="https://uss.useenet.cn/picgo/20200414123428.png" caption="Typroa">}}

## 什么是Typroa
Typora 是一款支持实时预览的 Markdown 文本编辑器，它有 OS X、Windows、Linux 三个平台的版本且完全免费，使用起来十分简洁舒适，同时它的自定义化也非常强大，是个不可多得的 Markdown 编辑器，以下进行简单的优化设置，佛系更新。
<!--more-->
<!-- > Typroa官网    [飞机直达](https://www.typora.io/) -->
{{< link href="https://www.typora.io/" content="Typroa官网" card=true >}}

## 图片插入
- 默认：使用本地图片进行插入，使文档不便于多设备浏览，需要同时拷贝目录中的图片文件
- 优化：使用网络图床，图片直接通过云端加载，便于文档跨设备访问而不影响图片显示

1. 下载Picgo  
> [Picgo](https://github.com/Molunerfinn/PicGo/releases)  
> [Picgo-core](https://github.com/PicGo/PicGo-Core)

2. 准备图床
<!-- ![](https://uss.useenet.cn/picgo/20200414130706.png) -->
{{< image src="https://uss.useenet.cn/picgo/20200414130706.png" caption="准备图床">}}
> PS：注意加速域名需要添加协议前缀（https、http、ftp等）

3. 设置`Typroa`图像
<!-- ![Picgo](https://uss.useenet.cn/picgo/20200414130229.png) -->
{{< image src="https://uss.useenet.cn/picgo/20200414130229.png" caption="Picgo">}}

> picgo和picgo-core可自行选择，picgo安装即可使用
<!-- ![picgo-core](https://uss.useenet.cn/picgo/20200414130330.png) -->
{{< image src="https://uss.useenet.cn/picgo/20200414130330.png" caption="picgo-core">}}

4. 食用方式
<!-- ![Typroa-unuplaod](https://uss.useenet.cn/picgo/20200414131629.png) -->
{{< image src="https://uss.useenet.cn/picgo/20200414131629.png" caption="Typroa-unuplaod">}}

<!-- ![Typroa-uploaded](https://uss.useenet.cn/picgo/20200414131844.png) -->
{{< image src="https://uss.useenet.cn/picgo/20200414131844.png" caption="Typroa-uploaded">}}

5. 指定Typroa文档目录为有道云等云端自动备份目录即可在其他设备访问时正常显示图片