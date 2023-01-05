---
title: "Typecho博客添加运行时间"
subtitle: ""
date: 2020-03-07T23:20:15+08:00
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
- blog
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
## 将以下代码加入functions.php

> 一般在主题根目录：`网站/usr/themes/主题` 修改一下你自己的网站时间

``` php
// 设置时区
date_default_timezone_set('Asia/Shanghai');
/**
 * 秒转时间，格式 年 月 日 时 分 秒
 *
 */
function getBuildTime() {
    // 在下面按格式输入本站创建的时间
    $site_create_time = strtotime('2019-12-13 12:08:00');
    $time = time() - $site_create_time;
    if (is_numeric($time)) {
        $value = array(
            "years" => 0, "days" => 0, "hours" => 0,
            "minutes" => 0, "seconds" => 0,
        );
        if ($time >= 31556926) {
            $value["years"] = floor($time / 31556926);
            $time = ($time % 31556926);
        }
        if ($time >= 86400) {
            $value["days"] = floor($time / 86400);
            $time = ($time % 86400);
        }
        if ($time >= 3600) {
            $value["hours"] = floor($time / 3600);
            $time = ($time % 3600);
        }
        if ($time >= 60) {
            $value["minutes"] = floor($time / 60);
            $time = ($time % 60);
        }
        $value["seconds"] = floor($time);

        echo '<span class="btime">'.$value['years'].
        '年'.$value['days'].
        '天'.$value['hours'].
        '小时'.$value['minutes'].
        '分</span>';
    } else {
        echo '';
    }
}
```

## 修改footer.php
> 在页脚选择合适的位置加入：

``` php
<?php getBuildTime(); ?>
```