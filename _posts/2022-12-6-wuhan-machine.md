---
layout: post
title: 机器学习三大基础库
author: Ranok
color: brown
tag: [机器学习,python,numpy,pandas,matplotlib]
thumbnail: "assets/img/thumbnails/feature-img/machine.jpeg"
permalink: machine
---

机器学习是研究怎样使用计算机模拟或实现人类学习活动的科学，是人工智能中最具智能特征，最前沿的研究领域之一。自20世纪80年代以来，机器学习作为实现人工智能的途径，在人工智能界引起了广泛的兴趣，特别是近十几年来，机器学习领域的研究工作发展很快，它已成为人工智能的重要课题之一。机器学习不仅在基于知识的系统中得到应用，而且在自然语言理解、非单调推理、机器视觉、模式识别等许多领域也得到了广泛应用。一个系统是否具有学习能力已成为是否具有“智能”的一个标志。

---

## 前言

本次博客主要内容为以下三个python库
* numpy
* pandas
* matplotlib

前两个库`numpy`、`pandas`主要作用是对于数据存储与数据处理，并且广泛适用于很多机器学习的模型。而`matplotlib`是作图的好帮手，主要用户机器模型数据的可视化。

## numpy（机器学习前缀知识）
#### 属性
1.	数组的维数：对象名.ndim
2.	数组的每个维度的数量：对象名.shape返回一个元组，元组中的数字表示该维度的长度。
3.	元素总个数：对象名.size
4.	成员的数据类型：对象名.dtype
5.	矩阵的转置：对象名.T
6.	对象名.flat 表示返回一个可以遍历所有元素的迭代器
7.	numpy.nan 表示无穷
8.	xxx

#### 功能型小函数

1.	numpy.sum 求和
2.	numpy.min 求最小值
3.	numpy.max 求最大值
4.	numpy.average 求平均值
5.	numpy.median 求中位数
6.	numpy.cumsum 返回前缀和向量
7.	numpy.diff 返回一个差分数组（少一位）
8.	numpy.argmin 求最小值的索引（从0开始计算）
9.	numpy.argmax 求最大值的索引（从0开始计算）
10.	numpy.nonzero返回n个向量，表示非元素所在位置的索引。
11.	numpy.sort 返回对数组排序的结果，如果是多维则只会对一维排序（每一行）。
12.	numpy.transpose 返回矩阵转置的结果
13.	对象名.flatten() 返回该对象的一维展开（即变成一个行向量）
14.	对象名.copy() 返回该对象的值拷贝（直接使用“=”是引用拷贝）注意不同于列表使用对象名[:]不能实现值拷贝，必须使用copy函数
15.	numpy.random.randn 按正太分布的概率产生随机数数组
16.	numpy.all(逻辑表达式) 逻辑表达式后半段 通过用这种方式将矩阵中所有数据参与计算返回一个bool判断矩阵中是不是所有元素都满足这个式子。
17.	numpy.any(数组对象)逻辑表达式后半段 通过用这种方式将矩阵中所有数据参与计算返回一个bool判断矩阵中是否存在某个元素满足这个式子。

#### 示例（以numpy.sum为例）
函数的默认计算区域是所有元素，当想要指定维度使用时需要使用axis来指定，axis从<br>
0开始计数。特别的对于一个矩阵来说，axis=0表示对每一列求和，axis=1表示对每一行求和。
##### 代码示例：

```python
import numpy as np

a = np.arange(4).reshape(2,2)
print(a)
print(np.sum(a),np.sum(a,axis=1))
```
##### 程序运行截图：
```json
[[0 1]
 [2 3]]
6 [1 5]
```

#### 矩阵索引
以二维数组（矩阵）为例

##### 访问单元素的方法
`a[i][j]`，或 `a[i,j]`

##### 访问多元素的方法
访问第`i+1`行的所有元素<br>
`a[i,:]`<br>
访问第`j+1`列的所有元素<br>
`a[:,j]`

#### 矩阵初始化 array
函数签名：
```python
array(p_object, dtype=None, *args, **kwargs):
```
上面的构造器接受以下参数：
1.	object 任何暴露数组接口方法的对象都会返回一个数组或任何（嵌套）序列。
2.	dtype 数组的所需数据类型，可选。
3.	copy 可选，默认为true，对象是否被复制。
4.	order C（按行）、F（按列）或A（任意，默认）。
5.	subok 默认情况下，返回的数组被强制为基类数组。 如果为true，则返回子类。
6.	ndmin 指定返回数组的最小维数。

