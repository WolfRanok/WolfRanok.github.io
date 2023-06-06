---
layout: post
title: 大数据技术原理与应用
author: Ranok
tags: [big data,java ,期末考试]     #标签会影响
feature-img: "assets/img/feature-img/bigdata.jpg" # 这是一个会出现在博客文章内部的图片
thumbnail: "assets/img/thumbnails/feature-img/bigdata.jpg" # 这是一个会出现在博客外部的图片
permalink: bigdata # 这条会将该界面的URL自定义
---

&emsp;&emsp;“大数据技术原理与应用”是一门介绍大数据技术的课程。通过学习这门课程，学生可以深入了解大数据技术的原理和应用，并学会如何使用各种工具和技术来处理和管理大数据。此外，该课程还涵盖了大数据架构、设计和性能优化等方面的内容，这些知识对于开展大规模数据处理和分析项目非常重要。因此，“大数据技术原理与应用”对于计算机科学和数据科学领域的学生和从业人员，以及对大数据感兴趣的其他人士都有很大的意义。

---
# 前言
&emsp;&emsp;本博客是本人反复听了上课的28分钟录音，听了8个小时左右辛苦肝出来的。如果你可以看到这篇博客，说明我对你有足够的信任，请不要辜负这份信任。

> 未经本人允许，请不要分享本博客出去，分享方式包括但不限于分享链接，截图等。

---
# 考题整理

## 客观题部分（50分）

### 1. Hadoop运行模式有哪些？

1. 单机模式
2. 伪分布式模式
3. 完全分布式模式

---

### 2. 单机模式和伪分布式模式的区别

&emsp;&emsp;单机模式：Hadoop只在一台机器上运行，存储采用本地文件系统，没有采用分布式翁建系统HDFS。<br>
&emsp;&emsp;伪分布式：Hadoop存储采用分布式文件系统HDFS，而且HDFS的名称结点和数据结点位于集群的不同机器上。

---

### 3. 伪分布式的安装

#### 3.1 Hadoop的开发和运行需要什么环境？

&emsp;&emsp;需要Java环境在hadoop-env.sh 中配置

#### 3.2 伪分布式的安装需要修改哪些配置文件？

&emsp;&emsp;需要修改文件：core-site.xml hdfs-site.xml


#### 3.3有关fs.defaultFS的配置的两种问法

##### 3.3.1问法一：fs.defaultFS的参数在哪一个配置文件中进行配置？

&emsp;&emsp;在sore-site.xml中配置

##### 3.3.3问法二：配置NameBode地址时由哪一个参数指定的

&emsp;&emsp;由core-site.xml中的dfs.namenode.dir.参数指定

---

### 4 Hadoop的核心功能组件

> 可能会考填空或简答。

#### 4.1 填空的问法：请列举出两个除hdfs和MapReduce之外的两个文件

1.	HBase
2.	Hive
3.	Pig
4.	Mahout
5.	ZooKeeper
6.	Flume
7.	Sqoop
8.	Ambari

#### 4.2 简答题的问法：请举两个核心组件并说明其作用

1.	HBas：是一个提供高可靠性、高性能、可伸缩、实时读写、分布式的列式数据库
2.	Hive：是一个数据库工具
3.	Pig：是一种数据流语言和运行环境
4.	Mahout：是一个开源的项目，它提供了一些课扩展的机器学习领域经典算法的实现
5.	ZooKeeper：是一个高效和可靠的协同工作系统。5 Namenode

---

### Namenode

> Datanode会定时的为Namenode发送心跳

#### 5.1用于存储数据块信息的目录结构的是哪一个结点？

&emsp;&emsp;Namenode

#### 5.2 从功能的角度分析Namenode主要用于存储什么信息（不确定）

&emsp;&emsp;NameNode存储着文件系统树以及文件树中所有的文件和文件夹的元数据信息

#### 5.3在HDFS中保存着两个数据结构，请说明这两个数据结构是什么，有什么用？

&emsp;&emsp;这两个数据结构分别是FsImage和Editlog。<br>
&emsp;&emsp;FsImageL用于维护文件系统树以及文件树中所有的文件和文件夹的元数据。<br>
&emsp;&emsp;EditLog用于操作日志文件以及记录了所有针对文件的创建、删除、重命名等操作。<br>

---

#### 6 DataNode的主要功能是什么？

&emsp;&emsp;负责管理它所在结点上存储的数据的读写,及存储数据（存放数据）<br>

> DataNode和DataNode之间会进行进程通信

---

### 7 Hadoop集群主要瓶颈是什么？

&emsp;&emsp;不是CPU，主要瓶颈是**磁盘IO**

---

### 8 ssh免密登录是为了什么/目的是什么？

1.	启动集群不需要输入密码
2.	进程之间可以免密通信
3.	免密登录**不是必须的**


---

### 9 Hadoop的启停命令

1.	start-all.sh：启动所有的Hadoop守护进程
2.	stop-all.sh：停止所有的Hadoop守护进程
3.	start-dfs.sh：启动Hadoop HDFS守护进程NameNode、SecondaryNameNode和DataNode
4.	stop-dfs.sh：停止Hadoop HDFS守护进程NameNode、SecondaryNameNode和DataNode
5.	单独启动某个进程：hadoop-daemons.sh start name
6.	单独关闭某个进程：hadoop-daemons.sh stop name

---

### 10 Hadoop是否支持随机读取

&emsp;&emsp;**不支持**

---

### 11 ：指令相关

