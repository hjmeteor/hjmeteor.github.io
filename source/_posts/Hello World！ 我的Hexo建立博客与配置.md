---
title: Hello World！ 我的Hexo建立博客与配置
data: 2017-07-20 20:00:00
tags: Hexo, Github, Tutorial, Setting
---
![hexo+github](http://otedbc93y.bkt.clouddn.com/hexo+github.png-Normal)

# 前言：
最近闲着无聊，搞个博客没事儿吐槽下，自己建站耗时耗力，选择了HEXO来建站，据说生成静态网页的速度比Jekyll快（虽然Jekyll官方推荐，主要是相比于Ruby我觉得我更熟悉Node.js,而且Windows用Ruby很蛋疼）。而且一直很喜欢用Markdown写东西，很带感。下面我就是记录下我的过程没有详细的解释哈哈，因为懒。

# 一步一步来：
## 1. 获取绑定域名：
选择了github student package里的一年免费的namecheap的.me域名，全程无脑操作，自动和Github Page绑定还有DNS解析也自动弄好了弄好了，如下:

    A Record： 192.30.252.153
    A Record： 192.30.252.154
    CNAME Record: hjmeteor.github.io.

## 2. 建立Repo：
    仓库名应该为：用户名.github.io

## 3. 安装Node.js：
Node.js下载地址：[https://nodejs.org/en/download/](https://nodejs.org/en/download/)

检查Node.js是否安装完成：
```bash
$ node -v
```

## 4. 安装Hexo：
用npm命令安装Hexo，安装时间较长：
```bash
$ npm install -g hexo-cli 
```
在本地找个地方初始化博客：
```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```
检测是否初始化成功：
```bash
$ hexo g 
($ hexo generate)
hexo s
($ hexo server)
```
## 5. 推送网站：
首先有2个配置文件都叫**_config.yml**，一个在**根目录**下，一个在**themes**文件夹下，所以前者称之为站点配置文件，后者是主题配置文件。如下是配置文件各项说明：
```yml
# Site #站点信息
title:  #标题
subtitle:  #副标题
description:  #站点描述，给搜索引擎看的
author:  #作者
email:  #电子邮箱
language: zh-CN #语言
timezone: #时区
avatar: #网站头像

# URL #链接格式
url:  #网址
root: / #根目录
permalink: :year/:month/:day/:title/ #文章的链接格式
permalink_defaults:
# Directory #目录
source_dir: source #源文件目录
public_dir: public #生成的网页文件目录
tag_dir: tags #标签目录
archive_dir: archives #存档目录
category_dir: categories #分类目录

# Writing #写作
new_post_name: :title.md #新文章标题
default_layout: post #默认的模板，包括 post、page、photo、draft（文章、页面、照片、草稿）
titlecase: false #标题转换成大写
external_link: true #在新选项卡中打开连接
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
highlight: #语法高亮
  enable: true #是否启用
  line_number: true #显示行号
  tab_replace:

# Category & Tag #分类和标签
default_category: uncategorized #默认分类
category_map:
tag_map:

# Date / Time format #日期时间格式
date_format: YYYY-MM-DD #参考http://momentjs.com/docs/#/displaying/format/
time_format: H:mm:ss

# Pagination #分页
per_page: 10 #每页文章数，设置成 0 禁用分页
pagination_dir: page

# Extensions #拓展插件
theme: icarus #主题 我用的这个icarus
exclude_generator:
plugins: #插件，例如生成 RSS 和站点地图的
- hexo-generator-feed
- hexo-generator-sitemap

# Deployment #部署配置
deploy:
  type: git
  repo: repo的地址
  branch: master
```
将deployment配置好后由于我们使用的是git，所以要有如下命令：
```bash
$ npm install hexo-deployer-git --save
```
所以之后做出修改后我们可以有如下命令：
```bash
$ hexo clean  
$ hexo d -g
```
> Hexo常用命令:   
> Hexo npm update hexo-cli -g #升级  
> hexo init#初始化博客 命令简写   
> hexo n "我的博客" == hexo new "我的博客" #新建文章   
> hexo g == hexo generate #生成   
> hexo s == hexo server #启动服务预览   
> hexo d == hexo deploy #部署   
>hexo d -g == hexo generate -> hexo deploy  
> hexo server #Hexo会监视文件变动并自动更新，无须重启服务器   
> hexo server -s #静态模式   
> hexo server -p 5000 #更改端口   
> hexo server -i 192.168.1.1 #自定义 IP   
> hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令

## 6. 更换主题：
我用的主题是[**icarus**](https://github.com/ppoffice/hexo-theme-icarus)。安装方法参见他的网站。
## 7. 添加插件：
## 8. 各种小改动：
1. 添加了各种图标
2. 更换了share插件
3. 瞎折腾CSS：

    可以看看这个[Hexo主题配置与优化（二）](http://jerry011235.github.io/2015/05/06/Hexo%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E4%B8%8E%E4%BC%98%E5%8C%96%EF%BC%88%E4%BA%8C%EF%BC%89/)
4. 标签云变色：
    参考这个[标签云](http://jerry011235.github.io/2015/05/16/Hexo%E5%BD%A9%E8%89%B2%E6%A0%87%E7%AD%BE%E4%BA%91/)
## 100. 注意事项：
1. 将CNAME文件和README.md文件放入source中，否则一次deploy就会让在根目录的他们消失。CNAME中将我们的网址输入。然后在站点_config.yml文件中添加一行：

    skip_render: README.md

目的是防止README.md被渲染