示例：
```python
array = numpy.array([[1,2,3],[4,5,6]].numpy.int64)
```
#### 滤波器clip

##### 函数签名：
```py
def clip(a, a_min, a_max, out=None, **kwargs):
```
将数组中小于a_min的值取a_min，将数组中大于a_max的值取a_max<br>
代码示例：
```py
import numpy as np

a = np.arange(12)

print(np.clip(a,5,9))
```
程序运行截图：
`[5 5 5 5 5 5 6 7 8 9 9 9]`

#### 创建一个全1数组ones
函数签名：
```py
def ones(shape, dtype=None, order='C', *, like=None):
```
示例：
```py
numpy.noes((2,3,4)) # 创建一个2叶3行4列的全1矩阵
```

#### 创建一个全0数组zeros
函数签名：
```py
def zeros(shape, dtype=None, order='C', *args, **kwargs):
```

示例：
```py
numpy.zeros((2,3,4)) # 创建一个2叶3行4列的全0矩阵。
```

#### 创建有序数组arange
函数签名：
```py
def arange(start=None, *args, **kwargs):
```
##### 示例1（创建一个0~9的行向量）：
```py
numpy.arange(10)
```
程序输出：`[0 1 2 3 4 5 6 7 8 9]`

##### 示例2（创建一个5~9的行向量）：
```py
numpy.arenge(5,10)
```
程序输出：`[5 6 7 8 9]`

##### 示例3（创建一个以3为步长1~10的行向量）
```py
numpy.arange(1,11,3)
```
程序输出：`[ 1  4  7  10]`

##### 示例4（创建一个0~9的2行5列的矩阵）
```py
numpy.arange(10).reshape(2,5) # 规模必须与元素个数相匹配
```
程序输出：
```json
[[0 1 2 3 4]
 [5 6 7 8 9]]
```

#### 创建一个均匀划分的线段 linspace
函数签名：
```py
def linspace(start, stop, num=50, endpoint=True, retstep=False,type=None,axis=0):
```
作用：以start为开始以stop结束以num为划分次数创建一个行向量。

##### 示例1（一般示例）：
```py
numpy.linspace(0，10，2)
```
程序输出：
`[ 0. 10.]`

##### 示例2（重组元素为一个2*5的矩阵）
```py
numpy.linspace(0,10,10).reshape(2,5)
```
程序输出：
```json 
[[ 0.          1.11111111  2.22222222  3.33333333  4.44444444]
 [ 5.55555556  6.66666667  7.77777778  8.88888889 10.        ]]
```

#### numpy的运算
##### 矩阵加减法：
代码示例：
```py
a = np.array([10,20,30,40])
b = np.arange(1,5)
print(a-b)
print(a+b)
```
程序运行截图：
```json
[ 9 18 27 36]
[11 22 33 44]
```

##### 矩阵点乘：
###### 代码示例1（矩阵点乘）：
```py
import numpy as np

a = np.array([10,20,30,40])
b = np.arange(1,5)
print(a*b)
```
程序运行截图：`[ 10  40  90 160]`

###### 代码示例2（矩阵乘数字）：
```py
import numpy as np

a = np.array([10,20,30,40])

print(a*5)
```
程序运行截图：`[ 50 100 150 200]`

##### 矩阵乘法：
###### 示例1（使用np.dot函数实现矩阵乘法）
代码示例：
```py
import numpy as np

a = np.arange(1,4).reshape(1,3)
b = np.arange(1,4).reshape(3,1)

c_dot = np.dot(a,b)
d_dot = np.dot(b,a)
print(c_dot,d_dot,sep='\n')
```
程序运行截图：
```json
[[14]]
[[1 2 3]
 [2 4 6] 
 [3 6 9]]
```
###### 示例二（使用@符号实现矩阵乘法）：

代码示例：
```py
import numpy as np

a = np.arange(1,4).reshape(1,3)
b = np.arange(1,4).reshape(3,1)

print(a@b,b@a,sep='\n')
```
程序运行截图：
```json
[[14]]
[[1 2 3]
 [2 4 6]
 [3 6 9]]
```
##### 数组的逻辑判断：

