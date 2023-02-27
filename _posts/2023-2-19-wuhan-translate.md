---
layout: post
title: 基于svm实现的屏幕翻译项目解析
author: Ranok
tag: [人工智能,计算机视觉,python,机器学习,爬虫]
permalink: tranlate     # 网页的路径
feature-img: assets/img/feature-img/translate.jpg # 这是一个会出现在博客文章内部的图片
thumbnail: assets/img/thumbnails/feature-img/translate.jpg # 文件路径在github还是只支持正斜杠'/'
---
<a id="go_to_top"></a>
&emsp;&emsp;不知不觉间，人工智能慢慢开始走进千家万户。无人驾驶、AI绘图、语音识别、AI聊天都是人工智能的领域。我作为一个智能的学生已经被迷得不行了，在这份热爱的支持下我完成了这份项目。虽然我的项目与当今智能技术无法比拟，但是其中运用到的机器学习模型（如`SVM`分类器）足以能够让我的项目归类到人工智能。

---
# 目录
- [目录](#目录)
- [前言](#前言)
- [项目总目标](#项目总目标)
- [正文](#正文)
  - [数据收集与数据清洗](#数据收集与数据清洗)
    - [为什么要收集数据？](#为什么要收集数据)
    - [数据收集](#数据收集)
    - [数据规范化](#数据规范化)
  - [建模与机器学习（SVM）](#建模与机器学习svm)
    - [对建模的理解与机器学习的理解](#对建模的理解与机器学习的理解)
    - [建模](#建模)
      - [1.随机划分训练集与测试集](#1随机划分训练集与测试集)
      - [2.参数调优](#2参数调优)
      - [3.训练](#3训练)
      - [4.模型检验](#4模型检验)
      - [5.模型保存](#5模型保存)
    - [数据处理](#数据处理)

---

# 前言
&emsp;&emsp;此项目专用于204技术交流会使用，未经本人允许不得外传。为了更好地展示项目，所以在这里写下这篇博客。本博客面向新人，我尽可能的使用了最朴素的方式来表达我的项目技术流程以及算法思想，且文章中不会出现大量生僻难懂的术语，请放心食用。另外，此静态博客网基于[Jekyll](http://jekyllrb.com/)框架搭建，但对`Jekyll`的讨论并不在此次技术交流之列中。如果你对`Jekyll`感兴趣，随时欢迎与我讨论❤️。

&emsp;&emsp;本项目设计以及编码历时共7天，共计划分8个模块，项目大致可以划出以下几个技术分支：
- 基于opencv实现的数据清洗与预处理
- 基于svm机器学习分类器识别字母
- 基于selenium无头浏览器实现的翻译爬虫
- 使用threading线程池优化

---

> 温馨提示：如果你觉得界面配色有些刺眼，你可以点击右上角的菜单，选择使用**圆形**按钮切换主题背景。


# 项目总目标

&emsp;&emsp;实现一个可以实时读取屏幕信息，并翻译图中英文的屏幕翻译器。

&emsp;&emsp;效果展示如下图，左右分别为翻译前后的对比：

{% include aligner.html images="blog-img/translate/2.jpg,blog-img/translate/1.jpg" column=3 %}

&emsp;&emsp;项目主要的技术点以及流程如下所示

{% include aligner.html images="blog-img/translate/9.png" column=3 %}

---
# 正文

---

## 数据收集与数据清洗
---

### 为什么要收集数据？

&emsp;&emsp;要翻译屏幕中的英文，首先要做的应该是识别出屏幕中的英文。识别的工作是交由机器学习模型实现的，但是模型并不是一开始就拥有识别英文的能力。事实上你可以将`python`所提供机器学习模型视为空壳，只有通过不断的喂养其数据，主观的告诉模型什么是对的什么是错的，在不断的训练学习之后模型才有识别的能力。机器学习因此得名“机器学习”。

&emsp;&emsp;什么？你问我为什么不直接去网上下载一个模型？<br>
&emsp;&emsp;那肯定是~~（没找到）~~想要锻炼💪自己呀！

&emsp;&emsp;一般的，一个模型的好坏主要最关键的因素是数据的优劣。数据越多越纯净就越容易训练出优秀的模型。因此数据整理的部分显的尤为重要。

---
### 数据收集

&emsp;&emsp;模型需要识别的是屏幕中的英文，所以收集的数据也应该是印刷体的的字母图片。不过这类数据资源在网上很少能找得到，少数在[Gethub](https://www.php.cn/tool/git/413611.html)和[Kaggle](https://cloud.tencent.com/developer/news/68329)上找到的资源所训练出的模型效果都不尽人意。

&emsp;&emsp;最终还是决定，自己动手创造数据。<br>
&emsp;&emsp;首先准备好自制的52个大小写英文字母一份。
{% include aligner.html images="blog-img/translate/3.jpg" column=3 %}

&emsp;&emsp;每个字母只有一张图片用以供应模型的训练肯定是不够用的，所以应该对数据进行扩充，保证至少每个字母对应能有20张匹配的图片。这里使用到的技术是图片的**下采样**以做到图片的扩充，简单的理解就是通过对一张图片采用随机的不同程度的模糊化处理从而到多张图片。

&emsp;&emsp;其中对字母A的采样结果示意图如下：

{% include aligner.html images="blog-img/translate/4.jpg" column=3 %}

&emsp;&emsp;你问我为什么不多造几个数据，而是使用下采样扩充？<br>
&emsp;&emsp;~~（肝不够多）~~下采样得到的图片是对原有图片的衍生，同样拥有原图像的基本信息，用这样的数据进行训练不会影响模型的效果。


### 数据规范化

&emsp;&emsp;图像数据需要最终供模型训练，而训练的接口是固定的，因此所有的数据应该有相同的规格。

&emsp;&emsp;我的做法是将数据处理成 $$ 20*20 $$ 像素的黑白图片素材使用。

&emsp;&emsp;也就是将一个普通的字母图片通过横向纵向的拉伸与压缩变成一个 $$ 20*20 $$ 标准的图片。显而易见的，这种做法很容易导致图片信息了流失。我在实践中也遇到了这个问题，其中影响最大的就是字母 $$ il $$ 等长宽比差距较大的字母，如果直接通过拉伸与放缩的手段让其规范化的话就会出现以下的结果（左边为原图，右边为处理后的图像）以至于影响到后面建模的效果:

{% include aligner.html images="blog-img/translate/5.jpg,blog-img\translate\6.jpg" column=10 %}

&emsp;&emsp;对此我的做法是显式地判断图片的长宽比，当长宽比超过4时，手动放缩，具体代码如下：

```python
    def resize(self, img):
        """
        图像需要原先就是灰度图像
        将图片调整到标准大小20*20
        :param img: 原图像
        :return:finish_img
        """

        if img.shape[0] / img.shape[1] > 4:  # 表示长宽比太大了，不适合做拉伸操作
            ## 待补充，这里需要解决过度拉伸的问题，可能需要寻找填充的方法
            # 计算需要用于填充的图像的宽高
            high = img.shape[0]
            wide = int((img.shape[0] - img.shape[1]) / 2)

            grid = np.zeros((high, wide))  # 计算用于填充的黑色图片

            img = np.hstack((grid, img))  # 左右都做填充
            img = np.hstack((img, grid))  # 左右都做填充

            # 最后将填充的图像重新转换为20*20的格式
            img = cv2.resize(img, (20, 20))
            if self.debug:
                print("这里做了一次对称填充")
        else:
            img = cv2.resize(img, (20, 20))
        # 调整大小并返回
        return img
```
---

## 建模与机器学习（SVM）

### 对建模的理解与机器学习的理解
&emsp;&emsp;在数据规范化后我们得到了，噪音（杂质）相对较少的 $$20 * 20$$的图片信息，但是我们的$$ SVM $$分类器模型（下面以“$$SVM$$”简称）还不能直接使用这些数据，$$SVM$$所反映的是多个数值影响一个数值的**映射关系函数**，可以简单的概括成以下的函数，训练的最终目的就是为了得到这个函数：

$$ f(x) = w_1x_1 + w_2x_2 + w_3x_3 + \dots w_nx_n $$

> 其中 $$ x_i $$ 表示自变量，可以理解为对应图片像素点的数值，$$ w_i $$表示权值，$$f(x)$$是最终计算出来的结果。

&emsp;&emsp;将之前清洗好的图像，当成一个个$$ n $$组400维的方程组，使用$$ SVM $$ 算法“解方程”。

> 400维由来：一个20*20的图片有400个像素点

&emsp;&emsp;上面最终计算得到上面的式子，也就是我们所说的一个训练好的模型。

---
### 建模
&emsp;&emsp;数据建模，在这里不是指3D建模，而是指一个**机器学习**的流程。这里数据建模用到了机器学习是本项目可以称之为**人工智能**的原因之一。<be>接下来将简单讲解机器学习的流程。

#### 1.随机划分训练集与测试集

&emsp;&emsp;将整理好的数据，按照一定比例划分成训练集与测试集，训练集的数据顾名思义是用于训练数据的，测试集的数据是用来检验模型的正确率的。

> 训练集的数据就好比那些的有答案的课本，我们拿他学习提升自己的能力，而测试集则更像是试卷，用来检测我们的学习成果。

#### 2.参数调优

&emsp;&emsp; 一个模型往往有很多的参数需要我们定义，这些参数在不同的情况下需要取不同的数值才能使模型达到最优的效果。不同于平时的算法竞赛题目，这些参数值往往不是确定的，需要我们自己去调整。当然，我们不需要自己手动调参，我们可以用[网格搜索](https://blog.csdn.net/guoyc439/article/details/123381908)与[k折交叉验证](https://blog.csdn.net/qq_36535820/article/details/119762665)两种方法来解决最优参数的寻找问题。

&emsp;&emsp;这两种算法的主要做法是，将训练集的数据继续分出一个和验证集，通过不断测试与调整，最终计算出最优模型的参数。由于篇幅有限，其具体做法这里不做过多的描述。

#### 3.训练

&emsp;&emsp;模型训练的操作，其实才是机器学习里面最难的部分，不过好在SVM已经被python封装好了，我们只需要提供前面清洗出的数据以及定义[参数调优](#2参数调优)，稍等片刻即可得到训练好的模型。

#### 4.模型检验

&emsp;&emsp;将之前分出的测试集数据代入模型进行预测，计算正确率。当然评价一个模型的好坏的指标有很多其他的评价指标还有$$ R^2 $$，召回率等等，这里不做延伸。

#### 5.模型保存

&emsp;&emsp;每次训练一个模型经常要消耗大量的时间，为此我们需要保存训练好的模型，在下次做识别时就不需要再训练了。

&emsp;&emsp;上面对机器学习的建模过程的描述地十分简单，但是实际的建模过程远比这个要复杂。只要前面在的“数据分析”“数据选择与清洗”“模型选择”“参数设置”等等环节出现了一个错误都有可能把你的人工智能模型训练成“人工智障”，而且前面的繁多步骤也会加大调参排错的难度。我也是花了4天左右的时间才训练出了一个比较过得去的模型。

> ⚡如果你也想入门人工智能，那要求你至少要有比较强的python基础，成熟的面向对象的思维，以及强大的心理素质。⚡

&emsp;&emsp;以下是py代码实现
```python
    def train(self):
        """
        SVM模型实现
        :return: None
        """
        ## 数据分析与预处理
        x_train, y_train, x_test, y_test = self.get_data()

        ## 网格搜索,找到最优参数
        machine_svm = svm.SVC()

        param_grid = {'C': range(0, 50, 10)}  # 这里设置了参数的测试范围
        grid_search = GridSearchCV(machine_svm, param_grid, cv=3)  # 建立网格搜索器模型
        grid_search.fit(x_train, y_train)  # 开始搜索

        ## 创建分类器对象
        print("最优参数是 c= ", grid_search.best_params_)
        print("最优模型正确率 = ", grid_search.best_score_)
        self.machine_svm = grid_search.best_estimator_  # 获取最优模型

        ## 模型训练
        self.machine_svm.fit(x_train, y_train)

        ## 模型验证
        result = self.machine_svm.predict(x_test)
        correct = np.count_nonzero(result == y_test)
        accuracy = correct / result.size

        print("测试集正确率：", accuracy)

        ## 模型保存
        joblib.dump(self.machine_svm, 'model/svm.pkl')

```


---

### 数据处理

&emsp;&emsp;在前面，我们用做了特殊处理的图片对模型进行训练，所以在用该模型进行识别操作时，也需要对被识别图像做同样的操作。在之前清洗数据时我并没有详细讲解具体的操作，所以放到这里详细说明。

&emsp;&emsp;我们想要预测一个图像，显然无法直接对一个RGB格式的图片下手，对于一个RGB格式的图片，它的每一个像素点都由三个数值组成（Rad Green Blue），这不利于识别，所以需要处理成一个数值，这样的处理过程我们称之为**灰度化**。

&emsp;&emsp;如下方的两个图像就是做了灰度化处理的图像对比。


{% include aligner.html images="blog-img/translate/7.jpg,blog-img\translate\8.jpg" column=10 %}

&emsp;&emsp;为了更好的配对模型，我们需要对灰度图进一步简化，通常的做法是将像素点间的差距拉的尽可能大（离散化），我们通常使用的方式是**二值化**

&emsp;&emsp;如下方的两个图像是灰度图像做了二值化处理的前后对比。

{% include aligner.html images="blog-img\translate\8.jpg,blog-img/translate/10.jpg" column=10 %}

&emsp;&emsp;二值化后的图像，为过滤或弱化出图形中的小白点（噪音），我们常常采用高斯模糊（打马赛克）以及腐蚀的方法。

&emsp;&emsp;如下图分别为做了高斯模糊和腐蚀操作的二值图像。

{% include aligner.html images="blog-img\translate\11.jpg,blog-img\translate\12.jpg" column=10 %}

&emsp;&emsp;有时，我们会把握不好腐蚀操作的度，以至于一些重要信息也被过滤掉了，为了弥补过滤掉的内容，一般会对腐蚀后的图像做**膨胀**操作。<br>
一般的，先对一个图像做腐蚀再对齐做膨胀的组合操作我们称之为**开运算**。

&emsp;&emsp;如下为两个分别是做了碰撞和开运算的图像。

{% include aligner.html images="blog-img\translate\13.jpg,blog-img\translate\14.jpg" column=10 %}

&emsp;&emsp;通过`opencv`库实现以上操作，可以帮助我们从一张图片中提取出很多有效的信息。你可以从下面的代码中直观得体会出这个处理流程。

```python
    def change_color(self, img):
        """
        将图像进行预处理
        :param img:img 彩图
        :return: img 二值图
        """
        ## 原图像备份
        copy_img = img.copy()
        self.show(copy_img)

        ## 高斯模糊
        copy_img = cv2.GaussianBlur(img, (3, 3), 0)

        ## 图像灰度化
        copy_img = cv2.cvtColor(copy_img, cv2.COLOR_BGR2GRAY)
        self.show(copy_img)

        ## 图像二值化
        _, copy_img = cv2.threshold(copy_img, 115, 255, cv2.THRESH_BINARY_INV)
        self.show(copy_img)

        ## 开运算降噪
        copy_img = cv2.morphologyEx(copy_img, cv2.MORPH_OPEN, np.ones((2, 2)), iterations=2)
        self.show(copy_img)

        ## 膨胀运算
        copy_img = cv2.morphologyEx(copy_img, cv2.MORPH_DILATE, np.ones((5, 5)), iterations=4)
        self.show(copy_img)

        return copy_img
```


---
[回到顶部](#go_to_top)