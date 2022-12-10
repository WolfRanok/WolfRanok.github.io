---
layout: post
title: 机器学习期末考试
author: Ranok
color: brown
tag: [机器学习,期末考试,python]
thumbnail: "assets/img/thumbnails/feature-img/machinelearning.png"
permalink: machinelearning
---

今天的人工智能主要依赖的不再是符号知识表示和程序推理机制，现代 AI 而是建立在新的基础上，即机器学习。无论是传统的基于数学的机器学习模型或决策树，还是深度学习的神经网络架构，当今人工智能领域的大多数 AI 应用程序都是基于机器学习技术。

---

## 前言
机器学习是智能专业的专核心课，其科目本身的难度较高，不论是在于理论层面还是代码实现层面都有一定的难度。想要征服机器学习还是一件非常具有挑战性的事情。

本次博客整理了有关机器学习课程的期末考试重点，希望同学们可以获得一个好成绩。

---

## 问题一：有关拟合的问题
#### 什么是过拟合和欠拟合？

过拟合是指模型在训练集上表现很好，到了验证和测试阶段就很差，即模型的泛化能力很差。
欠拟合是指模型在训练集上表现的不好，以至于在验证和测试阶段表现的也比较差。

#### 如何解决过拟合与欠拟合？
##### 过拟合的解决方法：
1.	重新调整一下参数和超参数。
2.	对数据进行特征降维处理，有选择性的抛弃一些特征。
3.	降低模型的复杂度。
4.	使用正则化约束。

##### 欠拟合的解决方法：
1.	增加模型的复杂度，例如使用神经网络代替线性回归、用随机森林代替决策树。
2.	考虑选用更多更具有代表意义的特征的数据特征。
3.	重新调整一下参数和超参数。
4.	降低正则化约束。

#### 决策树如何防止过拟合
剪枝。

---
## 问题二：回归模型与分类模型的区别是什么？请举例说明。

回归模型：是对连续变量，进行预测的模型，即回归问题是定量问题。<br>
回归模型问题的举例：对某城市房价预测、对某地区空气湿度的预测。

分类模型：是对离散变量、进行预测的模型，即分类问题是定类问题。<br>
分类模型问题的举例：对明天是否下雨的预测、判断病人是否患有某种疾病的预测。

---
## 问题三：机器学习的四大问题是什么？
回归、分类、聚类、降维。

---
## 问题四：机器学习的一般步骤。（需要以某一实物为例）
#### 回归问题以披萨价格预测为例。
##### 明确任务收集数据。
在一定范围内的各个城市中随机选取若干家披萨店，作为初始数据。
##### 数据分析与预处理。
将数据特征初步定为以下几项：

比萨的尺寸、披萨的脂肪含量、披萨的制作成本、披萨的口味、披萨的品牌、披萨所在城市的GDP水平、生产披萨的披萨店的知名度。

分析这些特征是否出现缺失值，对缺失值较多的特征直接删除。对缺失值较少的使用平均值填补定量的特征（例如披萨的脂肪含量），使用众数填补定类的特征（例如披萨的口味）。

将定类数据数值化，方便后期计算。

使用灰色关联分析法有选择性地剔除关联度较小的几个特征，即进行降维与特征选择处理。

##### 模型训练

选择使用线性回归解决该回归问题。

##### 模型评估与参数调优

R2评估，模型的优劣，当R2的值越接近1时模型性能越好。
使用k折交叉验证方法选取出最佳的学习率等参数并再次进行模型训练。

##### 模型应用

将训练模型保存下来，并公布用以推广。

---

## 问题五：k折交叉验证的简述。

k折交叉验证常用于参数调优，使得更容易训练出较高性能的模型。

k折交叉验证的工作流程：<br>
1. 将训练集随机地进行k块、并选出其中1块作为验证集。
2. 用其余k-1块的数据进行训练，并用验证集，计算出这一次的误差。
3. 重复k次以上步骤，每次选取不同的块作为验证集
4. 统计每一次计算得到的误差估计，并取平均值作为本次训练参数的最终指标。

---

