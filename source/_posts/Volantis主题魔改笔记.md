---
title: Volantis主题魔改笔记
date: 2020-03-17 12:29:46 
comments: true
toc: true
top: false

categories: 
- [笔记,博客]
tags: [博客,hexo]
---

主题首页：[Volantis](https://volantis.js.org/)

记录一些DIY博客的过程

<!-- more -->

## 主题文件目录

在主题的根目录下。

layout为页面、卡片、各部位的布局代码

source存放css、js、字体、图片等代码与资源

_config.yml为主题配置文件

![mark](http://blogimg.wa2000.cn/blog/20200317/hSKFk5ikk9JB.png?imageslim)

## 顶部导航栏

设置顶部导航栏始终显示。

打开source/css/_layout/navbar.styl

找到最下面的代码，将其注释

![mark](http://blogimg.wa2000.cn/blog/20200317/BLeQEolGaKwF.png?imageslim)

```stylus
// .cover-wrapper
//   .l_header
//     trans(0.5s)
//     transform: translateY(-2 * $navbar-height)
//     &.show
//       transform: translateY(0)
```

## 搜索栏

修改搜索结果中的输入内容的上边距，使内容显示在合适位置

原来的样式：

![mark](http://blogimg.wa2000.cn/blog/20200317/MzNiXRI17xKD.png?imageslim)

修改后：

![mark](http://blogimg.wa2000.cn/blog/20200317/88km2cPb1WHm.png?imageslim)

打开source/css\_layout/search.styl

使用搜索功能搜索关键词`input`

修改margin，将`$gap`改为`5px`

```stylus
#u-search-modal-input
	margin: 5px 50px
```

## 修改卡片的内外边距

打开_config.yml

找到`gap`的设置，添加base值，大小为要设置的内外边距

![mark](http://blogimg.wa2000.cn/blog/20200317/D0yaYQXcnYD9.png?imageslim)

```yml
base: 10px
```

该方法是同时修改卡片之间的距离以及卡片内容与卡片边框之间的距离。

若要分开修改需要到css文件逐一修改，可以用该方法添加一个新的变量来传参。

例如：

在gap中添加一个变量，变量名自定义，这里用test示例，后面的大小为要设置的大小。

```yml
test: 10px
```

接着打开source/css/_defines/layout.styl，找到gap的设置

![mark](http://blogimg.wa2000.cn/blog/20200317/OJ1SN2kH9f4E.png?imageslim)

添加自定义的变量

![mark](http://blogimg.wa2000.cn/blog/20200317/1GsC3rODl1Y6.png?imageslim)

```stylus
$test = convert(hexo-config('style.gap.test')) || 16px
```

$test为CSS设置中的变量名，`style.gap.test`中的test为在_config.yml中设置的变量名，||后面为默认值

设置完成后，在对应的CSS设置中仅需要将间距大小改为`$test`，就会使用设置中test的值

## 封面界面去掉搜索

效果如图

![mark](http://blogimg.wa2000.cn/blog/20200317/BjXFPLvKIWLT.png?imageslim)

打开layout/_cover/index.ejs

找到如图所示代码，将其注释

![mark](http://blogimg.wa2000.cn/blog/20200317/EKabzjWjCJ1Y.png?imageslim)

## 添加QQ在线联系

打开_config.yml，搜索social，找到社交功能设置部分

![image-20200317161443443](C:%5CUsers%5C84452%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200317161443443.png)

添加内容如下

```yml
- icon: fab fa-qq
  url: http://wpa.qq.com/msgrd?v=3&uin=【你的QQ号】&site=qq&menu=yes
```

第一次点击会提示未开通，到提示网站登入一次即可。

## 将侧边栏移动到左边

打开layout文件夹，对以下文件统一修改

![mark](http://blogimg.wa2000.cn/blog/20200317/qeYmT3crtzeE.png?imageslim)

打开一文件后，搜索代码

```ejs
<%- partial('_partial/side') %>
```

将该行代码复制到第一行代码`<%- partial('_pre') %>`的下方，然后将原来位置的代码注释（方便以后若需要的话改回），示例：

![mark](http://blogimg.wa2000.cn/blog/20200317/NmjNwJwr1Pgg.png?imageslim)

然后修改CSS文件，

打开source/css/_layout/main.styl

搜索`.l_main`，找到`padding-right`，将right改为left，使原本的右边距变为左边距

![mark](http://blogimg.wa2000.cn/blog/20200317/SlAHUzX3EiID.png?imageslim)

修改后为

![mark](http://blogimg.wa2000.cn/blog/20200317/CedRTRknjOda.png?imageslim)