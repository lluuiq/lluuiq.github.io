---
title: Atom编辑器尝试
comments: true
toc: true
top: false
categories:
  - - 笔记
tags:
  - Atom
date: 2020-04-06 00:40:35
---

从最早的Notepad++，到后面Sublime Text，再转为VS Code，一直感觉编辑器都有说不出的缺陷。

一开始追求编辑的插件功能，后面又感觉插件管理不方便，直到尝试了Atom，发现真是一款让人上瘾的编辑器。

不仅流畅、简洁，还有非常方便的插件管理以及强大的DIY样式，并且支持Git，对文件的管理非常人性化。

<!-- more -->

## Atom下载

Atom的下载地址（Git Hub）：[Atom](https://github.com/atom/atom/releases)

64位Windows用户下载选择`atom-x64-windows.zip`，下载后解压。`AtomSetup-x64.exe`会很艹地在打开时直接安装到C盘的默认路径。

## Atom界面

打开编辑器左边为询问是否愿意提交个人数据帮助改善，右侧为常规的打开软件后的一些选项

![image-20200406005646356](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406005656.png)

Atom的布局可以拖动窗口来更改，也可以右键标题栏来为上下左右添加空白窗口。

图例为自己随意拖动后的效果。

![image-20200406030218614](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406030221.png)



## Atom配置

### 编辑器自动换行

`settings -> Editor` 勾选 Soft Wrap

![image-20200406014702337](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406014703.png)

当文本超过当前编辑区的窗口大小时，会自动转换到下一行（实际代码并没有换行，仅显示文本进行换行）

如下图，可以根据左边的行数知 第二行的内容算在第一行中

![image-20200406014752946](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406014754.png)

### 缩进指示线

`setting -> Editor` 勾选 Show Indent Guide

![image-20200406014709849](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406014711.png)

效果对比：

![image-20200406012427851](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406012429.png)

![image-20200406012410107](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406012412.png)

### 显示不可见字符

当输入回车、Tab时，用一些字符来表示这些特殊的输入

`setting -> Editor` 勾选 Show Invisibles

![image-20200406014854945](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406014856.png)

效果对比：

![image-20200406012427851](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406012429.png)

![image-20200406012620482](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406012623.png)

另外在`setting -> Editor`中可以设置用于显示的字符

![image-20200406012806293](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406012807.png)

### 添加到右键菜单栏

`setting -> System`，第一个为将Atom添加到打开方式，第二个为右键文件时显示通过Atom打开，第三个为右键菜单栏时通过Atom打开

![image-20200406014950451](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406014952.png)

### 修改快捷键

Atom的快捷键修改真的是简单无脑…并且可以同样的操作去修改插件的快捷键

进入`settings -> Keybindings`，即可看到所有的快捷键以及对应的命令、来源、CSS属性？

![image-20200406024742965](D:\blog\source\_drafts\Atom编辑器尝试.assets\image-20200406024742965.png)

可以在搜索框中按快捷键、命令进行搜索，但注意连接符是减号而不是加号，如搜索快捷键`Ctrl+S`，则输入

```
ctrl-s
```

![image-20200406024952283](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406024954.png)

也可以搜索`save`来查找与save相关的快捷键

![image-20200406025108129](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406025109.png)

若想修改快捷键，只需要如图顺序点击

![image-20200406025223346](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406025226.png)

然后在新打开的文件中的底部，将刚刚复制的信息粘贴，然后修改快捷键，保存即可。

![image-20200406025358311](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406025401.png)

所有自定义的快捷键都可以在这里进行添加、修改、删除、注释等。

## Atom插件

### 前言

注：尽量科学上网，下载源在境外，网速捉鸡

若是刚打开Atom，可以在欢迎界面中选择Install a Package，然后点击Open Installer来进入插件社区

![image-20200406005938736](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406005940.png)

或者在菜单栏的`File -> settings`（快捷键Ctrl+逗号）打开设置，然后选择Install

![image-20200406010249017](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406010251.png)

安装后的插件可以在设置的Packages进行管理，Atom会自动对插件进行大体分类。

点击Disable或Enable来设置是否启动，点击Settings进入插件的设置。

![image-20200406011335793](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406011337.png)

### 简体中文

```
搜索
simplified-Chinese-menu
```

![image-20200406011239540](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406011241.png)

在设置界面可以选择汉化的部分

![image-20200406011651896](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406011653.png)

### 缩略图

```
搜索
minimap
```

![image-20200406030822798](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406030824.png)

![](https://raw.githubusercontent.com/atom-minimap/minimap/master/resources/screenshot.png)

安装后，既可以在编辑处将鼠标放在缩略图上点击齿轮进行一些设置。

![image-20200406031002377](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406031003.png)

也可以进入插件的settings进行详细设置

![image-20200406031126891](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406031128.png)

### 连击特效

一个趣味的插件，当敲代码时会在右上角出现连击提示，并且在代码编辑区会有窗口抖动效果

![activate-power-mode-0 4 0](https://cloud.githubusercontent.com/assets/688415/11615565/10f16456-9c65-11e5-8af4-265f01fc83a0.gif)

![activate-power-mode-combo](https://cloud.githubusercontent.com/assets/10590799/18817237/876c2d84-8321-11e6-8324-f1540604c0bd.gif)

```
搜索
activate-power-mode
```

![image-20200406013637806](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406013639.png)

## 配置C/C++开发环境

### 安装编译器

MinGW下载地址：[MinGW](https://osdn.net/projects/MinGW/releases/)

在中间点击图标下载windows版

![image-20200406015857057](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406015858.png)

下载后打开安装，一直下一步最后安装完成后点击Continue。

在打开的界面中，勾选`MinGW32-gcc-g++-bin`，然后点击菜单栏的`Installation ->  Apply Changes `安装gcc

安装完成后点击Close关闭即可。

![image-20200406021018449](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406021026.png)

若不小心安装后关掉了或者没有打开安装编译器的界面，可以在MinGW的安装目录中打开bin文件夹下的

`MinGW-get.exe`

![image-20200406020903397](D:\blog\source\_drafts\Atom编辑器尝试.assets\image-20200406020903397.png)

### 报错问题

若在安装时出现`输入错误: 没有文件扩展“.js”的脚本引擎`的报错，则打开运行，输入`regedit`

![image-20200406020051445](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406020052.png)

在路径`HKEY_CLASSES_ROOT\.js`下，更改默认值为`JSFile`

![image-20200406020303194](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406020304.png)

### 添加环境变量

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

![image-20200406021833581](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406021835.png)

### 安装插件

搜索插件`linter-gcc`并安装，安装后会提示安装其依赖插件`linter`与`linter-ui`，一同安装即可。

![image-20200406023528088](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406225233.png)

安装后进入`linter-gcc`的设置，勾选 `Lint on-the-fly`，实现当停止编写代码时，自动进行编译，若有错则会提示错误信息 。

![image-20200406024152098](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406024353.png)

![image-20200406024342794](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406024355.png)

linter还能实现在下方即时弹出错误信息

![image-20200406025839501](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406025841.png)

搜索插件`gcc-make-run`，随后按`F6`即可运行C语言文件，快捷键可以修改，参考[修改快捷键](#修改快捷键)

![image-20200406024045860](https://gitee.com/lluuiq/blog_img/raw/master/img/20200406024608.png)