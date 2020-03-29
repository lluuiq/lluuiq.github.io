---
title: PyCharm+Anaconda3+PyQt环境配置
comments: true
toc: true
top: false
categories:
  - - 笔记
    - python
tags:
  - Anaconda3
  - PyQt
date: 2020-03-29 00:13:44
---

记录用Pycharm搭建PyQt环境的过程

<!-- more -->

## 配置Qt Designer

下载PyCharm与Anaconda3后，Anaconda3的包中集成了PyQt，并且也安装了Qt Designer

其中Qt Designer位于Anaconda3根目录/Library/bin/designer.exe（windows）

打开PyCharm设置，在Tools中点击External Tools，然后点击+号添加

![image-20200329002445201](https://gitee.com/lluuiq/blog_img/raw/master/img/20200329003506.png)

然后在设置的界面输入名称与描述（自定义）

Program为designer.exe路径，比如我的路径为`C:\Anaconda3\Library\bin\designer.exe`

Working directory设置为项目路径，可以直接复制粘贴该变量或者在右边的Insert Macro中找到ProjectFileDir，点击添加（结果都一样）。最后点击OK即可。

![image-20200329002702298](https://gitee.com/lluuiq/blog_img/raw/master/img/20200329003510.png)

```
$ProjectFileDir$
```

回到External Tools界面点击OK保存。

配置完成后，即可通过右键菜单栏启动Qt designer

![image-20200329003350595](https://gitee.com/lluuiq/blog_img/raw/master/img/20200329003512.png)

或者点击PyCharm上方菜单栏的Tools来启动

![image-20200329003456533](https://gitee.com/lluuiq/blog_img/raw/master/img/20200329003514.png)

## 配置pyuic

添加pyuic用于将Qt designer生成的.ui文件转为.py文件

在设置的External Tools添加一个新的Tool

名称与描述自定义，Program为Anaconda3根目录下的python.exe路径

Arguments填以下命令

```
-m PyQt5.uic.pyuic  $FileName$ -o $FileNameWithoutExtension$.py
```

Working directory使用当前文件所在的目录

```
$FileDir$
```

![image-20200329005406124](D:\blog\source\_posts\新建文章.assets\image-20200329005406124.png)

添加后保存即可。这样每次用designer生成的代码只需要右键->External Tools->pyuic即可生成python文件在相同目录下。