数组可以直接进行逻辑判断，其返回值为与元素组同规模的bool型结果数组。
可以使用对象[逻辑表达式] 来过滤符合条件的项，返回一个行向量。

代码示例：
```py
import numpy as np

a = np.arange(10)
print(a < 3)
s = np.random.random((4,4))
print(s[s > 0.5])
```
程序运行截图：
```py
[ True  True  True False False False False False False False]
[0.50784044 0.51138057 0.75612031 0.61457462 0.9712732  0.79497591]
```
##### 矩阵元素的函数运算：
代码示例：
```py
import numpy as np

a = np.arange(10)
print(np.sin(a))
```
程序运行截图：
```py
[ 0.          0.84147098  0.90929743  0.14112001 -0.7568025  -0.95892427
 -0.2794155   0.6569866   0.98935825  0.41211849]
```

##### 创建一个元素值在0~1之间的随机矩阵
###### 示例（创建一个元素值在0~1之间的2行4列的随机矩阵）：
代码示例：
```py
import numpy as np

a = np.random.random((2,4))

print(a)
```
程序运行截图：
```json
[[0.24853676 0.47803948 0.04436044 0.92552742]
 [0.61756337 0.31913713 0.83677922 0.51923448]]
```

#### 合并数组
##### 上下合并函数签名：
```py
def vstack(tup):
```
##### 左右合并函数签名：
```py
def hstack(tup):
```
代码演示：
```py
import numpy as np

a = np.array([1,2,3,4])
b = np.array([4,3,5,8])
print(np.vstack((a,b)))
print(np.hstack((a,b)))
```
程序运行截图：
```json
[[1 2 3 4]
 [4 3 5 8]]
[1 2 3 4 4 3 5 8]
```
#### 数组分割 split or array_split
##### 等量数组分割 split

函数签名：
```py
def split(ary, indices_or_sections, axis=0):
```
注意：axis表示对照切割的维度，例如对于矩阵而言axis=0表示横向切割，axis=1表示纵向切割，切割必须是对等切割否则报错。<br>
代码展示：
```py
import numpy as np

A = np.arange(12).reshape(3,4)
print(A)
print("纵向切割")
print(np.split(A,2,axis=1))
print("横向切割")
print(np.split(A,3,axis=0))
```
程序运行截图：
{% include aligner.html images="blog-img/machine/1.png" %}

##### 不等量数组分割 array_split
函数签名：
```py
def array_split(ary, indices_or_sections, axis=0):
```
注意：这里与函数split最大的区别就是可以实现不等分的分法。前面等分，后面几项少分。<br>
代码展示：
```py
import numpy as np

A = np.arange(12).reshape(3,4)

print(A)
print("纵向切割")
print(np.array_split(A,3,axis=1))
print("横向切割")
print(np.array_split(A,2,axis=0))
```
程序运行截图：

{% include aligner.html images="blog-img/machine/2.png" %}

## pandas（机器学习前缀知识）
#### 属性
1.	dtypes 获取所有列的数据格式
2.	columns 获取所有列名
3.	values 去除行名和列名，返回所有的内容，返回对象是numpy.ndarry。
4.	T 获得矩阵的转置（列名和行名也会一起转）。
##### 功能型小函数
1.	fillna(x) 将序列中出现的nan转变为x
2.	isnull返回一个bool矩阵当原矩阵中该数值为nan时为true，非nan数据时为false。可以与numpy.any，numpy.all配套使用。
3.	读取csv文件pd.read_csv(文件名)

#### 初始化矩阵
##### 创建矩阵 Series
创建方式类似于numpy<br>
代码展示：
```py
import pandas as pd

s = pd.Series([1,3,6,44,1])
print(s)
```
程序运行截图：

{% include aligner.html images="blog-img/machine/3.png" %}

定义有名称的数据 DataFrame<br>
说明：<br>
index表示行标题，columns表示列标题，默认名称为从0开始的有序数列<br>
注意：每一行对应的数据数量要保持一致。<br>
##### 示例1（使用序列创建）
代码展示：
```py
import pandas as pd
mport numpy as np
s = 
d.DataFrame(np.random.randn(3,4),index=['x','y','x'],columns=['a','b','c','d'])
print(s)
```
程序运行截图:

{% include aligner.html images="blog-img/machine/4.png" %}

