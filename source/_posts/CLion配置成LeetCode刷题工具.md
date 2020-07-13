---
title: CLion配置成LeetCode做题工具
comments: true
toc: true
top: false

categories:
- [笔记]
tags: [CLion]

date: 2020-04-07 13:21:56
---

LeetCode自带的编译感觉并不好用，而且代码补全与提示是收费，故使用本地IDE作为LeetCode做题的工具。

<!-- more -->

## 前言

关于CLion的C/C++环境配置在另一篇文章里有说明。

PyCharm、intellij IDEA等JetBrains公司的IDE都可以使用相同的配置流程。 

## 安装插件

leetcode-editor：

打开CLion设置，在Plugins搜索leetcode即可找到插件：

![image-20200407133534599](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407133543.png)

若网速过慢，或无法下载，也可以下载压缩包然后加载本地插件来安装。

在Git Hub的Releases下载插件压缩包 https://github.com/shuzijun/leetcode-editor

在JetBrains的插件库下载压缩包 https://plugins.jetbrains.com/plugin/12132-leetcode-editor

下载完成后在Plugins的上方点击齿轮处，选择Install Plugin from Disk，然后选择下载的压缩包路径安装即可。

![image-20200407133724459](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407133737.png)

## 配置插件

leetcode editor [中文文档](https://github.com/shuzijun/leetcode-editor/blob/master/README_ZH.md)

安装好插件后，在IDE的右方侧边栏的下方，可以打开leetcode editor

![image-20200407135437696](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407135439.png)

打开后先点击齿轮进入配置

![image-20200407135502970](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407135504.png)

也可以通过 `settings -> Tools ->leetcode plugin`进入设置。

![image-20200407135725899](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407135727.png)

URL选择境内还是境外的leetcode

- Code Type选择C语言（若是其他环境的IDE选择对应语言）

- LoginName输入登陆的用户名（邮箱）和密码

- TempFilePath为存放代码的位置，注：选择路径后，会创建`leetcode\editor\cn`目录来将代码存放在cn，例如我选择路径`D:\code\`，则会生成路径``D:\code\leetcode\editor\cn`，然后将题目代码放在cn文件夹下

- LevelColour为划分题目难度的颜色设置，默认即可，也可以修改。

- CodeFileName为创建题目代码时的文件名，默认为`[题目标号]题目名.c`，如：`[1]两数之和.c`

- CodeTemplate为代码编辑处的默认模板，先是题目描述，然后是题目给的默认代码

  两部分都可以根据下方给出的参数来修改模板

---

**注：若需要Debug，则先创建一个project，然后将TempFilePath的路径改为该项目。推荐设置项目名为leetcode，然后将TempFilePath设置为项目的父级文件夹，这样可以少一层插件创建的leetcode文件夹**

例如：我在D:/code下创建一个project名为leetcode，然后插件的路径改为D:/code，则生成路径为下图：

![image-20200407141639456](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407141640.png)

但如果我的项目名不是leetcode，然后插件路径设置为D:/code/项目名，则效果为下图：

![image-20200407142014111](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407142015.png)

![image-20200407142039705](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407142041.png)

可以看到插件自己生成了leetcode文件夹来当做父级目录

---

回到正题，配置完成后保存，然后点击第一个图标登录

![image-20200407140451560](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407140500.png)

若有提示使用cookie登录，则进入LeetCode，按F12点击加载的文件，找到cookie复制粘贴然后login即可

![image-20200407140759524](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407140801.png)

登陆成功后便会刷新出题目，可以浏览全部题目

![image-20200407140830680](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407140956.png)

![image-20200407140951578](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407140954.png)

也可以根据难度、做题状态、以及一些活动来获取题目

![image-20200407140932410](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407141000.png)

## 配置Debug

因leetcode给的默认代码为一个类或一个方法，因此需要自己编写main()函数来调用函数，实现Debug。

### 自定义代码块

详细参考：[Pycharm自定义模板](https://lluuiq.com/post/202003300841/?t=1586250575670) 

打开设置，搜索`Live Templates`，进入自定义代码块配置，选择C/C++，点击+号添加模块，这里我已经添加过一个`main`和一个`lmain`，默认是没有的。

![image-20200407171040815](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407171114.png)

填入缩写、描述以及代码块，下方的Applicable选择C。

![image-20200407171145352](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407171147.png)

这里的代码块在调用后，会按\$No\$（题号）、\$FILE\$（题目名）、\$CODE\$（代码块）的顺序进行填写，填写完一项后按TAB切换到下一项，参数的名称是自定义的 。

关于`#include "editor/cn/[$No$]$FILE$.c"`，调用目标.c文件，其中文件名应与配置插件时的自定义名称的格式相同。

```C
#include "stdio.h"
#include "editor/cn/[$No$]$FILE$.c"

int main() {
    $CODE$
    return 0;
}
```

这样当以后想对一道题进行Debug时，只需要新建一个.c文件，然后输入lmain调用该代码块，填写题号和题目后就可以编写对应代码然后调用题目中的函数了，Java、Python应该是调用类 。接下来就是解决C语言一个项目只能有一个main()函数的问题，需要修改CMakeLists。

### 实现多个main()函数文件

添加一个`add_executable`，内容可以看到前面为一个项目名，后方为main函数的文件

这个项目名可以不存在，但需要与其他项目名不同，故可以在项目名后方加上数字来表示第几题即可，.c文件的名字自定义就行。这样以后想Debug时只需要在项目中新建一个.c文件，生成自定义代码块然后调用题目代码，编译前添加到CMakeLists即可。

![image-20200407170824491](https://gitee.com/lluuiq/blog_img/raw/master/img/20200407170825.png)