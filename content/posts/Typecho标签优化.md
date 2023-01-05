---
title: "Typecho标签优化"
subtitle: ""
date: 2020-03-28T14:56:55+08:00
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
- Typecho
- 标签
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

## 原效果
<!-- ![Tags-old.png](https://uss.useenet.cn/2020/03/28/792d1a8730254.png) -->
在编辑时需要手动输入标签名，如遇原标签名不一致，则会新建一个
{{< image src="https://uss.useenet.cn/2020/03/28/792d1a8730254.png" caption="Tags-old">}}

## 优化后效果展示
在编辑文章时如上可以直接选择已有标签，便于操作
<!-- ![Tags-new](https://uss.useenet.cn/2020/03/28/582374d6d186f.png) -->
{{< image src="https://uss.useenet.cn/2020/03/28/582374d6d186f.png" caption="Tags-new">}}

<!--more-->

## 优化步骤
编辑`Typecho`中的撰写页面文件，路径`站点根目录/admin/write-post.php`
找到标签栏的代码，在合适位置插入以下代码即可
``` php
< div id = "exist-tags" >
    < p style = "background: #fff;border: 1px solid #D9D9D6;display: block;padding: 2px 4px;" >
    <? php
      $stack = Typecho_Widget::widget('Widget_Metas_Tag_Cloud') - > stack;
      $i = 0;
      while (isset($stack[$i])) {
          echo "<a id=\"mydiv$i\" style=\"cursor:pointer;padding: 0px 6px;margin: 2px 0;display: inline-block;\" onclick=\"mytag=document.getElementById('mydiv$i');mytag.style.backgroundColor='#E9E9E6';t=document.getElementById('tags').value;c=t?',':'';document.getElementById('tags').value=t+c+'", $stack[$i]['name'], "'\">", $stack[$i]['name'], "</a>";
          $i++;
          if (isset($stack[$i])) echo "  ";
    } ?>
    < /p> 
< /div>
```