## 问题六：模型的评估标准
#### 回归问题的评估标准
1.  MSE（均方误差） 预测残差的平方和，数值越小越好。
2.  RMSE（平均绝对误差）是在MSE的基础上开根号计算得到，同样数值越小越好。
3.  MAE（平均绝对误差）预测残差的绝对值之和，值越小越好。
4.  R2 (R方分数)既考虑预测值与真值之间的差异又考虑问题本身与真值之间的差异。结果的约接近于1越好。
#### 分类问题的评估标准
1.  正确率（Accuracy）即被预测正确的样本在所有预测样本中的占比。
2.  召回率(TRR) 即在所有真的正类中被模型预测出来的比例。
3.  AUC值：AUC的概率意义是随机取一对正负样本，正样本得分大于负样本得分的概
 AUC的范围在[0, 1]之间，并且越接近1越好，越接近0.5属于乱猜

---

## 问题七：决策树的建立（以ppt为例）
#### 考察公式：

信息熵公式：$$H(X)=\sum_{i=1}^{n}p_i log_2^{\frac{1}{p_i}}=-\sum_{i=1}^{n}p_i log_2{p_i}$$<br>
信息增益公式：$$Gain(D,a)=Ent(D)-Ent(d|a)=Ent(D)-\sum_{v=1}^V \frac{D_v}{D}Ent(D_v)$$

#### 问题描述

如下图，第一列为论坛号码，第二列为性别，第三列为活跃度，最后一列用户是否流失。
{% include aligner.html images="blog-img/machinelearning/1.png" %}

根据该图整理得到如下表格：

{% include aligner.html images="blog-img/machinelearning/2.png" %}

#### 整体熵为多少

{% include aligner.html images="blog-img/machinelearning/3.png" %}

##### 计算按照性别划分的信息增益

要计算性别的信息增益需要先计算性别的信息熵
{% include aligner.html images="blog-img/machinelearning/3.png" %}

因此得到按照性别划分的信息增益为
{% include aligner.html images="blog-img/machinelearning/4.png" %}

#### 计算按照活跃度划分的信息增益

同样的，要计算活跃度的信息增益需要先计算活跃度的信息熵

{% include aligner.html images="blog-img/machinelearning/5.png" %}

因此得到按照活跃度划分的信息增益为：

{% include aligner.html images="blog-img/machinelearning/6.png" %}

#### 比较两种特征对流失度的影响

活跃度的信息增益比性别的信息增益大，也就是说，活跃度对用户流失的影响比性别大。

#### 做出决策树图形并说明理由

根据第三问的分析，活跃度的信息增益比性别的信息增益大所以要选用，活跃度作为决策树的根节点。最终结果如下所示：

{% include aligner.html images="blog-img/machinelearning/7.png" %}

---

## 问题八：逻辑回归的优化目标函数是什么？交叉熵中的两个概率是分布什么？(不确定)

逻辑回归的优化目标函数是:对数似然函数。 <br>
交叉熵的灵感概率是：真实分布，非真实分布。

## 问题九：简述k近邻的算法流程，以及问题问题分析
### 算法流程
1. **计算距离**：计算已知类别数据集中的点与当前点之间的距离
2）**排序**：按距离递增次序排序
3）**选择**：选取与当前点距离最小的k个点
4）**计算频次**：统计前k个点所在的类别出现的频率
5）**确定类别**：返回前k个点出现频率最高的类别作为当前点的预测分类

### 计算题（以ppt为例）
#### 考察公式
欧氏距离：平方和开根号 <br>
曼哈顿距离（城市街区距离）：绝对值的和


### 提问
假设我们现在有几部电影，如何去预测序号9电影的类别？
{% include aligner.html images="blog-img/machinelearning/8.png" %}

分别计算每个电影和被预测电影的距离，然后求解
{% include aligner.html images="blog-img/machinelearning/9.png" %}

所以最终结果预测为喜剧片。

---

## 问题十：标准化与归一化问题（以PPT为例）
#### 归一化（重点）

**归一化定义**：通过对原始数据进行变换把数据映射到(默认为[0,1])之间
{% include aligner.html images="blog-img/machinelearning/10.png" %}

作用于每一列，max为一列的最大值，min为一列的最小值，那么X’’为最终结果，mx，mi分别为指定区间值，默认mx为1，mi为0

{% include aligner.html images="blog-img/machinelearning/11.png" %}

#### 标准化

定义：通过对原始数据进行变换把数据变换到均值为0,标准差为1范围内
{% include aligner.html images="blog-img/machinelearning/12.png" %}

其中，它作用于每一列，mean为平均值，σ为标准差

---

