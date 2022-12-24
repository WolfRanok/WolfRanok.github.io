---
layout: post
title: OpenStack
author: Ranok
color: brown
tag: [OpenStack,期末考试]
thumbnail: "assets/img/thumbnails/feature-img/openstack.png"
permalink: openstack
---
OpenStack是Rackspace和NASA共同成立的一个开源项目，它是为云计算服务的，提供存储空间、计算能力等资源服务的Web Service。简单来说，OpenStack就是一个操作系统，一套软件，一套IaaS（基础设施即服务）软件，对资源进行管理，并且以服务的形式提供给上层应用或者用户去使用。

---

## 前言

以下为openstack的期末复习，考试考点整理，内容比较多且知识点生僻难懂，请好好准备，祝愿各位可以在期末获取一个好成绩！

---

## 第一章考点
#### 什么是云计算
云计算是一种把计算机基础资源经过重组后给用户使用的一系列相关服务。

#### 云计算架构对应几种架构模式以及概念
IaaS（基础设施即服务）<br>
PaaS（平台即服务）<br>
SaaS（软件即服务）

#### OpenStack 的主要项目以及对应的项目名称


| 服务 | 直译 | 项目名称 |
| -   | -   | -   |
| Dashboard  | 仪表盘   | Horizon   |
| Computer   | 计算   | Nova   |
| Natwork   |  网络 | Neutron  |
| Object Storage   | 对象存储  | Swift  |
| Block Storage  | 块存储  | Cindar  |
| Identity | 身份| Keystone |
| Image|镜像 | Glance|
| Telemetry | 计量 | Ceilometer |
| Orchestration | 编排 | Heat |
| Database | 数据库 | Trove |
|Data Processing| 数据处理 | Sahara |

---

## 第二章考点
#### 网络配置流程

1. 进入网络配置的文件：`vi  /etc/sysconfig/netwrok-scripts/ifcfg-ens33`<br>
2. 修改`BOOTPROTO`的值为`static` <br>
3. 修改`ONBOOT`的值为`yes`<br>
4. 添加配置4条信息：`IPADDR NETNASK GATEWAY DNS1`<br>
5. 键入`qw`保存并退出配置文件
6. 输入：`systemctl restart network` 重启`network`服务。

#### openstack的安装

1. 安装openstack-packstack以及其依赖包：`yum install -y openstack-packstack`
2. 安装openstack：`packstack --allinone`
3. 进入文件查看生成的初始密码配置：`vi /etc/my.cnf.d/server.cnf`

---

## 第三章考点

### 数据库
#### 1.数据库验证
验证方式：`systemctl status sqlname`

#### 2. 数据库有哪些
NoSQL数据库：`MongoDB Memcached Redis`<br>
SQL数据库：`MySQL Maria PostgreSQL`

### 消息队列
#### 什么是消息队列
消息队列是一种应用程序对应用程序的通信方法。消息传递指的是程序之间通过打消良中发送数却进行通信,而不是通过百捉调用彼此来通信。

#### 消息队列实现的协议以及对应的软件
协议：AMQP<br>
软件：RabbitMQ

---

## 第四章考点

#### REST 含义解释
RESTFUL是一种网络应用程序的设计风格和开发方式，是我们用http调用资源的时候的统一接口的访问形式，用自己的话说就是把对资源的调用转化到一种表现方式上来，例如开发的时候使用微信小程序表现可以避免用不同的语言开发app应用

#### 调用OpenStack API的四种方式
1. cURL <br>
2. OpenStack命令行客服端<br>
3. REST客户端<br>
4. OpenStack的Python SDK

#### OpenStack 的认证与API 请求流程

1. 向云管理员提供的身份端点请求一个认证令牌。
2. 如果请求成功，服务器会返回一个认证令牌。
3. 发送API请求，并在X-Auth-Token头部包括上一步返回的认证令牌。可以一直使用这个令牌发送API请求，直到服务完成该请求，或者出现未授权(401)的错误。
4. 如果遇到未授权（401）的错误，则需要重新请求另一个令牌。

##### 获取OpenStack认证令牌

