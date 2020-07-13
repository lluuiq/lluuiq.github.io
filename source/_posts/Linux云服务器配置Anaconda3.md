---
title: Linux云服务器配置Anaconda3
comments: true
toc: true
top: false
mathjax: false
categories:
  - - 笔记
tags:
  - Anaconda3
date: 2020-07-03 04:55:02
---

记录一下Linux云服务器上搭建Anaconda3并进行配置的过程，开启远程访问。

<!--more-->

## 说明

Linux服务器：Centos7

Anaconda3版本：2020.02-Linux-x86_64



[Anaconda3下载](https://www.anaconda.com/products/individual)

## 下载Anaconda3并上传到服务器

在[说明](# 说明)中的下载地址里，找到Linux版本。

（选择适合自己的安装包，我这里Linux是**x86_64**）

![image-20200630170224375](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630170224375.png)



将下载的安装包上传到服务器（Xshell、FinalShell等软件）

![image-20200630170537967](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630170537967.png)

## 安装Anaconda3

```shell
bash Anaconda3-2020.02-Linux-x86_64.sh
```

安装包的名字对应自己下载的版本即可。

<br>

![image-20200630170639627](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630170639627.png)

回车

<br>

![image-20200630170718992](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630170718992.png)

疯狂回车

<br>

![image-20200630170757862](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630170757862.png)

输入yes

<br>

![image-20200630171034378](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630171034378.png)

按回车安装到当前目录 `/root/anaconda3`

<br>

![image-20200630171800088](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630171800088.png)

输入yes

---

最后安装完成后，输入`ipython`即可启动ipython

![image-20200630174756536](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630174756536.png)

输入`exit()`或使用`ctrl+z`退出

## 配置 `/root/.bashrc` 文件

### 使用Anaconda3的python3.7

Anaconda3附带的是python3.7，在安装好Anaconda3后，输入python还是linux自带的python2。故对版本进行配置。

添加如下代码（若安装路径不一样修改为自己的路径 ）

```shell
export PATH="/root/anaconda3/bin:$PATH"
```

### 是否显示`(base)`

添加Anaconda3的python后会在指令行前面会出现`(base)`

![image-20200630172947611](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630172947611.png)

表示启用了conda。如果不想显示这个`(base)`的话，在`/root/.bashrc`中添加

```shell
conda deactivate
```

### 配置alias

加入下方代码

```shell
alias python2="/usr/bin/python2.7" 
```

python2为自定义的别名，可以使用py2或者其余自己喜欢的别名替代

### 更新.bashrc

每次修改.bashrc后都要输入`source ~/.bashrc` 进行更新才能生效。

## 远程访问jupyter

打开ipython，然后按顺序输入以下代码

```python
from notebook.auth import passwd
```

```python
passwd()
```

然后输入一个登陆jupyter的密码，再输入一次确认。

输入后，会输出一个跟密钥一样的字符串

![image-20200630175648701](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630175648701.png)

然后退出ipython。到anaconda3的安装目录下的`etc/jupyter`，执行

```shell
jupyter notebook --generate-config
```

![image-20200630175919302](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630175919302.png)

会输入信息显示配置文件的位置，编辑`/root/.jupyter/jupyter_notebook_config.py`

最后一行如果是root用户就加上，否则不用加。

```python
c.NotebookApp.ip = '*' # 设置使用此服务器的ip进行访问
c.NotebookApp.password = u'sha1:XXXX' # 输入之前生成的key
c.NotebookApp.open_browser = False # 关闭启动jupyter时打开浏览器
c.NotebookApp.port = XXXX # 设置使用的端口
c.NotebookApp.enable_mathjax = True # 启用 MathJax
c.NotebookApp.notebook_dir = '你的目录' #设置共享目录
c.NotebookApp.allow_remote_access = True
c.NotebookApp.allow_root = True # 允许在root用户下运行
```

效果图：

![image-20200630182338967](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630182338967.png)

<br>

接下来到服务器商那里放行设置的端口，如果有安装宝塔，宝塔上也要放行。

![image-20200630182248653](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630182248653.png)

![image-20200630182351764](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630182351764.png)

<br>

然后输入`jupyter notebook`，开启jupyter

![image-20200630182143408](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630182143408.png)

<br>

其余设备上打开浏览器，输入 `IP:port` 即可访问，如 `192.168.0.123:8888`

输入密码即可进入。

![image-20200630182122207](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630182122207.png)

<br>

修改密码方法为输入 `jupyter notebook password`，然后像设置密码一样输入密码，最后会生成json配置文件。

![image-20200630183218003](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630183218003.png)

然后打开生成的json文件，在.py配置文件中使用新生成的key

![image-20200630183536102](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200630183536102.png)



json文件的优先级大于py，所以会覆盖。

