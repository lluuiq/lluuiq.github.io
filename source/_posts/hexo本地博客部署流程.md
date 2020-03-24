---
title: hexo本地博客部署流程
date: 2020-02-19 21:00:39
urlname: hexo博客部署流程
comments: true
toc: true
top: false
categories: 
- [笔记,博客]
tags: [博客,github,hexo]
---

最开始用hexo部署过博客，有记录当时的部署过程，现在更新一下，后来又尝试了wordpress与typecho，但个人比较喜欢修改主题样式，感觉wordpress与typecho的封装性太强，于是又回来hexo了。

用hexo部署过博客，有记录当时的部署过程，现在更新一下，后来又尝试了wordpress与typecho，但个人比较喜欢修改主题样式，感觉wordpress与typecho的封装性太强，于是又回来hexo了。

一年前用hexo部署过博客，由于其他事情导致长时间未使用，后来又尝试了wordpress与typecho，但个人比较喜欢修改主题样式，感觉wordpress与typecho的封装性太强，于是又回来继续使用hexo。记录自己重新部署hexo博客的过程，更新以前的部署笔记，故有的时间显示为2019年，但流程都是一样的。

这篇笔记里可以看到	

1. [博客本地部署过程](#博客本地部署过程)
2. [静态页面部署到github过程](#博客部署到github过程)
3. [hexo修改配置](#hexo修改配置)
4. [为博客绑定域名](#为博客绑定域名)
5. [将博客源代码保存到github](#将博客源代码保存到github)

<!-- more -->

---

# 博客本地部署过程

需要安装的东西：git、Node.js、hexo。

其中git安装完成后的Git Bash，其作用与系统自带的CMD命令行相同，系统中的CMD命令同样可以在Git Bash中完成。

链接：

- [git官方下载地址](https://git-scm.com/downloads)

- [git淘宝镜像下载地址](https://npm.taobao.org/mirrors/git-for-windows/)

- [Node.js官网下载地址](https://nodejs.org/en/)

hexo使用命令安装。

[hexo官方文档](https://hexo.io/zh-cn/docs/)里面有关于hexo的各种使用方法，包括各个指令、文件的说明、如何更改网站的一些信息等等。

---

## hexo常用指令：

`hexo new "title"` 新建文章(md文件)，title为文章的标题
`hexo new page "pagename"` 新建网页，pagename为网页的名称
`hexo clean` 清除部署的緩存
`hexo n == hexo new` 新建一篇文章
`hexo g == hexo generate` 生成静态页面
`hexo s == hexo server` 本地部署，可预览网站，默认端口为4000，浏览器输入`localhost:4000`即可进入网站进行预览，回到git-bash按`ctrl+c`退出预览(退出后`localhost:4000`失效)
`hexo d == hexo deploy` 将网站部署到GitHub
`hexo g -d` 生成页面并部署到GitHub
`hexo g -s` 生成页面并本地部署进行预览

---

## 安装git：

本文章书写日期时最新版本为2.22.0版本

因版本可能不同，因此安装过程中的组件选择可能会有所差异，基本默认选项即可

下载完成后进入安装界面 (注:以下安装的选项请以实际自身需求为准，仅供参考):

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030720.png)

选择需要安装的组件。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030722.png)

选择git的默认编辑器:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030724.png)

配置环境变量选项,推荐默认第二项:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030721.png)

选择https传输协议 默认即可:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030723.png)

选择git的换行方式 请根据自身需求更改:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030725.png)

设置git命令行的样式:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030726.png)

设置选项：1.是否允许文件缓存 2.是否允许git许可证管理，默认勾选：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030740.png)

是否参与新的测试,貌似是会使git更快，但还不稳定:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030727.png)

install 安装即可:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030728.png)

git安装完成后，需要进行配置，在git安装目录或菜单栏中找到git-bash，打开后如图

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030737.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030729.png)

输入如下，其中" "中的your name 和your email为你的Git Hub用户名(非昵称)与邮箱

