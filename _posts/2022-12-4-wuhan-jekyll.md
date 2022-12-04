---
layout: post
title: Jekyll 入门指导
author: Ranok
color: brown
tag: [Jekyll,web前端]
thumbnail: "assets/img/thumbnails/feature-img/jekyll.png"
permalink: jekyll
---

jekyll是一个简单的免费的Blog生成工具，类似WordPress。但是和WordPress又有很大的不同，原因是jekyll只是一个生成静态网页的工具，不需要数据库支持。但是可以配合第三方服务,例如Disqus。最关键的是jekyll可以免费部署在Github上，而且可以绑定自己的域名。

---

## 前言

该博客的部署使用的就是Jekyll框架，Jekyll是一门很成熟的技术（也可能是有点老的缘故），他可以将makedown格式的文档转化成一个个静态的页面，即便你没有系统的学过前端三件套也可以制作自己的主页（真的太棒了！）。

对于使用者来说只需要找到对应的资源模板，套用jekyll即可得到你想要的博客。

如果你想要了解更多，这个是Jekyll官网的传送门 $$\Longrightarrow$$ [Jekyll](https://www.jekyll.com.cn/)

---

## Jekyll 基础知识

### 基本结构
Jekyll 也遵循「约定大于配置」的基本原则，所以上手成本极低。

在新创建的项目目录下，有几个重要的文件夹：

#### _layouts

用于存放各种布局.html 的文件用于对.md文件的转换，在md设置的消息头中的变量，.md文件选择了layout布局之后，会引入对应的布局.html中，html会存放这些变量的默认值，

#### _drafts 

用于存放.md博客的草稿，不会再jekyll工作的时候生成，需要使用指令jekyll server –draft 才会显示在界面中
#### _posts

用于存放博客文章
#### _site

用于存放项目构建完成之后所生成的静态文件，也就是说，静态网站的所有文件都会来源于此，其中 CSS 文件、JS 文件以及图片文件，会存放在该目录下的 assets 文件夹中。我们可以直接把该目录下的文件拿去部署

除此之外，还有一些其他文件：
#### _config.yml

是项目的配置文件，一些全局配置会写在这个文件内，比如 collections（后续推文会讲解），默认文件/路径，等等。总之，这里可以自定义很多东西

####  .gitignore

创建项目时会自动生成，不需要纳入到 CVS 的文件存放于此，它可以限制一些元素在_site 中的生成

#### Gemfile & Gemfile.lock

存放项目所依赖的 Ruby gems，里面拥有存放页面的样式信息，当新加入了主题配置之后，需要使用bundle install指令安装新的配置才能使用。需要使用新的主题时，需要在_config.yml文件的there做更改。注意，使用了新的布局之后可能会导致一些布局不可用，例如“post”，因为在新的主题上可能没有定义这样的布局。所以使用新的布局之后要在_layout中查看一下是否有对应的布局可以使用。

#### about.md 

会存放有关在界面中的about的内容，生成的页面会出现在主界面上的位置，同理命名其他的文件也会在主界面的上方出现

---

## makedown 语法
#### permalink
可以用于自定义所创建页面的URL。例如，permalink：/Jekyll/ 表示创建的页面会在主页面URL中后加上/Jekyll

#### layout
表示自己所使用的界面样式，常见的值有post

#### ._config.yml

1. defaults：可用于写一些默认值，例如为layout设置默认值（要注意以下冒号的位置）
```yml
defaults:
  - 
    scope:
      path: ""  # 这里填写此默认值影响的返回路径
    values:   # 这里补充默认值
        layout: "post"
```
再例如对图片文件的加载：
```yml
defaults:
  -
    scope:
      path: "assets/img"
    values:
      image: true
```
该例子表示，在html文件中可能加载图片信息的位置会在，assets/img的文件夹下寻找

---
## 常用指令
1.	`jekyll new 工程名`  创建工程
2.	`bundle exec jekyll server`   启动项目，启动项目之后可以在浏览器中访问http://127.0.0.1:400/看到效果。
3.	`jekyll new PATH --blank`  创建新的空项目
4.	`jekyll build` 或 `jekyll b` 构建项目，生成可部署的 _site 目录
5.	`jekyll serve` 或 `jekyll s`  构建并运行项目，会自动监听文件变化，不需要反复执行
6.	`jekyll clean`  清除所有的构建产物
7.	`jekyll new-theme`  创建一个新的主题脚手架
8.	`jekyll doctor`  诊断，输出所有已经废弃的依赖包或者有问题的配置