##### 示例2（使用字典创建）
代码展示：
```py
import pandas as pd

s = pd.DataFrame({
    "a": [1,3],
    "b": [1.2,4],
    "c": [1.5,84],
    "d": [0.2,6]
})
print(s)
```
程序运行截图：

{% include aligner.html images="blog-img/machine/5.png" %}

#### 数组访问
##### loc （名称）表示法
说明：
```js
loc[ [行名序列]，[列名序列] ]直接访问
loc[ 行名序列i：行名序列j，列名序列i：列名序列j ]切片访问（切片是闭区间）
```
两者可以混合使用。

代码展示：
```py
import pandas as pd
import numpy as np

dates = pd.date_range('20221001', periods=6)
s = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=['a', 'b', 'c', 'd'])

print(s)
print('单个数据访问',s.loc["20221002",'a'],sep='\n')
print('多行单列',s.loc[['20221002','20221001'],'b'],sep='\n')
print('单行多列',s.loc['20221002',[1,2]],sep='\n')
print('多行多列',s.loc[['20221002','20221001'],['a','b']],sep='\n')
print('多行多列切片访问',s.loc['20221001':'20221002',['a','b']],sep='\n')
```
程序运行截图：

{% include aligner.html images="blog-img/machine/6.png"%}

##### iloc（下标）表示法
说明：<br>
使用方式等同于loc但是序列名变成了索引号（从0开始计数）（不同于loc的是使用切片表示法时是左开右闭区间）<br>
代码展示：
```py
import pandas as pd
import numpy as np

dates = pd.date_range('20221001', periods=6)
s = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=['a', 'b', 'c', 'd'])

print(s)
print('单个数据访问',s.iloc[1,1],sep='\n')
print('多行单列',s.iloc[0:3,3],sep='\n')
print('单行多列',s.iloc[0,0:3],sep='\n')
print('多行多列',s.iloc[0:2,[0,3]],sep='\n')
```
程序运行截图：

{% include aligner.html images="blog-img/machine/7.png"%}

##### 访问一列
访问方式：<br>

对象名[列名]（适用于所有情况的访问方式）<br>
对象名.列名（这种访问方式仅适用于标题为字符串型的情况）

代码展示：
```py
import pandas as pd
import numpy as np
dates = pd.date_range('20221001', periods=6)
s = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=['a', 'b', 'c', 'd'])
print(s)
print(s['a'])
```
程序运行截图：
{% include aligner.html images="blog-img/machine/8.png"%}

##### 访问一行数据 loc
代码展示：
```py
import pandas as pd
import numpy as np

dates = pd.date_range('20221001', periods=6)
s = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=['a', 'b', 'c', 'd'])

print(s)
print(s.loc["20221002"])
```
程序运行截图：
{% include aligner.html images="blog-img/machine/9.png"%}

##### 访问多行数据

多行数据直接访问语法：<br>
`对象名[start:end]` 这里的start、end既可以是数字用于表示序列的索引，当行名不是整数型时也可以直接使用行名（行名可以是字符串）


#### 数组修改
说明：<br>
与赋值相似，对已存在的数值进行修改就是修改，对不存在的数据就是添加可以通过修改不存在的行列使得数据的行列增加（未知数据用NAN代替）<br>
代码展示：
```py
import pandas as pd
import numpy as np

dates = pd.date_range('20221001', periods=6)
s = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=['a', 'b', 'c', 'd'])
print(s)
print("修改数值")
s.a[s.a < 0] = 0
print(s)
print("增加行")
s.loc['new_index'] = np.nan
print(s)
print("增加列")
s.loc[:,"new_columns"] = np.array([0,1,2,3,4,5,6])
print(s)
print("同时增加行和列")
s.loc[8,'f'] = np.nan
print(s)
```
程序运行截图：
{% include aligner.html images="blog-img/machine/10.png"%}

#### 删除行列 dropna
说明：

`axis = 0` 时表示删除行，1表示删除列

`how`参数有两个值：

* “any”：如果存在任何NAN值，则删除该行或列。
* “all”：如果所有值都为NAN值，则删除该行或列。

