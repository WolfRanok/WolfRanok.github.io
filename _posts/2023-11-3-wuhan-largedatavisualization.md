---
layout: post
title: 大数据可视化
author: TraSorrow
tag: [python,大数据]
color: brown
permalink: largedatavisualization
thumbnail: assets/img/thumbnails/feature-img/largedatavisualization.jpg # 文件路径在github还是只支持正斜杠'/'
---

&emsp;&emsp;大数据可视化是指将庞大的数据集通过图表、地图、仪表盘等可视化工具呈现出来，使人们能够直观地理解和分析数据。它是数据分析和决策过程中的重要工具，有助于揭示数据背后的模式、趋势和关联关系，帮助用户更好地理解数据，并根据数据进行决策。

> 温馨提示：如果你觉得界面配色有些刺眼，你可以点击右上角的菜单，选择使用圆形按钮切换主题背景。

<a id="article_top"></a>

---
# 目录

- [目录](#目录)
- [前言](#前言)
- [题目部分](#题目部分)
  - [选择题](#选择题)
      - [1. 哪些图形适合显示多维数据:](#1-哪些图形适合显示多维数据)
      - [2. 哪些图形适合显示时间序列数据:](#2-哪些图形适合显示时间序列数据)
      - [3. 哪些图形适合显示分类数据:](#3-哪些图形适合显示分类数据)
      - [4. 哪些图形适合显示离散数据:](#4-哪些图形适合显示离散数据)
      - [5. 哪些图形适合显示二元数据:](#5-哪些图形适合显示二元数据)
  - [填空题:](#填空题)
      - [1. 条形图通常显示哪些数据:](#1-条形图通常显示哪些数据)
      - [2. 散点图用于显示什么类型的数据:](#2-散点图用于显示什么类型的数据)
      - [3. 直方图用于显示什么类型的数据:](#3-直方图用于显示什么类型的数据)
      - [4. 饼图用于显示什么类型的数据:](#4-饼图用于显示什么类型的数据)
      - [5. 折线图用于显示什么类型的数据:](#5-折线图用于显示什么类型的数据)
  - [问答题](#问答题)
    - [1.简述数据可视化流程](#1简述数据可视化流程)
    - [2.简述数据可视化常用的工具](#2简述数据可视化常用的工具)
    - [3.简述数据可视化可以用于哪些行业(至少五个)](#3简述数据可视化可以用于哪些行业至少五个)
    - [4.简述可视化的意义(至少三条)](#4简述可视化的意义至少三条)
    - [5.pandas中可以读取多种文件格式,常用的文件格式有哪几种](#5pandas中可以读取多种文件格式常用的文件格式有哪几种)
    - [6.据清洗有哪些方法](#6据清洗有哪些方法)
    - [7.异常值检测有哪些方法(两种基本方法):](#7异常值检测有哪些方法两种基本方法)
    - [8.可视化哪些图像适合对比,为什么适合](#8可视化哪些图像适合对比为什么适合)
    - [9. 编程题:](#9-编程题)
      - [9.1 阅读以上代码回答问题:](#91-阅读以上代码回答问题)
      - [9.1.1 encoding	是哪一个类型的参数:](#911-encoding是哪一个类型的参数)
      - [9.1.2 如果要把data3和data4按照B列合并,请写出合并代码:](#912-如果要把data3和data4按照b列合并请写出合并代码)
      - [9.2 根据图表来回答问题:](#92-根据图表来回答问题)
      - [9.2.1 请根据表的数据分析可以从哪几个角度可视化,并写出理由:](#921-请根据表的数据分析可以从哪几个角度可视化并写出理由)
      - [9.2.2 根据上题中选取一种可视化的需求,写出完整代码](#922-根据上题中选取一种可视化的需求写出完整代码)

---
# 前言
&emsp;&emsp;本博客针对，大数据可视化期末考试进行整理。材料内容由 **TraSorrow**同学亲情提供，本人只做整理排版工作。内容不多，祝你取得一个**好成绩**！。

---

# 题目部分

&emsp;&emsp;题型主要有，选择题、填空题、问答大题（包含编程题）组成。<br> &emsp;&emsp;内容如下仅供参考。

---

## 选择题

#### 1. 哪些图形适合显示多维数据:

    直方图

#### 2. 哪些图形适合显示时间序列数据:
    
    折线图

#### 3. 哪些图形适合显示分类数据:
    
    条形图

#### 4. 哪些图形适合显示离散数据:
    
    散点图

#### 5. 哪些图形适合显示二元数据:
    
    散点图

--- 

## 填空题:

#### 1. 条形图通常显示哪些数据:

    分类数据

#### 2. 散点图用于显示什么类型的数据:

    离散数据

#### 3. 直方图用于显示什么类型的数据:

    连续数据

#### 4. 饼图用于显示什么类型的数据:
    
    离散数据

#### 5. 折线图用于显示什么类型的数据:
    
    连续数据

---

## 问答题

### 1.简述数据可视化流程

    1. 采集数据
    2. 数据处理和变换
    3. 可视化映射
    4. 人机交互以及用户感知

### 2.简述数据可视化常用的工具
    
    1. Tableau
    2. dataV
    3. ECharts
    4. FineBl
    5. Python numpy Matplotlib库
    6. Excel


### 3.简述数据可视化可以用于哪些行业(至少五个)
    
    1. 金融行业
    2. 教育行业
    3. 天气预报
    4. 医疗行业
    5. 物流行业

### 4.简述可视化的意义(至少三条)

    1. 通过图形化手段清晰有效地传达与沟通信息
    2. 帮助人更好的分析数据
    3. 帮助企业从信息中提取知识、从知识中收获价值

### 5.pandas中可以读取多种文件格式,常用的文件格式有哪几种

    1. CSV文件
    2. Excel文件
    3. JSON文件
    4. 压缩文件(.zip等)
    5. 文本文件(.tsv,.txt等)

### 6.据清洗有哪些方法

    1. 去除空值
    2. 缺失值填充
    3. 重复值处理
    4. 数据标准化

### 7.异常值检测有哪些方法(两种基本方法):

    1. 箱线图法
    2. Z-Score法
    3. IQR法
    4. 散点图法
    5. 直方图
    6. 线图

### 8.可视化哪些图像适合对比,为什么适合
    1.  柱状图 原因: 可以通过柱子的高度可以直观地展示数值之间的差异
    2.  饼图 原因: 可以通过扇形面积和角度来比较不同类别的数据
    3.  条形图 原因: 可以通过不同长度的条形可以清晰地比较各个类别的数值大小
    4.  线状图 原因: 通过线条的起伏变化可以反映出一个序列中的趋势和规律
    5.  散点图：原因散点图通过点的分布情况，可以直观地展示两个变量之间的关联程度。

---

### 9. 编程题:

``` python

    Import pandas as pd
    
    data1 = pd.read_csv(“F:\\tmp\\数据1.csv”,encoding=’gb18030’)
    
    data2 = pd.read_csv(“F:\\tmp\\数据2.csv”,encoding=’gb18030’)
    data3 = pd.DataFrame({‘A’:[‘a1’,’a2’,’a3’],’B’:[‘b1’,’b2’,’b3’],’C’:[‘c1’,’c2’,’c3’]})
    data4 = pd.DataFrame({’B’:[‘b2’,’b3’,’b4’],’D’:[‘d2’,’d3’,’d4’]})

```

#### 9.1 阅读以上代码回答问题:

#### 9.1.1 encoding	是哪一个类型的参数:
    
    关键字参数

#### 9.1.2 如果要把data3和data4按照B列合并,请写出合并代码:
    
    merged_data = pd.merge(data3, data4, on='B', how='outer')

---
 
{% include aligner.html images="blog-img/largedatavisualization/1.jpg" %}

#### 9.2 根据图表来回答问题:

#### 9.2.1 请根据表的数据分析可以从哪几个角度可视化,并写出理由:
    
    可以选择两个角度考虑年度和指标
    在国民总收入,比较随着年度的变化,收入总量的变化趋势
    还可以根据某一年不同指标之间的比较来获取数据信息

#### 9.2.2 根据上题中选取一种可视化的需求,写出完整代码

> 注意本题代码老师并未透露。且题目也可能变化，为了避免误导此处不展示代码示例。

[回到顶部](#article_top)