```
git config --global user.name "your name"
git config --global user.email "your email"
```

并可通过以下命令查询用户名与邮箱

```
git config user.name
git config user.email
```

结果如下

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030731.png)

## 安装Node.js：

该文章书写时，版本为10.16.0

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030730.png)

安装界面:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030732.png)

选择安装模式,我选择了第四个，next即可:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030733.png)

以下过程命令行既可使用windows的cmd，也可以使用git安装过程中的 git-bash进行操作

命令行中输入`node -v`可查看node的版本 ,输入 `npm -v`查看npm包的版本

```
node -v
npm -v
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030735.png)

因为npm为国外源，下载速度感人，故使用cnpm使下载指向国内源。

使用淘宝镜像下载 cnpm:

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

下载完后查看cnpm版本

```
cnpm -v
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030734.png)

查询成功则证明安装完成。

## 安装hexo：

使用cnpm下载hexo,用hexo -v查看hexo的版本:

```
cnpm install -g hexo-cli
hexo -v
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030736.png)

## hexo部署博客：

在我的电脑中创建文件夹用于存储博客网站，即网站的站点。文件夹名称自定义，我使用blog,目录为D:\blog。打开blog文件夹，右键空白处点击Git Bash Here在该目录下打开Git Bash(或者用CMD切换到该目录也行)。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030738.png)

输入`cnpm install hexo --save`安装组件。

```
cnpm install hexo --save
```

输入`hexo init`进行初始化，等待时间较长，约几分钟。

```
hexo init
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030741.png)

**注**：若blog文件夹非空，则会报错:

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030742.png)

使用`hexo s` 在本地启动博客

```
hexo s
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030739.png)

如图所示显示本地部署成功

打开网页，地址栏输入`http://localhost:4000`即可从本地进入博客

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030746.png)

目录内的各个文件的作用参考[官方文档](https://hexo.io/zh-cn/docs/setup)

# 静态页面部署到github过程

## 在github上创建静态网站的存储库：

通过`Ctrl+C`停止服务

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030744.png)

登陆自己的Git Hub [点击进入登陆界面](https://github.com/login)

登陆成功后，网页右上角个人头像旁边，点击 + 号 选择New repository创建一个新的仓库

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030743.png)

输入的信息如下，其中 Repository name内容必须是 github的用户名，而不是昵称。点击Create repository创建项目。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030745.png)

创建成功后，界面如图，复制https的链接。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030748.png)

回到git-bash 使用cnpm安装git部署插件，插件名为:hexo-deployer-git

```
cnpm install --save hexo-deployer-git
```

安装过程中若有警告可以忽略

## 修改 _config.yml 文件：

打开网站目录的 _config.yml

移动到最低端，在deploy:后面写入内容