注意：`dropna` 只是返回修改后的结果不会改变原本的值
代码展示：
```py
import pandas as pd
import numpy as np

dates = pd.date_range('20221001', periods=6)
s = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=['a', 'b', 'c', 'd'])

print(s)
s.iloc[0,0] = np.nan
s.iloc[2] = np.nan
s.iloc[:,3] = np.nan
print(s)
print("axis == 0 时表示删除行，1表示删除列")
s = s.dropna(axis=0,how='all')
print(s)
s = s.dropna(axis=1,how='all')
print(s)
s = s.dropna(axis=0,how='any')
print(s)
```
程序运行截图：
{% include aligner.html images="blog-img/machine/11.png"%}

#### 读写excle文件 read_excle or .to_excle
注意：<br>

`read_excle` 得到的是一个`pandas`对象，之前数据访问修改删除等操作依然成立。
`to_excle`创建时会添加一列行名，可以使用`index=False` 去除行名的添加。
#### 脚本编程
##### 逻辑表达式筛选：

使用对象名[逻辑表达式]方式筛选。
代码展示：
```py
import pandas as pd
import numpy as np

dates = pd.date_range('20221001', periods=6)
s = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=['a', 'b', 'c', 'd'])
print(s)
print('第0列数据大于0的数据有：')
print(s[s.iloc[:,0] > 0])
```
程序运行截图：
{% include aligner.html images="blog-img/machine/12.png"%}

#### 数据分析 describe
代码展示：
```py
import pandas as pd

s = pd.DataFrame({
    "a": [1,3],
    "b": [1.2,4],
    "c": [1.5,84],
    "d": [2,6.2]
})
print(s.describe(),sep='\n')
```
程序运行截图：
{% include aligner.html images="blog-img/machine/13.png"%}

#### 排序 sort_index & sort_values
##### sort_index 对行列名排序
说明：<br>
`axis = 0`表示对行名进行排序，1表示对列名进行排序。<br>
排序默认升序排序，当ascending = True 表示倒序排序<br>
函数签名：
```py
def sort_index(
    self,
    axis: Axis = 0,
    level: Level | None = None,
    ascending: bool | int | Sequence[bool | int] = True,
    inplace: bool = False,
    kind: str = "quicksort",
    na_position: str = "last",
    sort_remaining: bool = True,
    ignore_index: bool = False,
    key: IndexKeyFunc = None,
):
```
代码展示：
```py
import pandas as pd
s = pd.DataFrame({
    "a": [1, 3],
    "b": [1.2, 4],
    "c": [1.5, 84],
    "d": [2, 6.2]
})
print(s.sort_index(axis=0, ascending=False), sep='\n\n')
```
程序运行截图：
{% include aligner.html images="blog-img/machine/14.png"%}

##### sort_values对数据列排序
函数签名：
```py
def sort_values(  # type: ignore[override]
    self,
    by,
    axis: Axis = 0,
    ascending=True,
    inplace: bool = False,
    kind: str = "quicksort",
    na_position: str = "last",
    ignore_index: bool = False,
    key: ValueKeyFunc = None,
):
```
代码展示：
```py
import pandas as pd

s = pd.DataFrame({
    "a": [1, 3],
    "b": [1.2, 4],
    "c": [1.5, 84],
    "d": [2, 6.2]
})

print(s.sort_values('a',ascending=False))
```
程序运行截图：
{% include aligner.html images="blog-img/machine/15.png"%}

#### 合并数组 merge
说明：<br>
`how` 有4个取值：inner（默认）、outer、left、right 分别表示内连接、外连接、左外连接、右外连接。
`on` 表示连接是使用的列（类似于外键）
`indictor == True`时，在结果列中增加一列以显示每一个数据连接的方式默认为False，可以给indictor赋予字符串，以表示新列的名称
`left_	index & right_index`同时为True时可以按行名合并，默认都为False，两者必须同为True才能生效。
`suffixex`当给其一个包含两个字符串的元组时，合并时若出现同名字段，则会加上这两个字符串后缀。
函数签名：
```py
def merge(
    left: DataFrame | Series,
    right: DataFrame | Series,
    how: str = "inner",
    on: IndexLabel | None = None,
    left_on: IndexLabel | None = None,
    right_on: IndexLabel | None = None,
    left_index: bool = False,
    right_index: bool = False,
    sort: bool = False,
    suffixes: Suffixes = ("_x", "_y"),
    copy: bool = True,
    indicator: bool = False,
    validate: str | None = None,
) -> DataFrame:
```

