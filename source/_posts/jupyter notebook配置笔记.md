---
title: jupyter notebook配置笔记
comments: true
toc: true
top: false
mathjax: false
categories:
  - - 笔记
tags:
  - jupyter
  - Anaconda3
date: 2020-07-04 09:10:06
---

记录下jupyter notebook的配置。

<!-- more -->

## 修改快捷键

在Help中可以查看快捷键（上）与修改快捷键（下）

![image-20200704111937518](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704111937518.png)

默认的就挺好用，但后面有安装一个autopep8插件，用来格式化代码，个人习惯的快捷键`Ctrl-Shift-F`与默认的查看命令按键冲突

![image-20200704111926335](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704111926335.png)

故把`Ctrl-Shift-F`从中删除，用于后面的格式化代码。

## 插件拓展库

```shell
pip install jupyter_contrib_nbextensions
pip install jupyter_nbextensions_configurator
```

```shell
jupyter nbextensions_configurator install --user
jupyter nbextensions_configurator enable --user
```

安装完成后，即可在jupyter的页面看到 Nbextensions 选项卡（或许需要重新打开jupyter）

![image-20200704061750041](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704061750041.png)

使用filter筛选插件时全小写，大写识别不出来

### Snippets Menu 

自定义代码模块

![image-20200704062022806](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704062022806.png)

可以在对应的库中选择Setup（基本导入），或者根据要求生成代码。

My favorites 为自定义的代码块，在 Nbextensions 中选择Snippets Menu来设置

![image-20200704062214712](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704062214712.png)

json内容如下

```json
{
  "name" : "My favorites(自定义名称)",
  "sub-menu" : [
      {
          "name" : "代码块名称",
          "snippet" : ["import numpy as np",
            "import pandas as pd",
            "import tensorflow as tf",
            "import matplotlib.pyplot as plt",
            "%matplotlib inline",
            " ",
            "plt.rcParams['font.sans-serif']=['SimHei'] # 显示中文标签",
            "plt.rcParams['axes.unicode_minus']=False # 显示负号"]
      },
      {
          "name" : "第二个代码块",
          "snippet" : [
          		其余内容同上
          ]
      }
  ]
}
```

json格式，注意逗号。

### ExecuteTime

可以在cell执行完毕后显示运行使用的时间与执行的时间

![image-20200704062615009](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704062615009.png)

### Notify

可以在需要长时间运行代码时使用，运行完毕后提醒自己。

### Table of Contents

markdown文本开启目录

![image-20200704062824767](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704062824767.png)

### Variable Inspector

显示所有变量信息

![image-20200704062859359](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704062859359.png)

### Autopep8

格式化代码工具，点击即可格式化cell内的代码。

可以在设置界面更改快捷键。

![image-20200704111529135](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704111529135.png)

<br>

我因为搭建了 tensorflow虚拟环境，所以报了以下错，需要安装autopep8包，安装完成后即可使用。

![image-20200704111126098](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704111126098.png)

切换到当前虚拟环境然后执行 

```shell
conda install autopep8
```

或者使用 `Anaconda Navigator`来安装

![image-20200704111302922](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704111302922.png)

### Collapsible Headings

按标题可以折叠markdown以及以下的代码，方便浏览代码。

### Freeze

可以冻结一个cell，使其不能运行与删除等。

免得误操作。

### Gist-it

可以将ipython代码添加到github的gist仓库，需要在红框位置添加密钥

![image-20200704110144017](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704110144017.png)

密钥的获得方式：

进入[github.com/settings/tokens](https://github.com/settings/tokens)，点击`Generate new token` 生成一个密钥

![image-20200704110241789](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704110241789.png)

Note类似名称，随意写，能区分是用来干什么的就行

![image-20200704110324350](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704110324350.png)

然后在选项中勾选gist，最后点击 `Generate token`即可。

![image-20200704110333029](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704110333029.png)

将生成的密钥复制，并粘贴进之前红框的位置。点击代码文件页面的github的图标。

![image-20200704110426829](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704110426829.png)

![image-20200704110637599](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704110637599.png)

若没有上传过则 Gist ID 是空的，会新建一个Gist仓库。

<br>

有个缺点就是修改不方便，因为上传的是ipython，所以只能打开ipython进行编辑再上传来更新，直接在gist上编辑是类似以下格式

![image-20200704110902327](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200704110902327.png)

## 修改样式

jupyterthemes的主题配置简单，但是和一些拓展有些bug而且并不能完全符合自己的喜好。

故使用自定义CSS的方法来配置。同路径下有个custom.js可以配置js脚本

配置文件路径： `C:\Users\用户名\.jupyter\custom\custom.css`

<br>

关于修改方法：建议打开jupyter页面，然后按F12，在这里测试样式，然后最后再写进代码里保存，刷新页面查看。

关于单元格字体的样式，修改对象：

![image-20200704073730823](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704073730823.png)![image-20200704073737931](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704073737931.png)

关于代码区域的字体样式，修改对象：

![image-20200704085644088](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704085644088.png)

定义了变量来存储值，修改只需要修改`:root`里面的值即可，详细的根据自己自定义的样式更改。

分享一下自己的设置，直接添加到最后面即可。

```css
/******** DIY ********/
/* 定义变量 */
:root {
  /* 不透明度 */
  --opacity: 0.9;
  /* 代码区域的字体样式 */
  --code_font_size: 16;
  --code_font_family: consolas;
  /* 单元格字体样式 */
  --cell_font_size: 14;
  --cell_font_family: consolas;
  /* 代码区行距  */
  --line_height: 1.4;
  /* 背景图片url */
  --background_image_url: url(https://gitee.com/lluuiq/blog_img/raw/master/img/932b3092a3fccecb49bb7b7880c3f24a9ed76d83.jpg@1320w_742h.png);
  /* 网页背景颜色 */
  --bg_color: gray;
  /* 笔记本的宽度 （默认居中）*/
  --width: 80%;
}

/* cell单元格区域 */
div.code_cell {
  /* 字体样式 */
  font-size: calc(var(--cell_font_size) * 1px);
  font-family: var(--code_font_family);
  /* 行距 */
  line-height: calc(var(--line_height) * 1em);
}

/* 代码区域 */
.CodeMirror {
  /* 字体样式 */
  font-size: calc(var(--code_font_size) * 1px);
  font-family: var(--code_font_family);
}

/* 注释 */
.cm-comment {
  /* 去掉斜体*/
  font-style: normal !important;
  /* 样式与代码区一样 */
  font-family: var(--code_font_family);
  font-size: var(--code_font_size);
}

/* 目录 */
#toc-wrapper {
  /* 背景颜色 */
  background-color: #ffffff;
  /* 不透明度 */
  opacity: var(--opacity);
}

/* 变量信息区域 */
.varInspector-float-wrapper {
  opacity: var(--opacity) !important;
}
/* 笔记本区域 */
div#notebook {
  /* 不透明度 */
  opacity: var(--opacity);
  /* 宽度缩小 */
  width: var(--width);
}
/* 笔记本区域的边框角弧度 */
#notebook-container {
  border-radius: 10px;
}

/* 页面 */
#site {
  /* 背景图片 ，与背景颜色二选一 */
  background: var(--background_image_url) no-repeat fixed;
  /* 背景颜色 */
  /* background-color: var(--bg_color); */
  background-size: cover;
}
```

效果图：

![image-20200704090834597](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200704090834597.png)