1. 进入demo环境：`source keystonerc_demo`
2. 运行命令cURL来请求一个令牌。

##### 发送API请求

1. 设置OS_TOKEN环境变量，将其值设为令牌ID： `export OS_TOKEN=令牌ID`
2. 设置OS_PROJECT_NAME环境变量：`export OS_PROJECT_NAME=demo`
3. 设置OS_COMPUTE_API环境变量：`export OS_COMPUTE_API=http://192.168.199.21:8774/v2.1`
4. 使用Compute API列出示例类型：`curl -s -H "X-Auth-Token: $OS_TOKEN" $os_COMPUTE_API/flavors lpython -m json.tool`。

---
## 第五章

#### Keystone的管理层次结构

{% include aligner.html images="blog-img/openstack/Keystone.bmp" column=1 %}

问：在一个域中的用户`User1`是否可以管理项目`Project1`

答：可以，因为用户User1是系统管理员，拥有对项目Project1的管理权限。

---
#### Keystone认证流程图
这张图需要背下来。

{% include aligner.html images="blog-img/openstack/KeystoneWWork.bmp" column=1 %}

对图片的解释：

1. 用户向Keystone提供凭证，Keystone验证通过后向用户返回令牌的同时还会返回一个通用目录。
2. 用户使用该令牌向该目录列表中的端点请求该用户对应的项目信息，Keystone验证通过后返回用户对应的项目列表
3. 用户从列表中选择要访问的项目再次向Keystone发出请求，Keystone验证通过后返回管理该项目的服务列表，并允许访问该项目的令牌。
4. 用户会通过这个服务和通用目录映射找到服务的端点，并通过端点找到实际服务组件的位置。
5. 用户在凭借项目令牌和端点来访问实际上的服务组件。
6. 服务组件会向Keystone提供这个用户项目令牌进行验证，Keystone验证通过后会返回一系列的确认信息和附加信息给服务
7. 服务执行一系列操作。

#### 罗列命令行操作
1. 列出可用角色：`openstack role list`<br>
2. 创建角色：`openstack role create new-role`<br>
3. 分配角色：`openstack role add --user 用户名或ID --oject项目名或ID角色名或ID`<br>
4. 查看角色详细信息：`openstack role show角色名或ID`<br>
5. 删除角色：`openstack role remove --user 用户名或ID--project用户名或ID角色名或ID`

---

## 第六章
#### 常用的镜像格式以及容器

镜像格式：`qcwr`<br>
不用容器使用`bare`代替<br>
使用容器可以在`ovf ova aki ari docker`中选择

#### openstack中创建镜像的流程
创建镜像，转成快照

1. 获取实例啃决照的文件路径，可通过查看其详细信息中的“ID”值。<br>
2. 其中执行openstack image create 创建新的镜像：`openstack image create "entOS7-img"--file varlib/glance/limages/快照id --disk-format qcow2--container-format bare`<br>
3. 新创建的镜像类型变为镜像(image) .<br>

---
## 第七章

#### 虚拟机实例化的流程
1. 首先用户（可以是OpenStack最终用户，也可以是其他程序）执行Nova Client提供的用于创建虚拟机的命令。<br>
2. nova-api服务监听到来白于Nova Client的HTTP请求,并将这些请求转换为AMQP消息之后加入消息队列。<br>
3. 通过消息队列调用nova-conductor报务。<br>
4. nova-conductor服务从消息队列中接收到虚拟机实例化请求消息后,进行一些准备工作。<br>
5. nova-conductor服务通过消息队列告诉nova-scheduler服务去选择一个合适的计算节点来创建虚拟机，此时nova-scheduler会读取数据库的内容。<br>
6. nova-conductor服务从nova-scheduler服务得到了合适的将计算节点的信息后，在通过消息队列来通知nova-compute服务实现虚拟机的创建。<br>


## 其他
#### 配置文件中对两个值的解释

##### "" 空字符串
表示“always”（总是）

##### "!" 感叹号
表示“nerver”或者“nobady”，即拒绝。

## 小知识点

1. `oslo.policy`是`json`格式的文件。
2. `openstack`是使用`python`语言实现的。