## 问题十一：k均值（k-means）聚类的算法
#### 流程
1. 随机设置K个特征空间内的点作为初始的聚类中心
2. 对于其他每个点计算到K个中心的距离，未知的点选择最近的一个聚类中心点作为标记类别
3. 接着对着标记的聚类中心之后，重新计算出每个聚类的新中心点（平均值）
4. 如果计算得出的新中心点与原中心点一样（质心不再移动），那么结束，否则重新进行第二步过程

#### 目标函数及其描述：
？？？

---

## 问题十二：梯度下降法
#### 梯度下降算法的作用：

梯度下降法是一个优化算法，可以递归地找到模型的最小值，从而找到在最优参数。

#### 需要处理的问题：

1. 学习率：需要在模型建立的速度和质量上做出权衡，学习率过大可能会导致最终结果不收敛，学习率过小会导致训练时间过长。
2. 方向：计算出当前点的梯度方向，并向下不断更新自己的位置。
3. 终止条件：考虑使用迭代次数、损失函数值到达一定范围之后终止。

---

## 问题十三：逻辑回归（不确定）
#### 损失函数：
{% include aligner.html images="blog-img/machinelearning/13.png" %}

#### 目标函数
{% include aligner.html images="blog-img/machinelearning/14.png" %}

#### 定义：
逻辑回归是机器学习中的一种分类模型，做二分类（1/0）任务，并给出相应概率。
#### sigmoid函数
sigmoid可以将数值压缩到[0,1]的范围内。

---

## 问题十四：编程大题
#### 线性回归（以实验为例）

|序号|直径（英寸）|价格（ 美元）|
|-   |-           |-            |
|1|	6|	7|
|2|	8|	9|
|3|	10|	13|
|4|	14|17.5|
|5|	18|	18|

##### 该线性回归是一个几元函数，表达式是什么？
是一个一元线性回归函数。<br>
表达式为：$$f(x) = w_1x_1 + b$$<br>
其中$$w_1$$表示的是“直径”特征的权重，$$x_1$$表示“直径”变量，$$b$$表示截距

##### 代码实现
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression   # 最小二乘法线性回归
from sklearn.model_selection import train_test_split
import matplotlib.pyplot as plt

X_train_old = np.array([6,8,10,14,18]).reshape(5,1)
Y_train_old = np.array([7,9,13,17.5,18]).reshape(5,1)
X_train_old,Y_train_old

# 因为数据较少所以没必要再单独划出测试集了
X_train,X_test,Y_train,Y_test = train_test_split(X_train_old,Y_train_old,random_state=33,test_size=0.2)
# X_train,X_test,Y_train,Y_test = X_train_old,[],Y_train_old,[]
X_train,X_test,Y_train,Y_test

model = LinearRegression()
model.fit(X_train,Y_train)

T_sim1 = model.predict(X_test)

```
##### 逻辑回归（以实验为例）
代码实现：
```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

# 1.获取数据
names = ['Sample code number', 'Clump Thickness', 'Uniformity of Cell Size', 'Uniformity of Cell Shape',
                   'Marginal Adhesion', 'Single Epithelial Cell Size', 'Bare Nuclei', 'Bland Chromatin',
                   'Normal Nucleoli', 'Mitoses', 'Class']
data = pd.read_csv(r"breast-cancer-wisconsin.data",names=names)
data.head()

x_train, x_test, y_train, y_test = train_test_split(x, y, random_state=22)
x_train.head()

estimator = LogisticRegression()
estimator.fit(x_train, y_train)

y_predict = estimator.predict(x_test)
```
## 问题十五：随机森林
#### 随机森林的算法流程（随机森林=Bagging+决策树）

1. 随机选取m条数据
2. 随机选取k个特征
3. 训练决策树
4. 重复1-3
5. 对上面的若决策树进行平权投票

#### bagging和boosting的区别

##### 区别一:数据方面
1. Bagging：对数据进行采样训练；
2. Boosting：根据前一轮学习结果调整数据的重要性。


##### 区别二:投票方面
1. Bagging：所有学习器平权投票；
2. Boosting：对学习器进行加权投票。

##### 区别三:学习顺序
1. Bagging的学习是并行的，每个学习器没有依赖关系；
2. Boosting学习是串行，学习有先后顺序。

##### 区别四:主要作用
1. Bagging主要用于提高泛化性能（解决过拟合，也可以说降低方差）
2. Boosting主要用于提高训练精度 （解决欠拟合，也可以说降低偏差）