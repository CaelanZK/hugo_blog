---
title: "Python数据分析 Day01"
subtitle: ""
date: 2020-12-23T01:05:09+08:00
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
- Python
- 数据分析
categories:
- 编程

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
## 前言

>话不多说先上题
<!-- ![image-20201223000000024](https://uss.useenet.cn/picgo_core/image-20201223000000024.png!) -->
{{< image src="https://uss.useenet.cn/picgo_core/image-20201223000000024.png!" caption="数据分析题1">}}

## 项目需求
1. 显示数据相关性
2. 猜测符合那种分布并给出可信度
3. 该分布在逻辑意义上对数据相关的指导意义（哪些数据有可能对哪些结果有直接因果关系，并且给出因果关系的概率）


## 前期准备

1. 统计学数据相关性：一是相关分析，即通过引入一定的统计指标量化变量之间的相关程度；另一个是回归分析，由于回归分析不仅仅刻画相关关系，更重要的是刻画因果关系
2. 统计学分布：离散型随机变量分布（两点分布/伯努利分布、二项分布、超几何分布、几何分布、负二项分布、泊松分布）、连续型随机变量分布（均匀分布、指数分布、正态分布）

3. python所使用的工具包（numpy、scipy、matplotlib）Anaconda
4. python所使用的辅助包（Pandas、Statsmodels、Seaborn）

## 工具包介绍

1. **numpy**，**scipy**，**matplotlib**

`NumPy`通常与`SciPy`（Scientific Python）和`Matplotlib`（绘图库）一起使用， 这种组合广泛用于替代`MatLab`，是一个强大的科学计算环境，有助于我们通过 Python 学习数据科学或者机器学习


  

2. **pandas**

Pandas 是基于 NumPy 的一个开源 Python 库，它被广泛用于快速分析数据，以及数据清洗和准备等工作。它的名字来源是由“ Panel data”（面板数据，一个计量经济学名词）两个单词拼成的。简单地说，你可以把 Pandas 看作是 Python 版的 Excel


  

3. **statsmodels**


Python StatsModels允许用户浏览数据，执行统计测试和估计统计模型。它应该补充SciPy的统计模块。它是Python科学堆栈的一部分，用于处理数据科学，统计数据和数据分析

  

4. **seaborn**

seaborn同matplotlib一样，也是Python进行数据可视化分析的重要第三方包。但seaborn是在matplotlib的基础上进行了更高级的API封装，使得作图更加容易，图形更加漂亮

  

