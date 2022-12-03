---
layout: post
title: 博客测试
tags: [Test, Image]     #标签会影响
feature-img: "assets/img/feature-img/circuit.jpeg" # 这是一个会出现在博客文章内部的图片
thumbnail: "assets/img/thumbnails/feature-img/circuit.jpeg" # 这是一个会出现在博客外部的图片
color: brown # 会影响界面部分元素的颜色，如果界面没有自定义图片的话就会给一个对应颜色的图片

---

这里写需要展示在外部的内容，且需要与正文隔一个空行

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
---

[百度一下](https://www.baidu.com) 超链接需要是http格式的

这是一个公式 $$ a^2+b^2 > 2ab $$

这是一个`行内代码`块

在写代码的时候可以用指定语言的方式来表现出不同的高亮，代码块之间需要有一个空行
```python
def showw():
    print("这是一个python代码块")
```

```c++
void show(){
    cout<<"这是一个C++代码块";
}
```

*斜体文字*

_斜体文字_

**粗体文字**

__粗体文字__

***粗斜体文字***

___粗斜体文字___


***
* * *
******
- - -
------

~~删除线~~

<u>下划线</u>

> 警告内容

表格是制作方式类似于latex

| hex | dec | oct |
| -   | -   | -   |
| 0   | 0   | 0   |
| 5   | 5   | 5   |
| A   | 10  | 12  |
| F   | 16  | 20  |
| F5  | 21  | 25  |

导入图片,图片的主路径在assets/img处 斜杠需要使用正斜杠‘/’
{% include aligner.html images="blog-img/wolf-test.jpg" %}

导入多张图片，只需要在图片导入的位置用，分隔即可
{% include aligner.html images="pexels/book-glass.jpeg,feature-img/desk-messy.jpeg" %}