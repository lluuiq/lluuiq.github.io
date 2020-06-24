---
title: CLion配置C/C++开发环境
comments: true
toc: true
top: false

categories:
- [笔记,C]
tags: [CLion,C,C++]

date: 2020-04-06 22:33:21
---

记录配置CLion的过程

<!-- more -->

## 安装MinGW

MinGW下载地址：[MinGW](https://osdn.net/projects/MinGW/releases/)

在中间点击图标下载windows版

![image-20200406015857057](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406015858.png)

下载后打开安装，一直下一步最后安装完成后点击Continue。

在打开的界面中，`Basic Setup`中勾选`MinGW32-gcc-g++-bin`。

![image-20200406224030801](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225159.png)

然后进入`All Packages`，找到`mingw32-make-bin`勾选。

![image-20200406224255010](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225203.png)

然后点击菜单栏的`Installation ->  Apply Changes `安装勾选的包

安装完成后点击Close关闭即可。

若不小心安装后关掉了或者没有自动打开MinGW，可以在MinGW的安装目录中打开bin文件夹下的

`MinGW-get.exe`

![image-20200406020903397](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225207.png)

## 报错问题

若在安装时出现`输入错误: 没有文件扩展“.js”的脚本引擎`的报错，则打开运行，输入`regedit`

![image-20200406020051445](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406020052.png)

在路径`HKEY_CLASSES_ROOT\.js`下，更改默认值为`JSFile`

![image-20200406020303194](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406020304.png)

## 添加环境变量

右键我的电脑，点击属性，然后进入高级系统设置

![image-20200406021230911](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406021233.png)

点击环境变量

![image-20200406021307818](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225211.png)

找到系统变量的Path，双击进入编辑

![image-20200406021429668](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406021431.png)

点击新建，添加路径：

```
C:\MinGW\bin
```

其中`C:\MinGW`为安装MinGW时的默认路径，若有修改则换为对应路径

然后打开CMD，输入

```
gcc -v
```

查看是否配置成功

## CLion配置

安装CLion后，并进行基础配置后，会提示配置C/C++环境，确保Environment为MinGW的安装目录即可。

Make、C语言编译器、C++编译器会自动搜索bin目录下上文中安装好的包（若提示没找到则自行选取路径，若在目录中没找到说明没有安装成功）

![image-20200406224427755](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225216.png)

其他无需更改，点击OK即可。

然后就可以新建一个C语言项目

![image-20200406225107766](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225218.png)

创建完成后会默认生成初始化代码块

![image-20200406225309144](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225316.png)

然后在菜单栏的Run中点击Run…

![image-20200406225337183](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225344.png)

![image-20200406225355896](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225357.png)

初次运行会进行编译，等待编译完成后便会输出结果

![image-20200406225425856](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225427.png)