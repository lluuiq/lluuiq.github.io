---
title: 在Pycharm中运行jupyter notebook
comments: true
toc: true
top: false
categories:
  - - 笔记
    - python
tags:
  - pycharm
  - python
  - Anaconda
date: 2020-03-02 22:55:47
---

因为熟悉了pycharm，所以想在pycharm上运行jupyter notebook而不用再打开网页。

首先确定已经安装了Anaconda3以及Pycharm

官方下载地址：[Anaconda3](https://www.anaconda.com/distribution/)、[Pycharm](https://www.jetbrains.com/pycharm/)

其中Pycharm要求是专业版，社区版的新版本已经不再支持jupyter notebook。

爱心分享方法百度

<!-- more -->

# Pycharm中使用Anaconda3的python环境

将Anaconda3的python环境设置为默认环境（若有需要不要设置成默认，根据项目不同设置不同的环境）

在Pycharm首页，进入设置。

![image-20200303020334884](C:%5CUsers%5C84452%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200303020334884.png)

在左边进入Project Interpreter。

![image-20200303020358934](C:%5CUsers%5C84452%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200303020358934.png)

点击如图所示右边的齿轮，选择Add

![image-20200303020447611](C:%5CUsers%5C84452%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200303020447611.png)

选择Conda环境，然后选择已经存在的环境，路径为安装的Anaconda3根目录下的python.exe。并勾选全局配置。然后点击OK。

![image-20200303020608279](C:%5CUsers%5C84452%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200303020608279.png)

添加后，在环境配置的界面会大致如图所示。然后点击右下方的Apply，然后点击OK保存。

![image-20200303020743765](C:%5CUsers%5C84452%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200303020743765.png)

这样在新建一个项目时，环境默认为安装的Anaconda3环境（没有使用虚拟环境，若有需要自行修改）

![image-20200303020837152](C:%5CUsers%5C84452%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200303020837152.png)

# 新建jupyter notebook文件进行测试

新建好项目后，右键项目，New里选择 Jupyter Notebook

![mark](http://blogimg.wa2000.cn/blog/20200303/lrQefnBf6l2w.png?imageslim)

如图，Pycharm会自动连接到jupyter notebook地址。

![mark](http://blogimg.wa2000.cn/blog/20200303/3VdTct3dyImK.png?imageslim)

# 配置环境变量（若未能成功打开jupyter notebook）

打开我的电脑的属性，进入高级系统设置

![mark](http://blogimg.wa2000.cn/blog/20200302/goYoDKsvV8yC.png?imageslim)

进入下方的环境变量

![mark](http://blogimg.wa2000.cn/blog/20200302/wtssD7811mIC.png?imageslim)



在系统变量中找到path，双击进入编辑

![mark](http://blogimg.wa2000.cn/blog/20200302/PJd373CSIbea.png?imageslim)

点击新建

![mark](http://blogimg.wa2000.cn/blog/20200302/9rAL6bIYpRWd.png?imageslim)

加入三条环境变量，路径为Anaconda3的安装的根目录、根目录下的Scripts文件夹、根目录下的Library中的bin文件夹。顺序无影响。

![mark](http://blogimg.wa2000.cn/blog/20200302/oR9inJmA0ze9.png?imageslim)

```
XXX\Anaconda3\Library\bin
XXX\Anaconda3\Scripts
XXX\Anaconda3
```

最后一直点确定就可以保存，然后重启电脑让配置生效。

重启后，打开终端，输入

```
jupyter notebook
```

出现如图所示信息，且打开了jupyter notebook则说明配置成功。

![mark](http://blogimg.wa2000.cn/blog/20200302/Sj7akUaKvEDw.png?imageslim)