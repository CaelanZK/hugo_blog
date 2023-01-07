---
title: "Python常见异常"
subtitle: ""
date: 2020-05-28T00:30:30+08:00
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
![Python](https://uss.useenet.cn/2020/05/28/320c18e890a17.jpg)
## 常见异常详情

1. SyntaxError：语法错误

   ``` python
   int a = 3
   
   #报错
   	int a = 3
   	  	  ^
   SyntaxError: invalid syntax
   ```

   

2. NameError：尝试访问一个没有申明的变量

   ``` py
   print(a)
   
   #报错
   	print(a)
   NameError: name 'a' is not defined
   ```

   

3. ZeroDivisionError：除数为0错误（零除错误）

   ``` py
   a = 3/0
   
   #报错
   	a = 3/0
   ZeroDivisionError: division by zero
   ```

   

4. ValueError：数值错误

   ``` py
   float('usee')
   
   #报错
   	float('usee')
   ValueError: could not convert string to float: 'usee'
   ```

   

5. TypeError：类型错误

   ``` py
   123 + 'abc'
   
   #报错
   	123 + 'abc'
   TypeError: unsupported operand type(s) for +: 'int' and 'str'
   ```

   

6. AttributeError：访问对象的不存在的属性

   ``` py
   a=100
   a.sayhi()
   
   #报错
   	a.sayhi()
   AttributeError: 'int' object has no attribute 'sayhi'
   ```

   

7. IndexError：索引越界异常

   ``` py
   a = [4,5,6]
   a[10]
   
   #报错
   	a[10]
   IndexError: list index out of range
   ```

   

8. KeyError：字典的关键字不存在

   ``` py
   a = {'name':"usee",'age':18}
   a['salary']
   
   #报错
   	a['salary']
   KeyError: 'salary'
   ```



## 常见异常汇总

|         异常名称          |                        说明                        |
| :-----------------------: | :------------------------------------------------: |
|      ArithmeticError      |               所有数值计算错误的基类               |
|      AssertionError       |                    断言语句失败                    |
|      AttributeError       |                  对象没有这个属性                  |
|       BaseException       |                   所有异常的基类                   |
|    DeprecationWarning     |               关于被弃用的特征的警告               |
|     EnvironmentError      |                 操作系统错误的基类                 |
|         EOFError          |             没有内建输入,到达 EOF 标记             |
|         Exception         |                   常规错误的基类                   |
|    FloatingPointError     |                    浮点计算错误                    |
|       FutureWarning       |           关于构造将来语义会有改变的警告           |
|       GeneratorExit       |        生成器(generator)发生异常来通知退出         |
|        ImportError        |                 导入模块/对象失败                  |
|     IndentationError      |                      缩进错误                      |
|        IndexError         |             序列中没有此索引（index）              |
|          IOError          |                 输入/输出操作失败                  |
|     KeyboardInterrupt     |             用户中断执行(通常是输入^C)             |
|         KeyError          |                  映射中没有这个键                  |
|        LookupError        |                 无效数据查询的基类                 |
|        MemoryError        |     内存溢出错误(对于 Python 解释器不是致命的)     |
|         NameError         |            未声明/初始化对象 (没有属性)            |
|    NotImplementedError    |                   尚未实现的方法                   |
|          OSError          |                    操作系统错误                    |
|       OverflowError       |                数值运算超出最大限制                |
|      OverflowWarning      |        旧的关于自动提升为长整型(long)的警告        |
| PendingDeprecationWarning |              关于特性将会被废弃的警告              |
|      ReferenceError       | 弱引用(Weak reference)试图访问已经垃圾回收了的对象 |
|       RuntimeError        |                  一般的运行时错误                  |
|      RuntimeWarning       |      可疑的运行时行为(runtime behavior)的警告      |
|       StandardError       |              所有的内建标准异常的基类              |
|       StopIteration       |                 迭代器没有更多的值                 |
|        SyntaxError        |                  Python 语法错误                   |
|       SyntaxWarning       |                  可疑的语法的警告                  |
|        SystemError        |                一般的解释器系统错误                |
|        SystemExit         |                   解释器请求退出                   |
|         TabError          |                   Tab 和空格混用                   |
|         TypeError         |                  对类型无效的操作                  |
|     UnboundLocalError     |               访问未初始化的本地变量               |
|    UnicodeDecodeError     |                Unicode 解码时的错误                |
|    UnicodeEncodeError     |                 Unicode 编码时错误                 |
|       UnicodeError        |                 Unicode 相关的错误                 |
|   UnicodeTranslateError   |                 Unicode 转换时错误                 |
|        UserWarning        |                 用户代码生成的警告                 |
|        ValueError         |                   传入无效的参数                   |
|          Warning          |                     警告的基类                     |
|       WindowsError        |                    系统调用失败                    |
|     ZeroDivisionError     |            除(或取模)零 (所有数据类型)             |