#### 11.1列举**两个**HDFS常用的shell命令

1.	Hadoop fs -ls <path> 用于展示在指定目录<path>下的文件详细信息
2.	Hadoop fs -cat <path> 将指定文件的内容输出到标准输出
3.	Hadoop fs -mkdir [-p] <path> 创建一个或多个文件夹，-p选型用于递归的创建子文件夹
4.	Hadoop fs -cp <src> <dst> 将文件从源路径<src>复制到目标路径<dst>

#### 11.2 列举两个常用的java API

1.	org.apache.hadoop.fs.FSDataInputStream：文件输入流，用于读Hadoop文件
2.	org.apache.hadoop.fs.FSDataOutputStream:文件输出流，用于写Hadoop文件
3.	org.apache.hadoop.fs.Path：用于表示hadoop文件系统中一个文件或者目录的路径

---

### 12 Hadoop的特性

#### 12.1 简答题的写法（写5个，不需要解释）：

1.	高可靠性
2.	高效性
3.	高可扩展性
4.	高容错性
5.	成本低
6.	运行的在linux系统上
7.	支持各种编程语言

#### 12.2 填空题的写法（挑两个即可）：

1.	高可靠性
2.	高效性
3.	高可扩展性
4.	高容错性
5.	成本低
6.	运行的在linux系统上
7.	支持各种编程语言

---

## 综合应用（50分）

### 13 Hive

&emsp;&emsp;大致题面：br

&emsp;&emsp;给你一段数据（两种数据）：

&emsp;&emsp;第一种：100 \t zhansan \t 18<br>
&emsp;&emsp;第二种：100，zhansan，18

#### 13.1 使用HQL语言创建一个数据库,并指定路径

&emsp;&emsp;use 指定的数据库;

&emsp;&emsp;如果是第一种数据则写：<br>
&emsp;&emsp;create table table_name(hight int, name string,age int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ‘\t’

&emsp;&emsp;如果是第二种数据则写：<br>
&emsp;&emsp;create table table_name(hight int, name string,age int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ‘,’

#### 13.3 装载数据

&emsp;&emsp;load data [local] inpath <path路径> into table <这里写刚才创建的数据表名>

> 这里local表示在本地文件中获取，即如果在本地才需要加上

#### 13.4 删除（非空）数据库

&emsp;&emsp;drop database <数据库名称> cascade

---

### 14 Hbase
#### 14.1 设计逻辑结构
&emsp;&emsp;题面：给你一个json串，设计一个逻辑结构

{% include aligner.html images="blog-img/bigdata/1.png" column=1 %}

&emsp;&emsp; 答

{% include aligner.html images="blog-img/bigdata/2.png" column=1 %}

##### 14.2 如何确定一个单元格？

&emsp;&emsp;以下面这个为例。

{% include aligner.html images="blog-img/bigdata/3.png" column=1 %}

&emsp;&emsp; 现在以确定一个姓名为LiuJun的人为例：<br>
**行键**“201505002”，**列族**“info”**限定符**“email”和**时间戳**“1230016521”这四个坐标值确定的单元格[“201505002”,”Info”,”email”,”1230016521”]

##### 14.2.2问法二：我们的单元格是通过坐标来决定的，这四维坐标分别是什么？

```python
[“行键”,”列族”,”列限定符”,”时间戳”]
```

#### 14.3 创建表 

以第一题的表格为例：

```SQL
create 'myTable', {NAME => 'personal_info'}, {NAME => 'office_info'}
```
#### 14.4 插入数据

&emsp;&emsp;可以使用 put 命令向 HBase 表格中的特定单元格添加数据。以下是向名为 myTable 的表格中，行键为 row1，列族为 cf1，列名为 column1 的单元格添加数据的示例：

```SQL
put 'myTable', 'row1', 'cf1:column1', 'value1'
```

&emsp;&emsp;其中，myTable 是表格的名称，row1 是行键，cf1 是列族名称，column1 是列名。要将值 value1 添加到该单元格，请将其作为最后一个参数传递给 put 命令。

---

### 15 mapreduce

#### 15.1MapReduce的编程规范

用户编写的程序分成三个部分：

**1：Mapper**
1. 用户自定义的Mapper要继承自己的父类
2. Mapper的输入数据是KV对的形式（KV类型可自己定义）
3. Mapper中的业务逻辑写在map0方法中
4. Mapper的输出数据是KV对的形式（KV类型可自定义）

**2：Reducer**
1. 用户自定义的Reducer要继承自己的父类
2. Reducer的输入数据类型对应Mapper输出数据类型
3. Reducer中的业务逻辑写在reduceO方法中
4. ReduceTask进程对每一组相同K的<kv>组调用一次reduce()方法

**3：Driver**<br>
相当于Yam集群的客户端，用于提交我们整个程序到YARN集群，提交的是封装了MapReduce程序相关运行参数的job对象。

#### 15.2自定义数据类型


1. 实现Writable接口
2. 空参构造
3. 重写序列化方法
4. 重写反序列化方法
5. 如果需要把结果显示在文件中，则需要重写toString()
6. 如果需要将自定义的bean放在key中传输，则要实现Comparable接口

#### 15.3代码实现

##### 第一套卷子考点：map逻辑实现

{% include aligner.html images="blog-img/bigdata/4.png" column=1 %}

##### 15.3.2第二套卷子考点：Driver逻辑实现

&emsp;&emsp;7点全要考
{% include aligner.html images="blog-img/bigdata/5.png" column=1 %}