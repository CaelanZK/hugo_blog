---
title: "第三届“全国大学生大数据技能竞赛”Updating"
subtitle: ""
date: 2020-06-07T20:19:06+08:00
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
- 大数据
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
## 比赛介绍
中国大数据技术与应用联盟此次举办的2020年第三届“全国大学生大数据技能竞赛”目的在于在提升高校大数据人才技能水平，增强领域知识覆盖范围，完善大数据人才培养机制，为我国大数据战略发展的稳步实施提供坚实可靠的人才基础。   
并充分调研企业中大数据岗位的用人要求，分析人才所需知识技能，并据此设计出贴近真实工作环境的赛项内容。此外，赛项设置了大数据环境搭建、数据预处理、数据初步分析、数据分析展示等环节。通过赛项的设置，考核锻炼选手如下能力：
1. 大数据环境搭建能力；
2. 大数据平台调优与运维能力；
3. 数据采集与预处理能力；
4. 数据采集与存储能力；
5. 数据关联分析、数据挖掘能力；
6. 数据可视化能力。

## 参赛初衷
> 学校刚出来实习，面对社会上很多知识都不了解，想多了解扩充自己的知识面，刚好借由此次竞赛的三次培训机会粗略了解认识大数据。

## Day One

### Linux系统环境准备

1. 安装好CentOS7系统

2. 配置网络

``` shell
# 修改网络配置
vim /etc/sysconfig/network-scripts/ifcfg-ens33

PROTOCOL=static			#修改为静态
IPADDR = 10.0.0.137
NETWORK = 255.255.255.0
GATEWAY = 10.0.0.2
ONBOOT=yes              # 开机启动
```

3. 设置主机名

``` shell
hostname									#查看主机名
hostnamectl set-hostname master				#永久更改主机名为：master
```

4. 关闭防火墙

``` shell
systemctl status firewalld				
systemctl stop firewalld
systemctl disable firewalld				#关闭自启
```

5. 修改映射文件

``` shell
# 修改映射文件hosts
vim /etc/hosts

# 添加映射列表
10.0.0.137 master
10.0.0.138 slave1
10.0.0.139 slave2
```

6. SSH免密登入

- 检查服务

``` shell
ssh -V				#查看版本
netstat -lnutp		#查看22端口是否开启
```

- 生成密钥对

``` shell
ssh-keygen -t rsa
#默认直接回车三次即可
```

- 将公钥放置授权列表并赋权

``` shell
cp .ssh/id_rsa.pub .ssh/authorized_key
chmod 600 authorized_key
```

>PS：可将其他节点生成的公钥拷贝至`./ssh`文件夹并命名为`authorized_key1`,在末尾添加序号加以区别并赋权

``` shell
scp .ssh/authorized_key0 root@10.0.0.138:.ssh/			#注意authorized_key序号
```

- 检验免密登入

``` shell
ssh slave1
#或者
ssh 10.0.0.138
```

>PS：`ssh`后面直接使用主机名需要修改好`hosts`映射文件

7. JDK安装

- 准备软件
<!-- 下载链接：[飞机直达](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html) -->
{{< link href="https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html" content="JDK下载页"  card=true >}}

- 解压软件包

``` shell
mkdir /root/software								#创建路径
tar -zxvf jdk-xxx-x64.tar.gz -C /root/software		#解压到指定路径
```

- 配置系统环境变量

``` shell 
vim /etc/profile

# 文件末尾添加如下
export JAVA_HOME=/root/software/jdk1.8.0_171		#配置JAVA安装路径
export PATH=$PATH:$JAVA_HOME/bin
```

- 重载更新配置文件

``` shell
source /etc/profile
```

- 检测JDK是否安装成功并查看版本

``` shell
java -version
cat $JAVA_HOEM			#查看路径
```

### 搭建HDFS伪分布式集群

1. 解压`hadoop2.7.7`安装包

