---
title: Scrapy笔记
date: 2020-03-04 04:05:53 
comments: true
toc: true
top: false

categories: 
- [笔记,python]
tags: [python,爬虫,Scrapy]
---

记录学习Scrapy时遇到的坑

[Scrapy官方文档](https://scrapy-chs.readthedocs.io/zh_CN/latest/)

学习时看的视频：[【python爬虫_从入门到精通（高级篇）】scrapy框架、反爬、分布式爬虫](https://www.bilibili.com/video/av57909837)

<!-- more -->

# 使用笔记

## 创建爬虫项目

CMD命令：

```
scrapy startproject 【项目文件夹名】
```

会在输入命令的目录中生成一个名称为【项目文件夹名】的文件夹用来存放爬虫项目

## 创建爬虫

CMD命令：

```
cd 【项目文件夹名】
scrapy genspider 【爬虫的名字】 "【爬取的域名】"
```

进入创建好的爬虫项目中创建爬虫，名字不能与其他爬虫重复，且不能与项目名相同。

爬取的域名指定爬取范围，使该爬虫仅仅在该域名内的页面中进行爬取。

## 更改设置

首先更改设置中的一些值

善用``CTRL+F`搜索参数，快速找到位置

打开爬虫根目录中的settings.py，进行更改。

```
# 设置爬取的延迟，单位为秒，即间隔1秒爬取一次
DOWNLOAD_DELAY = 1

# 不遵守协议
ROBOTSTXT_OBEY = False

# 设置默认的请求头，如有需要可以添加其他信息。
DEFAULT_REQUEST_HEADERS = {
  'User_Agent' :'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Safari/537.36'
}

# 设置pipelines自动运行，用于自动根据代码保存数据，找到后取消注释即可，不用更改
ITEM_PIPELINES = {
  # 执行优先级300，值越小，优先级越高
   '【爬虫项目名称】.pipelines.【爬虫项目名称】Pipeline': 300,
}

# 不显示warning以下级别的输出日志
LOG_LEVEL="WARNING"
```

## 创建运行脚本

创建后，不用每次运行爬虫都要输入终端命令，只需要执行python文件即可。

在项目中的任意位置创建一个python文件，名字自定义

输入内容：

```
from scrapy import cmdline

cmdline.execute('scrapy crawl 【爬虫的名字】'.split())
```

爬虫的名字指的是创建爬虫时用的名字，而不是项目的名字。

## 创建CrawlSpider爬虫

scrapy爬虫的进化版

CMD命令：

```
scrapy genspider -t crawl 【爬虫名字】 “【域名】”
```

## Scrapy Shell

cmd终端中，进入爬虫项目文件夹，输入

```
scrapy shell 【链接】
```

即可打开scrapy shell，

用于进行一些不调用scrapy引擎进行一些测试（如正则表达式，检查获取信息的内容等等）

 ![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023136.png)

## 关闭windows的快捷编辑模式

有时scrapy会在跳转到另一页面时莫名奇妙的自动终止，关掉windows的快捷编辑模式，问题得以解决。



# 报错笔记

# ERROR: Spider error processing

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023137.png)

response.body返回的是二进制文件，不能用w方式进行写入，应改为wb