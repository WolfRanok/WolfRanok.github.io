---
layout: post
title: 网络爬虫
author: Ranok
tags: [python, 爬虫, 期末考试]     #标签会影响
feature-img: "assets/img/feature-img/spider.jpg" # 这是一个会出现在博客文章内部的图片
thumbnail: "assets/img/thumbnails/feature-img/spider.jpg" # 这是一个会出现在博客外部的图片
permalink: crawler # 这条会将该界面的URL自定义
---

网络爬虫（Web Crawler）是一种自动化程序，它可以在互联网上浏览和收集信息。它们可以发现和抓取网站上的所有内容，包括文本、图片、视频、音频等，并将这些数据保存到数据库或文件中。

---

# 目录

- [目录](#目录)
- [前言](#前言)
- [正文](#正文)
  - [选择题部分](#选择题部分)
    - [1 下列选项中，不能用于解析网页数据的是（）](#1-下列选项中不能用于解析网页数据的是)
    - [2 下列选项中，用于匹配任意字符数字的是（）](#2-下列选项中用于匹配任意字符数字的是)
    - [3 下列选项中，用于在Xpath中选取属性节点的是（）](#3-下列选项中用于在xpath中选取属性节点的是)
    - [4 列选项中，关于re模块的说法错误的是（）](#4-列选项中关于re模块的说法错误的是)
    - [5 下列选项中，关于lxml说法错误的是（）](#5-下列选项中关于lxml说法错误的是)
    - [6 下列选项中，关于Selenium描述错误的是（）](#6-下列选项中关于selenium描述错误的是)
    - [7 下列选项中，属于Chrome浏览器驱动程序的是（）](#7-下列选项中属于chrome浏览器驱动程序的是)
    - [8 下列选项中，用于根据指定URL地址访问页面的方法是（）](#8-下列选项中用于根据指定url地址访问页面的方法是)
    - [9 下列选项中，通过类名定位元素的方法是（）](#9-下列选项中通过类名定位元素的方法是)
    - [10 下列选项中，关于显式等待和隐式等待描述错误的是（）](#10-下列选项中关于显式等待和隐式等待描述错误的是)
  - [简答题 \& 论述题](#简答题--论述题)
    - [1 什么是网络爬虫？](#1-什么是网络爬虫)
      - [理论定义：](#理论定义)
      - [分类：](#分类)
    - [2 网页的分类（简答题问法）](#2-网页的分类简答题问法)
    - [3 网络爬虫的应用场景有哪些？](#3-网络爬虫的应用场景有哪些)
    - [4 网络爬虫合法性研究](#4-网络爬虫合法性研究)
      - [4.1论述题的考法](#41论述题的考法)
        - [网络爬虫是否合法？](#网络爬虫是否合法)
        - [合法合规的爬虫是什么样的？](#合法合规的爬虫是什么样的)
        - [你认为不合法合规的爬虫是什么样的？](#你认为不合法合规的爬虫是什么样的)
      - [4.2简答题的问法](#42简答题的问法)
        - [什么是robots.txt协议？](#什么是robotstxt协议)
    - [5 防爬虫的应对策略有哪些？](#5-防爬虫的应对策略有哪些)
    - [6 http和https 的区别？](#6-http和https-的区别)
    - [7 网页的分类（论述题问法）](#7-网页的分类论述题问法)
      - [7.1静态网页，动态网页是什么？](#71静态网页动态网页是什么)
      - [7.2静态网页的特点](#72静态网页的特点)
      - [7.3动态网页的特点](#73动态网页的特点)
      - [7.4动态网页采集技术类型有哪些？你最喜欢用哪一个](#74动态网页采集技术类型有哪些你最喜欢用哪一个)
  - [综合应用题](#综合应用题)
    - [1 Scrapy-Redis架构](#1-scrapy-redis架构)
    - [2 scrapy.Spider类的常用属性和方法](#2-scrapyspider类的常用属性和方法)
  - [程序题部分](#程序题部分)
    - [程序填空](#程序填空)
    - [程序解释题](#程序解释题)

---

# 前言

&emsp;&emsp;本博客针对，网络爬虫期末考试进行整理。部分整理针对题型进行整理。祝你取得一个**好成绩**！。

---

# 正文

## 选择题部分

> 针对平时测试所整理，有概率考到

### 1 下列选项中，不能用于解析网页数据的是（）
    
    A. LXML     
    B. Beautiful Soup  
    C. JSONPath   
    D. Requests

&emsp;&emsp;正确答案：D

### 2 下列选项中，用于匹配任意字符数字的是（）
    
    A. \w    
    B. \d   
    C. \D    
    D. \W

&emsp;&emsp;正确答案：B

### 3 下列选项中，用于在Xpath中选取属性节点的是（）
    
    A. /     
    B. //    
    C. @   
    D. #


&emsp;&emsp;正确答案：C

### 4 列选项中，关于re模块的说法错误的是（）
   
    A. re模块是Python中可操作正则表达式的模块
    B. re模块中的compile( )函数用于对正则表达式进行编译
    C. 使用findall( )方法或finditer( )方法可以获取所有与正则表达式匹配的内容
    D. 使用finditer( )方法返回的是列表，使用findall( )方法返回的是迭代器

&emsp;&emsp;正确答案：D

### 5 下列选项中，关于lxml说法错误的是（）
    
    A. Element类的find( )方法用于从根节点开始查找，并以列表形式返回匹配的节点
    B. 使用lxml库可以对HTML文档或XML文档中的节点进行定位和提取
    C. ElementTree类的对象可以理解为HTML文档或XML文档的树节点
    D. 使用lxml库可以对HTML文档缺少的<html>和<body>元素自动补全

&emsp;&emsp;正确答案：D

### 6 下列选项中，关于Selenium描述错误的是（）
    
    A. Selenium是一个开源的便携式自动化测试工具
    B. Selenium可以直接在浏览器上运行
    C. Selenium自身携带浏览器，并支持浏览器的功能
    D. Selenium可以根据指令自动加载网页或判断网页上是否发生动作

&emsp;&emsp;正确答案：C

### 7 下列选项中，属于Chrome浏览器驱动程序的是（）
    
    A. ChromeDriver
    B. geckodriver
    C. operachromiumdriver
    D. IEDriverServer

&emsp;&emsp;正确答案：A

### 8 下列选项中，用于根据指定URL地址访问页面的方法是（）
    
    A. get()
    B. Post()
    C. head()
    D. put()

&emsp;&emsp;正确答案：A

### 9 下列选项中，通过类名定位元素的方法是（）
    
    A. find_element_by_name()
    B. find_element_by_class_name()
    C. find_element_by_id()
    D. find_element_by_tag_name()

&emsp;&emsp;正确答案：B

### 10 下列选项中，关于显式等待和隐式等待描述错误的是（）
    
    A. 隐式等待就是设置一个全局的最大等待时间
    B. 显式等待会先指定某个条件，再设置最长等待时间
    C. 隐式等待可作用于单个元素
    D. 显式等待只能作用于单个元素

&emsp;&emsp;正确答案：C

---

## 简答题 & 论述题

### 1 什么是网络爬虫？

    本题考察简答题 5'

#### 理论定义：

&emsp;&emsp;网络爬虫就是一个模拟真人浏览万维网行为的程序，这个程序可以代替真人自动请求万维网，并接收从万维网返回的数据。与真人浏览万维网相比，网络爬虫能够浏览的信息量更大，效率也更高。（重点）

#### 分类：

&emsp;&emsp;通用网络爬虫、聚焦网络爬虫、增量式网络爬虫、深层网络爬虫。

&emsp;&emsp;通用网络爬虫:是指访问全互联网资源的网络爬虫。它是搜索引擎（如百度、谷歌、雅虎等）抓取系统的重要组成部分，主要用于将互联网中的网页下载到本地，形成一个互联网内容的镜像备份。（重点）

&emsp;&emsp;聚焦网络爬虫:是指有选择性地访问那些与预定主题相关网页的网络爬虫，它根据预先定义好的目标，有选择性地访问与目标主题相关的网页，获取所需要的数据。

&emsp;&emsp;增量式网络爬虫:是指对已下载的网页采取增量式更新，只抓取新产生或者已经发生变化的网页的网络爬虫。

&emsp;&emsp;深层网络爬虫:是指抓取深层网页的网络爬虫，它要抓取的网页层次比较深，需要通过一定的附加策略才能够自动抓取，实现难度较大。

---

### 2 网页的分类（简答题问法）

    本题考察简答题 5'

&emsp;&emsp;主要分为表层网页，深层网页。

&emsp;&emsp;表层网页是指传统搜索引擎可以索引的页面，主要以超链接可以到达的静态网页构成的网页。<br>
&emsp;&emsp;深层网页是指大部分内容无法通过静态链接获取的，只能通过用户提交一些关键词才能获取的网页，如用户注册后内容才可见的网页。

---

### 3 网络爬虫的应用场景有哪些？

    本题考察简答题 5'

&emsp;&emsp;搜索引擎、舆情分析与监测、聚合平台、出行类软件等。

&emsp;&emsp;搜索引擎：如百度、谷歌、雅虎等。

&emsp;&emsp;舆情分析与监测：例如用于过滤敏感词汇。发掘舆情热点，跟踪目标话题。

&emsp;&emsp;运用网络爬虫技术对一些电商平台上的商品信息进行采集，将所有的商品信息放到自己的平台上展示，并提供横向数据的比较。

&emsp;&emsp;出行类软件，比如飞猪、携程、去哪儿等，也是网络爬虫应用比较多的场景。

---

### 4 网络爬虫合法性研究

    本题考察简答题 5' & 论述题 16'

#### 4.1论述题的考法

##### 网络爬虫是否合法？
&emsp;&emsp;（1）爬虫本身不违法。<br>
&emsp;&emsp;（2）如果爬虫程序采集到会侵犯到有关公民信息，以及商业机密等内容，并将之用于非法途径的，则肯定构成非法获取公民个人信息的违法行为。<br>
&emsp;&emsp;（3）部分公司提供公开API接口允许爬取其数据。爬取这样的数据并不违法。<br>
&emsp;&emsp;（4）网络爬虫在遵守法律政策和网站协议的情况下是合法的。<br>

##### 合法合规的爬虫是什么样的？

&emsp;&emsp;（1）遵守robots.txt协议<br>
&emsp;&emsp;（2）不断请求而不会影响网站的正常运行<br>
&emsp;&emsp;（3）不获取敏感信息<br>
&emsp;&emsp;（4）不会对目标网站造成安全隐患<br>
&emsp;&emsp;（5）网站公开数据允许收集<br>
&emsp;&emsp;（6）爬虫有明确用户使用场景<br>

##### 你认为不合法合规的爬虫是什么样的？

&emsp;&emsp;（1）爬取未公开、未经许可、且带有敏感信息的数据。<br>
&emsp;&emsp;（2）使用技术手段不克制，造成提供信息的平台的服务资源损失。<br>
&emsp;&emsp;（3）出售个人信息，将爬取的信息用在了不正当商业行为中。<br>
&emsp;&emsp;（4）不遵循数据许可协议，超出约定的使用。<br>
&emsp;&emsp;（5）无限制地抓取网页。<br>
&emsp;&emsp;（6）使用爬虫，模拟用户行为欺瞒网站。

#### 4.2简答题的问法

##### 什么是robots.txt协议？

&emsp;&emsp;Robots协议又称爬虫协议，它是国际互联网界通行的道德规范，用于保护网站数据和信息不受侵犯。网站管理员通常会在网页根目录下放置一个符合Robots协议的robots.txt文件，用于告知哪些数据允许爬取，哪些数据不允许爬取。

---

### 5 防爬虫的应对策略有哪些？

&emsp;&emsp;添加User-Agent字段、降低访问频率、设置代理服务、识别验证码。<br>

&emsp;&emsp;1. 添加User-Agent字段:浏览器在访问网站时会携带固定的User-Agent，向网站表明自己的真实身份。所以可以在请求网页时携带User-Agent，将自己伪装成一个浏览器。

&emsp;&emsp;2. 降低访问频率:同一账户在较短的时间内多次访问了网页可能会被封禁。所以可以每抓取一次页面数据就休息几秒钟，或者限制每天抓取的页面数据的数量。

&emsp;&emsp;3. 设置代理服务:反复使用同一IP地址进行访问，则极易被网站认出是爬虫。所以可以在网络爬虫和Web服务器之间设置代理服务器。

&emsp;&emsp;4. 识别验证码:有些网站可能会要求该客户端进行登录验证，并随机提供一个验证码，为了应对这种发情况可以将爬虫像人类一样通过滑动或点击行为识别验证码。

---

### 6 http和https 的区别？

    本题考察简答题 5'

&emsp;&emsp;HTTP协议全称为超文本传输协议，它用于将Web服务器的超文本资源传送到浏览器中。

&emsp;&emsp;HTTPS协议是一种超文本传输安全协议。

&emsp;&emsp;两者的不同：<br>
&emsp;&emsp;HTTP中浏览器与Web服务器的连接是一种一次性连接，它限制每次连接只能处理一个请求。<br>
&emsp;&emsp;HTTPS在HTTP协议基础上添加了安全套接字协议，完成互联网数据传输加密，实现互联网传输安全保护。

---

### 7 网页的分类（论述题问法）

    本题考察论述题 16'

#### 7.1静态网页，动态网页是什么？

&emsp;&emsp;静态网页中包含的诸如文本、图像、FLASH动画、超链接等内容，在编写网页源代码时已经确定，基本上不会发生变化，除非更改源码。

&emsp;&emsp;动态网页有数据库支撑、包含程序以及提供与用户交互功能，如用户登录、用户注册、信息查询等功能，这些功能根据用户传入不同参数网页会显示不同数据。

#### 7.2静态网页的特点

&emsp;&emsp;1. 静态网页的内容相对稳定，一经上传至网站服务器，无论是否有用户访问内容都会一直保存在网站服务器上。<br>
&emsp;&emsp;2. 静态网页的访问速度快，访问过程中无须连接数据库。<br>
&emsp;&emsp;3. 静态网页没有数据库的支持，内容更新与维护比较复杂。<br>
&emsp;&emsp;4. 静态网页的交互性较差，在功能方面有较大的限制。

#### 7.3动态网页的特点

&emsp;&emsp;1. 动态网页一般以数据库技术为基础。<br>
&emsp;&emsp;2. 动态网页并不是独立存在于服务器上的网页文件，只有当用户请求时服务器才会返回一个完整的网页。<br>
&emsp;&emsp;3. 采用动态网页技术的网站可以实现更多的功能，如用户注册、用户登录、在线调查、用户管理、订单管理等。

#### 7.4动态网页采集技术类型有哪些？你最喜欢用哪一个

&emsp;&emsp;1. 基于浏览器自动化工具（如Selenium）的采集技术。
&emsp;&emsp;2. 基于HTML请求模拟采集技术。
&emsp;&emsp;3. 基于无界面浏览器的采集技术。
&emsp;&emsp;4. 基于API接口调用的采集技术。

&emsp;&emsp;我最喜欢用浏览器自动化工具Selenium，因为使用Selenium，对于动态网页的数据可以直接使用模拟浏览器运行的方式进行实现，这样做就可以不用管网页内部是如何使用JavaScript渲染页面的，在浏览器中看到是什么样的内容，抓取的结果便是什么样的内容。

---

## 综合应用题

> 本题型一张试卷只有一题，16分，一题分多个小点

### 1 Scrapy-Redis架构

&emsp;&emsp;绘制以下一张完整的图像。统一要求对关键名称写中文。

{% include aligner.html images="blog-img/spider/1.jpg" column=1 %}

&emsp;&emsp;注意这里A卷中，与画图题一起考的还有一个多选题，请排除**第二个选项**

---

### 2 scrapy.Spider类的常用属性和方法

&emsp;&emsp;1. name属性：设置爬虫文件的名称。<br>
&emsp;&emsp;2. allowed_domains属性：设置爬虫允许抓取的域名范围。<br>
&emsp;&emsp;3. start_urls属性：表示需要提交的初始URL地址。<br>
&emsp;&emsp;4. __init__()方法：负责初始化爬虫名称和初始URL列表。<br>
&emsp;&emsp;5. start_requests()方法：负责生成Requests对象，交给Scrapy下载。<br>
&emsp;&emsp;6. parse(response)方法：负责解析Response，并返回Item或Requests。<br>
&emsp;&emsp;7. log(message[level, component])方法：负责发送日志信息。


这个大题下面有关知识点的整理（不用背）（会考多选题和判断题）：

&emsp;&emsp;该文件中可以定义多个管道，这些管道会按照定义的顺序**依次处理**Item对象。（✔）

&emsp;&emsp;CrawlSpider类由于继承了Spider类，所以继承了Spider类的所有公有成员。此外，CrawlSpider类自身也定义了一些属性。在这里，我们着重了解一下rules属性。<br>rules属性是一个包含一个或多个Rule对象给续会介绍的列表。每个Rule对象对抓取网站的动作定义了特定表现。如果多个Rule对象匹配了同一个链接，则根据它们在本属性中定义的顺序，使用第一个Rule对象。

---

## 程序题部分

### 程序填空

以下代码要求掌握，共计13点

```py
  text = etree.HTML(html)
```

```py
  # 文章标题
  title = node.xpath('./a[1]/text()')[0]
  # 文章链接
  url = node.xpath('./a[1]/@href')[0]
  # 文章作者
  author = node.xpath('./div[@class="foruminfo"]//a/span/text()')[0]
```

```py
  item = {
    "文章标题": title,
    "文章链接": url,
    "文章作者": author,
    '发布时间': release_time,
  }
  items.append(item)
```

```py
  options = webdriver.ChromeOptions()
```

```py
  # text属性 : 获取当前dd节点以及它的子节点和后代节点的文本内容
  one_film_info_list = dd.text.split('\n')
```

```py
  item['name'] = one_film_info_list[1].strip()
  item['star'] = one_film_info_list[2].strip()
  item['time'] = one_film_info_list[3].strip()
  item['score'] = one_film_info_list[4].strip()
```

```py
  def get_html(self, url):
    html = requests.get(url=url, headers=self.headers).text
```

```py
  p = etree.HTML(html)
```

```py
  item['name'] = dd.xpath('.//p[@class="name"]/a/@title')[0].strip()
  item['star'] = dd.xpath('.//p[@class="star"]/text()')[0].strip()
  item['time'] = dd.xpath('.//p[@class="releasetime"]/text()')[0].strip()
```

```py
  item['score'] = ''.join(dd.xpath('.//p[@class="score"]/i/text()'))
```

```py
  name = 'itcast'		# 这个是试卷上会给的
  allowed_domains = ['itcast.cn']
```

```py
  # 创建MyspiderItem类的对象
  item = MyspiderItem()
```

```py
  # 将每个讲师的信息封装成MyspiderItem类的对象
  item["name"] = name[0]
  item["level"] = level[0] 在浏览器中看到是什么样的内容，抓取的结果便是什么样的内容
  item["resume"] = resume[0]
  items.append(item)
```

---

### 程序解释题

这里可能会有干扰项
> 以下为我个人作答并不一定是参考答案

```python
def load_page(url):
    '''
    作用:根据url发送请求，获取服务器响应文件
    url：需要爬取的url地址
    '''
    headers = {"User-Agent": "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident / 5.0;"}
    request = requests.get(url, headers=headers)
    return request.text
```

答：根据url，封装请求头，使用get方法发送请求。获取服务器响应文件，并返回文件内容。

---

```python
  print("正在保存" + filename)
  with open(filename, 'w', encoding='utf-8') as file:
    file.write(html)
```

答：以打印需要保存的文件名信息；将以读的形式打开（如果不存在就创建）文件，并写入对应的内容

---

```python
  url = f'http://bbs.itheima.com/forum-425-{page}.html'
  file_name = "第" + str(page) + "页.html"
  html = load_page(url)
  save_file(html, file_name)
```

答：获取`page`信息，拼接`url`；给获取到的url命名为“第”+page+“页.html”；传递url参数，调用load_page函数获取网页信息，调用save_file函数保存获取到的信息。

---

```python
  html = json.loads(response.text)
  count = html['Data']['Count']
  total = count // 10 if count % 10 == 0 else count // 10 + 1
```

答：`json.loads`是将响应内容中的`json`数据转为字典；`count`是从字典中获取职位总条数，`total`是计算得到的所要获取的页数。

---

```python
def detail_page(self, response):
    """一级页面解析函数：提取每页中10个职位的postid"""
    one_html = json.loads(response.text)
    for one_job_dict in one_html['Data']['Posts']:
      post_id = one_job_dict['PostId']
      # 拼接二级页面URL地址,再次交给调度器入队列
      two_url = 'https://careers.tencent.com/tencentcareer/api/post/ByPostId?timestamp=1593656158948&postId={}&language=zh-cn'.format(post_id)
      yield scrapy.Request(url=two_url, callback=self.get_job_info)   #将所有的信息交给自定义函数self.get_job_info处理

```

答：`two_url`拼接二级页面URL地址,再次交给调度器入队列；`yield scrapy.Request`将所有的信息交给自定义函数`self.get_job_info`处理

---

```py
def get_job_info(self, response):
  """提取每个职位的具体信息"""
  two_html = json.loads(response.text)
  item = TencentItem()
  item['job_name'] = two_html['Data']['RecruitPostName']
  item['job_address'] = two_html['Data']['LocationName']
  item['job_type'] = two_html['Data']['CategoryName']
  item['job_time'] = two_html['Data']['LastUpdateTime']
  item['job_responsibility'] = two_html['Data']['Responsibility']
  item['job_requirement'] = two_html['Data']['Requirement']

  # 至此,一个职位完整信息抓取完成,交给管道文件处理
  yield item
```

答：调用`json.loads`方法提取每个职位的具体信息；`yield item`至此,一个职位完整信息抓取完成,交给**管道文件处理**。

---


```py
driver = webdriver.Chrome()   # 创建一个浏览器对象，并打开
driver.maximize_window()    # 最大化窗口
driver.get(url='https://mail.qq.com/')  # 调用get方法发起请求

driver.switch_to.frame('login_frame')# 切换iframe子页面


# 2、用户名、密码、登录
driver.find_element_by_id('u').send_keys('2621470058')  # 这个不用管
driver.find_element_by_id('p').send_keys('zhanshen001') # 这个不用管
driver.find_element_by_id('login_button').click()   # 查找登录按钮的位置，并调用click方法单击此按钮。
```

以上注解已写在程序当中