##### 案例演示
###### 示例1（依照指定列进行合并）：
代码演示：
```py
import numpy as np
import pandas as pd

left = pd.DataFrame({
    'key': ['K0', 'k1', 'k2', 'k3'],
    'A': ['A0', 'A1', 'A2', 'A3'],
    'B': ['B0', 'B1', 'B2', 'B3']
})

right = pd.DataFrame({
    'key':['K0', 'k1', 'k2', 'k3'],
    'C':['C0','C1','C2','C2'],
    'D':['D0','D1','D2','D3']
})

print(left)
print(right)
res = pd.merge(left,right,on='key')
print(res)
```
程序运行截图：
{% include aligner.html images="blog-img/machine/16.png"%}

###### 示例2依照多列进行合并
代码演示：
```py
import numpy as np
import pandas as pd

left = pd.DataFrame({
    'key1': ['K0', 'k0', 'k1', 'k2'],
    'key2': ['K0', 'k1', 'k0', 'k1'],
    'A': ['A0', 'A1', 'A2', 'A3'],
    'B': ['B0', 'B1', 'B2', 'B3']
})

right = pd.DataFrame({
    'key1': ['K0', 'k1', 'k1', 'k2'],
    'key2': ['K0', 'k0', 'k0', 'k0'],
    'C': ['C0', 'C1', 'C2', 'C2'],
    'D': ['D0', 'D1', 'D2', 'D3']
})

print(left)
print(right)
# how = ['left','right','inner','outer']
print('内连接')
print(pd.merge(left, right, on=['key1','key2'],how='inner'))
print('全外连接')
print(pd.merge(left, right, on=['key1','key2'],how='outer'))
print('左外连接')
print(pd.merge(left, right, on=['key1','key2'],how='left'))
print('右外连接')
print(pd.merge(left, right, on=['key1','key2'],how='right'))
```
程序运行截图：

{% include aligner.html images="blog-img/machine/17.png"%}

###### 示例3（显示每一列的合并方式）
代码演示：
```py
import pandas as pd
df1 = pd.DataFrame({'col1':[0,1],'col_left':['a','b']})
df2 = pd.DataFrame({'col1':[1,2,2],'col_right':[2,2,2]})
print(df1)
print(df2)
res = pd.merge(df1,df2,on='col1',indicator=True,how='outer')
print(res)
```
程序运行截图：
{% include aligner.html images="blog-img/machine/18.png"%}

###### 示例4（依照行名进行合并）
代码演示：
```py
import pandas as pd
left = pd.DataFrame({
    'A':['A0','A1','A2'],
    'B':['B0','B1','B2']},
    index=['K0','K1','K2'])
right = pd.DataFrame({
    'C':['C0','C2','C3'],
    'D':['D0','D2','D3']},
    index=['K0','K2','K3'])
print(left)
print(right)
res = pd.merge(left,right,right_index=True,left_index=True,how='outer')
print(res)
```
程序运行截图：
{% include aligner.html images="blog-img/machine/19.png"%}

###### 示例5（同名字段加后缀）
代码演示：
```py
import pandas as pd
boys = pd.DataFrame({'k': ['K0', 'k1', 'k2'], 'age': [1, 2, 3]})
girls = pd.DataFrame({'k': ['K0', 'K1', 'K2'], 'age': [4, 5, 6]})
print(boys)
print(girls)
res = pd.merge(boys,girls,on='k',suffixes=('_boy','_girl'),how='outer')
print(res)
```
程序运行截图：
{% include aligner.html images="blog-img/machine/20.png"%}

#### 合并数组 concat
说明：<br>
`axis == 0`(默认) 表示竖向的合并，1表示横向合并<br>
`ignore == True`表示纵向合并时忽略原行序列从新有序定义行标号，默认False<br>
`join` 表示纵向连接方式默认为`outer`外连接（默认），还可以选择 `inner` 内连接<br>
注意：当竖向合并时，列名不一致（不包括次序不一致）将产生新列（全外连接）

##### 示例1 
代码展示：
```py
import pandas as pd
import numpy as np

df1 = pd.DataFrame(np.ones((3,4))*0,columns=['a','b','c','d'])
df2 = pd.DataFrame(np.ones((3,4))*1,columns=['a','b','c','d'])
df3 = pd.DataFrame(np.ones((3,4))*2,columns=['a','b','c','d'])

print(pd.concat([df1,df2,df3],axis=0,ignore_index=True))
```
程序运行截图：
{% include aligner.html images="blog-img/machine/21.png"%}