``` shell
tar -zxvf hadoop-xxx.tar.gz -C /root/software
```

2. 配置环境变量`hadoop-env.sh`

``` shell
vim /root/software/hadoop-2.7.7/etc/hadoop/hadoop-env.sh
```

- 修改JAVA_HOME参数为JDK实际位置

<!-- ![修改JAVA_HOME参数为JDK实际位置](https://uss.useenet.cn/picgo/20200621135654.png) -->
{{< image src="https://uss.useenet.cn/picgo/20200621135654.png" caption="修改JAVA_HOME参数为JDK实际位置">}}  

3. 配置核心组件`core-site.xml`

``` shell
vim /root/software/hadoop-2.7.7/etc/hadoop/core-site.xml
```

- 将下面的配置内容添加到 `<configuration></configuration>` 中间：

``` xml
<!-- HDFS集群中NameNode的URI（包括协议、主机名称、端口号），默认为 file:/// -->
<property>
<name>fs.defaultFS</name>
<!-- 用于指定NameNode的地址 -->
<value>hdfs://localhost:9000</value>
</property>
<!-- Hadoop运行时产生文件的临时存储目录 -->
<property>
<name>hadoop.tmp.dir</name>
<value>/root/hadoopData/temp</value>
</property>
```

4. 配置文件系统`hdfs-site.xml`

``` shell
vim /root/software/hadoop-2.7.7/etc/hadoop/hdfs-site.xml
```

- 将下面的配置内容添加到 `<configuration></configuration>` 中间：

``` xml
<!-- NameNode在本地文件系统中持久存储命名空间和事务日志的路径 -->
<property>
<name>dfs.namenode.name.dir</name>
<value>/root/hadoopData/name</value>
</property>
<!-- DataNode在本地文件系统中存放块的路径 -->
<property>
<name>dfs.datanode.data.dir</name>
<value>/root/hadoopData/data</value>
</property>
<!-- 数据块副本的数量，默认为3 -->
<property>
<name>dfs.replication</name>
<value>1</value>
</property>
```

5. 配置 Hadoop 系统环境变量

``` shell
vim /etc/profile

# 文件末尾添加如下
export HADOOP_HOME=/root/software/hadoop-2.7.7
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
```

- 重载更新配置文件

``` shell
source /etc/profile
```

- 检测 Hadoop 是否安装成功并查看版本

``` shell
hadoop version
```

6. 格式化文件系统

``` shell
hdfs namenode -format
```

7. 脚本一键启动 HDFS 集群

``` shell
start-dfs.sh
```

8. 查看进程启动情况

``` shell
jps
```

9. 通过 UI 查看 HDFS 运行状态

>PS：通过浏览器访问http://ip:50070查看HDFS集群状态



### YARN伪分布式集群搭建

1. 配置环境变量`yarn-env.sh`

``` shell
vim /root/software/hadoop-2.7.7/etc/hadoop/yarn-env.sh
```

- 修改`JAVA_HOME`参数为JDK实际位置

<!-- ![修改JAVA_HOME参数为JDK实际位置](https://uss.useenet.cn/picgo/20200621142749.png) -->
{{< image src="https://uss.useenet.cn/picgo/20200621142749.png" caption="修改JAVA_HOME参数为JDK实际位置">}}

2. 配置计算框架`mapred-site.xml`

- 在`$HADOOP_HOME/etc/hadoop/`目录中默认没有该文件，需要先通过如下命令将文件**复制并重命名为`mapred-site.xml`**：

``` shell
cp mapred-site.xml.template mapred-site.xml
```

- 修改`mapred-site.xml`文件

``` shell
vim /root/software/hadoop-2.7.7/etc/hadoop/mapred-site.xml
```

- 添加如下内容

``` xml
<!-- 指定使用 YARN 运行 MapReduce 程序，默认为 local -->
<property>
<name>mapreduce.framework.name</name>
<value>yarn</value>
</property>
```

3. 配置YARN系统`yarn-site.xml`

``` shell
vim /root/software/hadoop-2.7.7/etc/hadoop/yarn-site.xml
```

- 将下面的配置内容加入中间：

``` xml
<!-- NodeManager上运行的附属服务，也可以理解为 reduce 获取数据的方式 -->
<property>
<name>yarn.nodemanager.aux-services</name>
<value>mapreduce_shuffle</value>
</property>
```

4. 脚本一键启动 YARN 集群

``` shell
start-yarn.sh
```

5. 查看进程启动情况

``` shell
jps
```

6. 通过 UI 查看 YARN 运行状态

> PS：通过浏览器访问http://ip:8088查看YARN集群状态
### Hadoop集群初体验

1. 启动 Hadoop 集群

- HDFS集群

``` shell
start-dfs.sh
```

- YARN集群

``` shell
start-yarn.sh
```

2. WordCount 示例执行流程

- 在本机桌面`/Desktop`上创建一个名为`inputdata`的文件夹，在此文件夹下新建一个名为`word.txt`的文本文件，内容如下：

``` 
hadoop jar hadoop mapreduce
hadoop hdfs
hdfs hadoop jar fs
fs
```

>PS：注意单词之间用`空格`进行分隔

- 接着，在 HDFS 上创建`/wordcount/input`目录，并将`word.txt`文件上传至该目录下，具体指令如下所示：

``` shell
hadoop fs -mkdir -p /wordcount/input
hadoop fs -put /headless/Desktop/word.txt /wordcount/input
```

- 进入`$HADOOP_HOME/share/hadoop/mapreduce/`目录下，使用 `hadoop-mapreduce-examples-2.7.7.jar`示例包，对 HDFS 上的`word.txt`文件进行单词统计，在 jar 包位置执行如下命令：

``` shell
hadoop jar hadoop-mapreduce-examples-2.7.7.jar wordcount \ 
/headless/Desktop/word.txt /wordcount/output
```

> PS：`\`为换行指令（可以写成一行，不使用换行符）

- 程序执行成功后，我们可以使用 HDFS Shell 的相关指令查看 part-r-00000 的内容，具体指令如下所示：

``` shell
hadoop fs -cat /wordcount/output/part-r-00000
```



## Day Two

### 初识Hive



### Hive架构原理



### Hive内嵌模式安装

1. Hive安装
- 解压安装包
- 配置环境变量

2. 内嵌模式安装

- 修改配置文件`hive-env.sh`
- 初始化元数据库
- Hive 连接



### Hive本地模式安装

1. 安装 MySQL

- 解压安装包
- 安装 MySQL 组件，顺序为：
>common ——> libs ——> libs-compat ——> client ——> server
- 登录 MySQL
  - 初始化 MySQL 的数据库
  - 启动 MySQL 服务
  - 登录 MySQL
  - 重置 MySQL 密码

- 增加远程登录权限

2. Hive 安装部署

- 解压安装包
- 配置环境变量：`/etc/profile`文件
- 修改配置文件：`hive-env.sh`

3. Hive元数据配置到MySQL

- 驱动拷贝：将MySQL驱动包 `mysql-connector-java-5.1.47-bin.jar` 拷贝到 `${HIVE_HOME}/lib` 目录下。
- 配置 `Metastore`到MySQL：`hive-site.xml`
- 初始化元数据库
- `Hive`连接

### Hive常见属性配置

1. Hive 运行日志信息配置

- 在Hive中，使用的是 Log4j 来输出日志，
>默认情况下，CLI 是不能将日志信息输出到控制台的。

- 默认的日志存放在`/tmp/${user.name}`文件夹的`hive.log`文件中，全路径就是`/tmp/${user.name}/hive.log`。

- 现要求将 Hive 的日志存放路径修改为 `/root/hive/logs`，日志文件为`myhive.log`。

## Day Three

### requests练习



### xpath练习



