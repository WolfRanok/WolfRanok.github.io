---
layout: post
title: OpenStack 期末复习
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

## OpenStack 的主要项目以及对应的项目名称


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

## 第四章考点

#### REST 含义解释
REST 是 Representational State Transfer 的缩写，通常译为**表现层状态转化**

客户端在使用HTTP提供的四种操作（GET、POST、PUT、DELETE）访问服务器上的资源时，这些操作会让服务端的状态发生转化，而这种转化是建立在表现层之上的，所以被称之为表现层转化。

---
#### OpenStack 的认证与API 请求流程

1. 向云管理员提供的身份端点请求一个认证令牌。
2. 如果请求成功，服务器会返回一个认证令牌。
3. 发送API请求，并在X-Auht-Token头部包含上一步返回的令牌认证。
4. 如果遇到未授权（401）的错误，则需要重新请求另一个令牌。

##### 获取OpenStack认证令牌

1. 进入demo环境：`source keystonerc_demo`
2. 运行命令cURL来请求一个令牌。

##### 发送API请求

1. 设置OS_TOKEN环境变量，将其值设为令牌ID： `export OS_TOKEN=令牌ID`
2. 设置OS_PROJECT_NAME环境变量：`export OS_PROJECT_NAME=demo`
3. 设置OS_COMPUTE_API环境变量：`export OS_COMPUTE_API=http://192.168.199.21:8774/v2.1`
4. 使用Compute API列出示例类型。

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

#### 配置文件中对两个值的解释

##### "" 空字符串
表示“always”（总是）

##### "!" 感叹号
表示“nerver”或者“nobady”，即拒绝。

## 小知识点

1. `oslo.policy`是`json`格式的文件。
2. `openstack`是使用`python`语言实现的。