##### 示例2（纵向连接，两种连接的比较）
代码演示：
```py
import pandas as pd
import numpy as np

df1 = pd.DataFrame(np.ones((3,4))*0,index=[1,2,3],columns=['a','b','c','d'])
df2 = pd.DataFrame(np.ones((3,4))*1,index=[2,3,4],columns=['b','c','d','e'])

print(pd.concat([df1,df2],axis=0,join='outer'))
print(pd.concat([df1,df2],axis=0,join='inner'))
```
程序运行截图：
{% include aligner.html images="blog-img/machine/22.png"%}

##### 示例三（横向连接的4种方式比较）
注意：
代码演示：
```py
import pandas as pd
import numpy as np

df1 = pd.DataFrame(np.ones((3,4))*0,index=[1,2,3],columns=['a','b','c','d'])
df2 = pd.DataFrame(np.ones((3,4))*1,index=[2,3,4],columns=['b','c','d','e'])
print("全外连接")
print(pd.concat([df1,df2],axis=1))
print("左外链接")
print(pd.concat([df1,df2.reindex(df1.index)],axis=1))
print("右外连接")
print(pd.concat([df2,df1.reindex(df2.index)],axis=1))
print("内连接")
print(pd.concat([df2.reindex(df1.reindex(df2.index).index)],axis=1))
```
程序运行截图：

{% include aligner.html images="blog-img/machine/23.png"%}

#### 数据筛选query
`DataFrame.query(expr, inplace=False, **kwargs)`，用于通过boolean表达式来查询dataframe中的列。
主要参数为expr，它是字符串表达式，有如下说明：

可以引用变量，方法是在变量前添加一个@字符，例如@a + b。<br>
可以在反引号内将包含空格或运算符的列名引用起来。 这样，您还可以转义以数字开头或Python关键字的名称。 基本上是无效的Python标识符。 

## matplotlib（图像绘制）

#### 函数应用
函数签名：
```py
def plot(*args, scalex=True, scaley=True, data=None, **kwargs):
```

*	x: 横坐标，可选的， 默认为 range(len(y))
*	y: 纵坐标，即数据项，可以是一维或多维的列表或数组
*	markersize: 标记大小
*	color: 线条颜色
*	marker: 数据标记的形状，默认是没有标记
*	linestyle: 线条样式，默认为实线
代码演示：

```py
import matplotlib.pyplot as plt

x = [1, 2, 3]
y = [1, 2, 3]
# 以下两种写法等价，
plt.plot(x, y, color='green', marker='o', linestyle='dashed', linewidth=2, markersize=12)
# plt.flot(x, y, 'go--'，linewidth=2, markersize=12)
# 可以在一个画布上绘制多张图片，
y1 = [4, 5, 6]
plt.plot(x, y1, color='red', marker='*', linestyle='solid', linewidth=2, markersize=12)
plt.show()
```

程序运行截图：
{% include aligner.html images="blog-img/machine/24.png"%}

#### 重要示例

##### 示例1（创建4个折线图）
说明：使用plot实现，其中show函数主要实现图像的展示工作。<br>
代码演示：

```py
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

data = pd.DataFrame(np.random.randn(1000,4),index=np.arange(1000),columns=list("ABCD"))

data = data.cumsum()    # 累加
data.plot()
plt.show()
```

程序运行截图：
{% include aligner.html images="blog-img/machine/25.png"%}

##### 示例二（创建2个散点图）
代码演示：
```py
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

data = pd.DataFrame(np.random.randn(1000,4),index=np.arange(1000),columns=list("ABCD"))
data = data.cumsum()    # 累加
ax = data.plot.scatter(x='A',y='B',color='DarkBlue',label="Class 1")
data.plot.scatter(x='A',y='C',color='DarkGreen',label="Class 2",ax=ax)
plt.show()
```
程序运行截图：
{% include aligner.html images="blog-img/machine/26.png"%}

#### 日常问题
##### 图形中文乱码

解决方法：更改字体防止图形乱码
```py
from matplotlib import pyplot as pl
pl.rcParams['font.sans-serif'] = ['SimHei']
```