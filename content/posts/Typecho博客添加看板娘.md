---
title: "Typecho博客添加看板娘"
subtitle: ""
date: 2020-03-21T02:45:13+08:00
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
- 看板娘
- Live2d
- Typecho
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

## 起因
> 最近把博客从腾讯云迁移到了阿里云，随便也把Z-Blog换成了Typecho；相比于Z-blog，Typecho比较轻量级，便于上手，重要的是它完美支持`Markdown`文章，手动滑稽 ≧◇≦
> 以下为柚見小站加上可爱的看板娘咯

## 准备工作

1. 为了便于操作，首先下载好所需要的文件，这里使用的是`fghrsh`、`stevenjoezhang`两位大大的源码

<!-- - [fghrsh](https://github.com/fghrsh)/ -->
- **fghrsh**：[live2d_api](https://github.com/fghrsh/live2d_api)、[live2d_demo](https://github.com/fghrsh/live2d_demo)
  
{{< link href="https://github.com/fghrsh" content="fghrsh github page" card=true >}}

<!-- - [stevenjoezhang](https://github.com/stevenjoezhang)/ -->
- **stevenjoezhang**：[live2d-widget](https://github.com/stevenjoezhang/live2d-widget)

{{< link href="https://github.com/stevenjoezhang" content="stevenjoezhang" card=true >}}

2. 所需工具，使用`XShell&XFtp`、`MobaXterm`上传文件或者使用宝塔面板；为方便操作，下文以宝塔为例

## 前端部署

1. 修改文件夹名称为`live2d`（上文中两大大任选一个即可，下文以`live2d-widget`为例）

2. 编辑配置文件中的`autoload.js`

<!-- ![live2d-change1.png](https://uss.useenet.cn/2020/03/22/2ccbb58f8f915.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/2ccbb58f8f915.png" caption="live2d-change-1" >}}
> PS：注释掉第二行，将第三行修改为上图所示（后面的`/`不能少）

3. 进入博客主目录  

<!--  ![live2d-cdmenu.png](https://uss.useenet.cn/2020/03/22/2bfe2fd439319.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/2bfe2fd439319.png" caption="live2d-cdmenu">}}

4. 上传前端文件至站点根目录

<!-- ![live2d-upload1.png](https://uss.useenet.cn/2020/03/22/82840d75add1e.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/82840d75add1e.png" caption="live2d-upload1">}}

5. 前往博客后台编辑`index.php`或者`footer.php`，在`header`标签中加入以下代码

``` javascript
<script src="/live2d/autoload.js"></script>
```

> PS：若使用的主题有便捷插入框也可直接引用
>
> {{< image src="https://uss.useenet.cn/2020/03/22/e7a663c4140fb.png" caption="live2d-link">}}
<!-- >![live2d-linkjs.png](https://uss.useenet.cn/2020/03/22/e7a663c4140fb.png) -->

6. 回到主页按`Ctrl+F5`强制刷新即可出现

<!-- ![live2d-slience.png](https://uss.useenet.cn/2020/03/22/967a32a57e640.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/967a32a57e640.png" caption="live2d-slience">}}

## 后端部署

1. 修改文件名为`api`（下文以`live2d_api`为例）

2. 将`api`文件夹上传到`live2d`目录下

<!-- ![live2d-upload2.png](https://uss.useenet.cn/2020/03/22/5454fa72cabec.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/5454fa72cabec.png" caption="live2d-upload2">}}

3. 编辑配置文件`authload.js`

<!-- ![live2d-change2.png](https://uss.useenet.cn/2020/03/22/69be16eb50acd.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/69be16eb50acd.png" caption="live2d-change2">}}

> PS：在上文长传的目录`live2d`下使用宝塔在线编辑；
>> 修改第36行`apiPath`为` "/live2d/api/"`如上图所示

4. 回到主页按`Ctrl+F5`强制刷新并`F12`打开控制台查看是否引用本地`api`

<!-- ![live2d-localapi.png](https://uss.useenet.cn/2020/03/22/ddba02018b087.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/ddba02018b087.png" caption="live2d-localapi">}}

5. 完成本地前后端部署

## 功能介绍

<!-- ![live2d-options.png](https://uss.useenet.cn/2020/03/22/5e94048be3b37.png) -->
{{< image src="https://uss.useenet.cn/2020/03/22/5e94048be3b37.png" caption="live2d-options">}}

1. 刷新`一言`文本框
2. 锁定界面
3. 更换看板娘
4. 看板娘换装
5. 当前状态截图
6. 关于看板娘
7. 关闭看板娘

## 详细配置

> 后续更新