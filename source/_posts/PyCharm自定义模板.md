---
title: PyCharm自定义模板
comments: true
toc: true
top: false
categories:
  - - 笔记
tags:
  - PyCharm
date: 2020-03-30 08:41:07
---

- 自定义文件模板：

  ​	新建一个文件时自动添加一些头信息。

- 自定义代码块模板 ：

  ​	当有的代码自己需要多次使用时，一次次重复编写效率过低，故可以自定义一个缩写来实现按TAB自动将代码块补全。

<!-- more -->

## 文件模板

详细说明可查看：[官方文档](https://www.jetbrains.com/help/pycharm/2017.1/file-and-code-templates-2.html)

打开PyCharm的设置，搜索`File and Templates`，即可看到设置模板的界面

![image-20200330084900658](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330091231.png)

不同的文件可以设置不同的模板，这里设置python文件，选中`Python Script`，在右边的编辑初添加信息。

首先添加两行代码用于指定python环境以及采用utf-8编码

```python
# !/usr/bin/env python3
# _*_coding:utf-8 _*_
```

接下来自定义文件的信息。

不同的变量名：

- `${PROJECT_NAME}` - the name of the current project.
- `${NAME}` - the name of the new file which you specify in the New File dialog box during the file creation.
- `${USER}` - the login name of the current user.
- `${DATE}` - the current system date.
- `${TIME}` - the current system time.
- `${YEAR}` - the current year.
- `${MONTH}` - the current month.
- `${DAY}` - the current day of the month.
- `${HOUR}` - the current hour.
- `${MINUTE}` - the current minute.
- `${PRODUCT_NAME}` - the name of the IDE in which the file will be created.
- `${MONTH_NAME_SHORT}` - the first 3 letters of the month name. Example: Jan, Feb, etc.
- `${MONTH_NAME_FULL}` - full name of a month. Example: January, February, etc.

示例：

```python
# @Author : lluuiq
# @File : ${NAME}.py
# @project : ${PROJECT_NAME}
# @Time : ${DATE} ${TIME}


```

最终设置结果：

![image-20200330090922739](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330091236.png)

设置后保存，新建一个python文件即可看到效果

![image-20200330091111859](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330091240.png)

## 代码块模块

打开PyCharm的设置。搜索`Live Template`，找到python，点击右方的`+`添加自定义代码块

![image-20200330091434748](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330092511.png)

选择第一个

![image-20200330091507144](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330092515.png)

设置界面如图

![image-20200330091546411](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330092517.png)

Abbreviation为缩写，即输入什么内容后按TAB会输出该代码块

Template text为自定义的代码块

在下方点击Define，勾选python

Description为描述，可以在输入缩写时弹出的信息中看到该描述

示例：

![image-20200330091927336](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330092520.png)

在python文件中输入`demo`，可看到如下信息。

![image-20200330092010175](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330092522.png)

按TAB后，会自动输出该部分自定义的代码

![image-20200330092035228](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330092524.png)

**优化：**回到设置界面，将代码中要输入的内容修改为参数类型

![image-20200330092229808](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330092526.png)

这样输出自定义的代码后，\$text1\$以及\$text2\$的内容默认为空，且光标会自动定位在\$text1\$处，当输入内容后按回车，光标会自动移动到\$text2\$处，最后移动到\$code\$处。

也可以用相同的参数名，这样输出代码后，光标会自动选中两个\$text\$，此时会对两处同时进行修改，按回车后跳转到\$code\$处。

![image-20200330092201513](https://gitee.com/lluuiq/blog_img/raw/master/img/20200330092530.png)