```
  type: git
  repo: 刚刚复制的https链接
  branch: master
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030747.png)

## 推送到github page：

修改完成后，保存文件，在Git Bash中输入

```
hexo d
```

即可将本地的网站服务器渲染出的静态页面上传到github。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030809.png)

该过程可能需要输入github和coding的用户名和密码，若Git Hub配置过SSH则不需要输入。

如果有报错，检查之前的配置是否有误。

```
git config --global user.name "your name"
git config --global user.email "your email"
```

配置语句是否正确 your name为用户名(非昵称)

推送完成后，再次进入仓库，即可看到上传完成的静态网页。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030750.png)

并且可以通过 `你的用户名.github.io` 来进入网站，此时网站已经部署到github page，其他人也可以通过该地址访问你的网站。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030751.png)

`hexo s`指令仅启动本地服务，修改后只能通过localhost:4000来进行访问，此时没有推送页面到github。想要推送到github生成页面的话，需要通过`hexo d`进行推送。推送前输入指令`hexo clean`清除缓存，然后再输入`hexo g`重新生成静态页面，然后推送即可。

# hexo修改配置

[官方文档](https://hexo.io/zh-cn/docs/configuration)里有基本的配置文件内容说明，例如修改博主名称、网站名称、副标题、描述等等。

## 永久链接：

打开博客目录下的配置文件_config.yml，按`Ctrl+F`搜索 URL

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030800.png)

url内容不用改，修改permalink内容

其意思为：修改一篇文章的url

默认的设置为将一篇文章的创建日期+title作为永久链接，但这样并不美观，并且在分享链接时因为编码问题中文会被转码造成如下结果

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030749.png)

链接的格式为 你的域名/permalink内容，

比如我修改后的`post/:year:month:day:hour:minute/`

会将创建文件时的年月日时分作为永久链接，避免了分享中文时的乱码。

加一个post是为了将文章统一放在一个文件夹中，在生成静态网页时，会生成一个post文件夹，里面存放生成的文章。还有其余的样式，在官方文档的永久链接中有说明。

还有一种改法是使用`:urlname`，然后在文档的头信息中给urlname参数，让该参数的值为永久链接，但同样避免不了中文转码的问题，我个人就使用日期作为永久链接了。但这样其实有个问题就是以后管理文档时，post文件夹内显示的都是日期数字，不能直观的看到文章标题。

## 修改默认文章模板：

打开站点目录下的`scaffolds`文件夹，打开`post.md`

该markdown文档的内容会在生成一个markdown文档后自动添加进去。

```
---
title: {{ title }} 
date: {{ date }} 
comments: true
toc: true
top: false

# 若使用urlname作为永久链接则添加该项
urlname:

categories: 
- [父类,子类]
- 同级分类
tags: [标签1,标签2]
---
# 前言

<!-- more -->

