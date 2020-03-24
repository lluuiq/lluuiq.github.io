---
title: hexo写作简易化 
date: 2020-02-22 00:37:41 
comments: true
toc: true
top: false

categories: 
- [笔记,博客]
tags: [hexo,博客]
---
hexo写文章不像WordPress与Typecho那样拥有后台管理系统，每次都要新通过指令新建文章（若本地创建的话没有配置的front-matter），并且写完后还要清除缓存，生成页面，然后部署。
而且hexo上传到网上的文章要考虑一个图床的问题，图片若不是url链接是无法在网上被访问到的。
hexo也缺少一个方便的、随时随地修改文章的后台管理。
于是写篇文章记录我简化写作的的过程。
<!-- more -->

## 使用HexoEditor进行写作

点击进入项目地址：[HexoEditor](https://github.com/zhuzhuyule/HexoEditor)
HexoEditor的优点：
    1. 读取hexo的post模板生成文章
        2. 可以在软件上清除缓存、生成页面、推送，也可以直接一键部署
        3. 支持图床链接
HexoEditor的缺点：
        1. 没有文件目录
        2. 没有文章目录
        3. 个人遇到了腾讯云无法配置图床以及七牛云图床链接缺少一个'/'的问题 

### 安装：

到HexoEditor的github地址，下载压缩包解压即可。
![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023219.png)

## 使用Typora进行写作

Typora[官方网站](https://typora.io/)
Typora具有写作即样式的效果，使用markdown的语法后会直接将该部分文字转为markdown的样子，真·所见即所得。
这是刚写完的一句话
![mark](http://blogimg.wa2000.cn/blog/20200222/4ubdJFf3jImV.png?imageslim)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023224.png)

当光标没有聚焦在该部分时，就会自动转为markdown样式，当光标再次回来时又会变成文本。
当然，因为Typora是一个markdown写作软件，不是专为hexo订制，所以写完后还是要通过命令行指令进行部署。

## 关于图床

有很多能存储图床的服务商，有域名的话可以选择自己域名的服务商提供的空间存储，也可以使用七牛云（个人目前使用），免费的图床有sm.ms。下面以个人使用的七牛云为例优化写作时的图片插入问题。
### ~~使用HexoEditor~~（舍弃）

因七牛云的链接会缺少一个'/'符号，导致要手动添加，腾讯云又无法配置，故不推荐使用，若用sm.ms作为图床的话可以使用（个人没有sm.ms，所以没有测试是否存在问题)

---

HexoEditor仅支持截图，不支持复制图片。
HexoEditor自带上传然后转化功能。只需要填好该三项，存储空间与域名会自动显示出，然后自行选择即可。
进入七牛云的密钥管理（HexoEditor右键空白处有快速打开能进入七牛云主页）。
![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023222.png)
可以看到对应的密钥，隐藏的话点击显示即可复制。
![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023223.png)
AK粘贴到AccessKey，SK粘贴到SecretKey，就完成配置了。
用法举例：
当截图后，会在本地保存图片，如下图所示，

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023221.png)
右键空白处，点击上传 七牛，链接会自动转化为七牛云存储空间里的URL，并且是整篇文章的图片全部转化。

## 使用Mpic

[Mpic官网](http://mpic.lzhaofu.cn/)
这是我一直在用的类似小工具一样的东西，支持截图（看更新日志说是QQ截图，不知其他截图是否支持）、复制、拖拽均可自动上传并复制URL，还可以查看上传目录并且复制链接或者删除（但没有预览图，可以复制URL地址粘贴到网址栏然后查看）
![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023226.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023225.png)

配置方法参考上方HexoEditor的配置，但域名、空间名需要自己填写。

# 使用Hexo-admin实现后台管理

hexo-admin有个缺点是只能在开启`hexo server`时才能进行管理。

## 安装

[hexo-admin官网](https://jaredforsyth.com/hexo-admin/)
在下方可以看到安装流程

若已经安装过hexo和创建好博客根目录了，则直接安装插件即可。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023229.png)

在博客根目录内右键空白处，点击`Git Bash Here`

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023227.png)

```
npm install --save hexo-admin
hexo server -d
```
然后打开浏览器输入
```
http://localhost:4000/admin/
```
即可进入后台管理。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023228.png)

Posts为文章列表
Pages管理hexo的页面
About是关于插件与hexo的信息
Deploy可以部署一些脚本
左边为写作区，右边为预览区，右上角有删除、文章设置与发布（这个发布仅仅部署在本地，未推送）。
文章会自动保存，同时也支持复制图片URL（但是我用的Mpic,hexo-admin的图片老是裂开）
![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023230.png)
点击发布后，会变成Unpublish，再次点击会取消在本地的部署。并且发布后，在这里编辑的内容可以在本地服务器上事实预览。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023231.png)

![mark](http://blogimg.wa2000.cn/blog/20200222/2vcs0AaFPDT8.png?imageslim)

## 为后台添加密码
可以设置是否需要帐号密码进入后台。（设置后每次hexo clean后登陆都要帐号密码）
点击Settings，点击如图所示的链接
![mark](http://blogimg.wa2000.cn/blog/20200222/I9MedKH58PPm.png?imageslim)
然后填好帐号与密码，Secret是加密用的，内容不用改。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023233.png)
最下面会生成一段代码，将这些拷贝到网站根目录下的配置文件`_config.yml`，然后保存即可。

## 实现一键部署

按照写脚本部署的方法windows不知道是因为权限问题还是不支持的问题，部署一直报错，查阅github上的issue后找到了作者给出的解决办法。
issue链接：https://github.com/jaredly/hexo-admin/issues/94
直接打开根目录下的node_modules文件夹，再打开hexo-admin文件夹，编辑器打开deploy.js，
将

```
var proc = spawn(command, [message], {detached: true});
```
改为（把原来的注释掉，换成下面这行代码即可）
```
var proc = spawn((process.platform === "win32" ? "hexo.cmd" : "hexo"), ['d', '-g']);
```
结果如图：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023232.png)

改完后要通过在网站根目录打开Git Bash 然后输入`hexo clean`清除缓存，之后输入'hexo g'重新生成静态页面，启动本地服务器即可。
回到hexo admin的部署界面，直接点击Deploy，效果如下
![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023234.png)
可以看到 Std Output里的内容说明部署成功，下方的警告是指windows与linux的换行符问题，可以无视。