```

提前设置好模板，这样生成一个新markdown文档后，只需修改urlname以及设置分类`categories`与标签`tags`即可，若主题支持，可设置是否有目录`toc`，是否置顶`top`，是否开启评论`comments`，不同的主题可能名称不同，根据自己的主题修改即可。

若有不支持的功能也不会出错，仅仅无法加载该内容。

{{ title }}与{{ date }} 为标题与文档创建日期，不需要改动

分类`categories`里，前面有减号`-`的表示为同级分类，中括号`[]`括起来的为父子分类。

例如

```
categories: 
- [生活,笔记]
- 娱乐
```

文档在推送后，分类为生活类中的笔记类，同时也是娱乐类。

也可以将娱乐类改为 `[娱乐,音乐]`，这样就同时是娱乐类中的音乐类。

# 为博客绑定域名

## 解析域名

以我的域名为例，不同商家解析时都差不多。在域名管理处点击解析

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030752.png)

点击添加记录。会出现如图的添加设置。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030755.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030757.png)

主机记录可理解为域名前缀，即用户输入什么样的网址访问到该解析目标。如果主机记录为www ，则用户需要输入www.[你的域名]才能访问到该解析目标。如果为@，则直接输入域名即可。如果不添加www ，则通过www+域名方式访问的用户将访问失败，@同理，其余的也同理。

<fancybox>

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030754.png)

</fancybox>

记录类型为解析目标的类型，如果想把该域名绑定到一个ip地址，则选A，如果目标为一个网址，则选CNAME。

这里有两种绑定方法，一种是选CNAME然后在记录值填写 [yourname].github.io ，另一种是选A，然后通过cmd命令行输入 `ping [yourname].github.io` 获取ip地址，记录值里填入ip地址。

获取 [yourname].github.io 的ip地址，如图，ping通后会显示ip地址。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030753.png)

记录值根据选择的记录类型进行填写。线路选默认。TTL为缓存生效时间，默认600秒即可，即10分钟后生效(实际大约需要5 分钟)。填写完毕后点击保存。可以为域名填写多个记录， 如图

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030756.png)

前两个是为github pages绑定时添加的记录，一个www、一个@，这样可以让用域名直接访问的和加了www访问的用户都能访问到自己的博客 (部署到服务器后就不再用了所以暂停了)。接下来两条A类型是将网站部署到自己的服务器时，把域名解析到了自己的服务器IP地址，这样可以通过www、或者直接输入域名的方式来访问自己的服务器。最后一条是绑定的七牛云，用来当做博客的图床。每条记录后面都有操作可以进行修改以及暂停和开启。

## 绑定到github pages

登陆到自己的github，进入网站绑定的仓库，进入设置

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030759.png)

往下找到GitHub Pages，在Custom domain填入刚刚购买的域名，点击save保存。勾选Enforce HTTPS则开启HTTPS安全协议。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030758.png)

然后到本地博客`source`文件夹下新建文件CNAME，输入内容为自己的域名，并将文件尾缀如`.txt`等删掉然后保存即可。(没有的话貌似每次将代码从本地推到github都会使域名访问404，因为每次推送都会覆盖原本的仓库代码。所以把CNAME文件放在source中，使每次推送都会建立一个CNAME)

至此，github pages的域名绑定完成了，稍等片刻即可尝试使用域名访问。

# 将博客源代码保存到github

## 创建分支

在仓库中的文件列表的左上方，点击Branch。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030802.png)

搜索 source （分支名，自定义），会提示未找到，是否创建，点击即可创建该分支

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030804.png)

## 设置新建分支为默认分支

进入设置，左边的列表中选择 Branches，默认分支为master，改为新建的分支，然后点击Update更新。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030805.png)

## 同步配置

首先随便找个地方新建一个文件夹，将你的仓库克隆下来。

打开新建的文件夹，右键空白处点击`Git Bash Here`

然后输入下方命令克隆文件

```
git clone 【你的仓库地址】
```

仓库地址获取方法：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030803.png)

点击红框内的按钮复制，然后粘贴到clone后面即可，用空格与clone隔开。

克隆完成后，该文件夹内会出现`【你的用户名】.github.io`文件夹，进去拷贝`.git`文件夹到本地的博客根目录，然后这个新建的文件夹就可以删除了。

接下来在博客根目录右键空白处，打开git bash，输入下方命令，警告不用理会，若没出现报错就没问题。

会需要github的帐号密码，填一下就OK了。

```
git remote add origin 【你的仓库地址】
git add .
git commit -m "【描述，随便写】"
git push origin 【你的保存源代码的分支名】
```

描述部分的效果如图，会将内容显示在该分支上。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030807.png)

每次推送时，输入的描述都会在这次推送时更新的文件后面显示出来。

接下来每次想保存时，输入下方指令即可，

```
git add .
git commit -m "【描述】"
git push
```

但每次都要输入这么多很麻烦，可以创建一个脚本文件，在博客根目录下新建一个txt文本文件，名字随意自己能知道是保存用的就行，将上方三条指令写进去，描述写好后以后固定都是这个，然后将文件改为`.sh`结尾。也可以直接建一个`.sh`尾缀文件，然后用编辑器打开写入。这样以后每次运行这个脚本文件就会自动执行上面三条指令，完成推送。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030806.png)

本地同步到github就完成了，但要注意的是只保存了关键文件，如主题、文章、配置等。

node_modules文件夹和public文件夹是没有保存上去的，public文件夹是生成的静态页面，不需要保存，若迁移后直接生成就有了。

node_modules文件夹存放着需要用到的插件，如果想保存的话，打开`.gitignore`文件，把里面的node_modules删掉保存即可，但是这样会造成每次保存都需要很久时间，因为里面东西太多了，看个人需要决定是否需要保存。

只要配置文件里面的deploy里的branch的值是master的话，生成的静态页面会推送到master分支

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324030808.png)

配置完成后，若以后要迁移到其他的服务器或者电脑上，只需要安装好git、Node.js、hexo，然后使用`hexo init`命令初始化一个根目录，再克隆下来就行了，若不指定克隆分支的话，会克隆默认分支，即设置好的保存博客源代码的分支。

