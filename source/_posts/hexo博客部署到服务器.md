---
title: hexo博客部署到服务器
date: 2020-02-23 09:09:25 
comments: true
toc: true
top: false

categories: 
- [笔记,博客]
tags: [hexo,github,webhook]

---
不使用github pages，改为自己的服务器。将代码托管到gtihub，使用webhook实现github与服务器同步推送代码，并且安装hexo-admin来实现后台管理与服务器到github上的推送。

<!-- more -->

# 购买服务器

服务器商千千万，自行挑选一个靠谱的。

**注意：国内各服务商有学生优惠套餐，但是只能购买大陆服务器，且大陆服务器需要备案才能使用，备案很麻烦，要花十几到二十天左右。但是便宜稳定。**

进入服务商的购买页面，选择配置。

若是一键选择套餐购买，需要选择地区、选择服务器的配置、选择服务器镜像系统、服务器带宽(越大则服务器能承受的压力越大)、购买时长。

若是自定义配置，需要选择购买的计时方式、配置的详细选择，更多的系统选择以及自定义镜像、存储空间。

总结就是越强越贵，时间越长越贵。个人博客不需要非常好的配置，推荐系统选择linux

**注意：大陆服务器需要至少购买3个月时长才可以进行备案。**

<fancybox>

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324032223.png)

</fancybox>

假如是国外服务器，则购买后可以直接进行部署了。如果是头铁选了国内，则需要先进行备案(大概20天左右。备案流程放到最后。)

我使用的宝塔控制面板，简单方便无脑。安装宝塔后，可以在控制面板进行操作来操作自己的服务器。



注：若服务器操作过程出现无法挽回的问题，可以在服务器控制台重装系统。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324032233.png)

# 连接服务器

首先下载putty、xhell等连接工具，我使用的是finalshell，用哪个都可以，原理都一样，用服务器商自带的登陆功能也可以。打开后界面如图。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324032240.png)

点击文件夹，新建一个连接，选择SSH连接

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324032246.png)

名称自定义，主机为上一步的ip地址。填写完后点击确定。

(国外服务器可勾选智能加速，国内则不勾选)此时我使用的是美国服务器，所以勾选了海外加速。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072356.png)

可以看到新建了一个服务器连接，ssr为刚刚自定义的名称，后面有ip地址和端口号，和服务器主机名。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072425.png)

双击该连接，进入服务器，连接成功出现如图所示界面。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072428.png)

如果出现该窗口

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072432.png)

点接受并保存。

# 部署到服务器

## 解析域名

**注**：若github page有绑定域名的话，先把绑定解除，并且将解析暂停，否则会冲突。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072437.png)

---

到域名管理处，点击解析

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072440.png)

按照如图所示添加两条记录，一个主机记录选`@`（直接输入域名即可进入网站），一个选`www`（前面加上www可进入网站），也可以自定义一个前缀，但在后面站点配置时要加进去。

记录类型选A，指向一个IP地址，然后在记录值处填自己服务器的公网IP。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072448.png)

主机记录说明：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072555.png)

## 安装宝塔面板

根据官方教程进行安装。

> [宝塔Linux面板安装教程](https://www.bt.cn/bbs/thread-19376-1-1.html)
>
> 若安装完成不能使用，则需要放行端口：
>
> 腾讯云：https://www.bt.cn/bbs/thread-1229-1-1.html
>
> 阿里云：https://www.bt.cn/bbs/thread-2897-1-1.html  
>
> 华为云：https://www.bt.cn/bbs/thread-3923-1-1.html 

进入服务器，根据自身系统输入安装命令，命令失效则看官方教程，有备用命令

**Centos安装命令：**

```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```

**Ubuntu/Deepin安装命令：**

```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh
```

**Debian安装命令：**

```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh
```

**Fedora安装命令:**

```
wget -O install.sh http://download.bt.cn/install/install_6.0.sh && bash install.sh
```

以cenOS为例：

输入命令进行安装

<fancybox>

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072600.png)

  </fancybox>

输入y，安装宝塔，然后稍等片刻

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072605.png)

如图安装完成，会显示控制面板的url以及用户名和密码

<fancybox>

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072609.png)

</fancybox>

安装完成后，就可以关闭finalShell了，打开浏览器，输入该地址，并输入刚刚显示的用户名和密码，进入面板

这里建议进入后修改登陆面板的帐号与密码，不使用默认生成的。并且将面板的网址保存起来，方便以后直接输入网址进入面板。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072613.png)

进入面板后，会出现如下提示，进行安装软件。可以根据需求进行安装，也可以直接点一键安装，推荐LNMP，且选择极速安装，编译安装太慢。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072618.png)

## 创建站点

宝塔面板安装完成后，在导航栏点击网站，选择添加站点。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072623.png)

设置如下，在域名处填写自己的域名，可填写多个 （填写进的域名在解析完成后可以访问到该网站）



![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072627.png)

生成站点后，点击网站名或者后面的设置，可以进入站点设置来添加一些新的域名以及二级域名等等。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072630.png)

**其中abc为自定义的二级域名，想不想设置随意。设置了就需要在解析时填写对应的主机记录。**

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072634.png)

点击添加后如下，这样用户可以通过以下域名访问到该服务器部署的网站，如果不想让github.io的地址也访问到该服务器，可以删除。

**添加的域名需要解析到服务器才可以正常使用。**

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072637.png)

添加完成后关闭设置即可。

最后到域名管理处。进行解析。添加记录如下

- 记录值：www和@各添加一次，
- 记录类型：选A
- 线路类型：默认
- 记录值：你的服务器IP地址

结果如下（若有自定义二级域名等等，需要再添加上。）

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072641.png)

等待几分钟生效，即可通过域名访问该服务器。

## 使用webhook实现同步页面

虽然服务器是配置好了，但是宝塔并不支持代码托管，也就是说使用`hexo d`命令推送的代码并不能推到宝塔上来实现更新网站。于是使用webhook来实现与github代码同步。

原理：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072645.png)

### 安装宝塔WebHook

在宝塔面板导航栏点击软件商店。搜索 `webhook` 点击安装。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072649.png)

### 配置webhook

安装完成后，点击设置，(可以勾选首页显示。)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072653.png)

点击添加，名称随意，执行脚本先随便填写一点内容，点击提交后再编辑脚本。

（若出现编辑不能保存的情况，则在宝塔面板的右上角点修复）

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072659.png)

添加完成后点击编辑，删除原来随意填写的内容，添加如下代码并修改gitHttp。

注：

1. 原代码有一个$1变量，在后面的密钥部分的URL地址最后通过param=X，将X作为 该变量传入脚本，但因为我无论怎么改都会出现参数错误，因此将该变量删掉了。然后改一下代码，将$1的参数替换为固定的值，只要站点目录存在就没问题。
2. 大概是因为自己设置了保存博客源代码的分支为默认分支的原因，用原代码里面的有一句`git pull`总是拉不过来文件，在服务器上手动拉取发现拉取的是博客源代码的分支。故在原代码中将`git pull`改成`git pull origin master`来指定拉取静态页面的分支。

![image-20200228112635921](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072705.png)

```
#!/bin/bash
echo ""
#输出当前时间
date --date='0 days ago' "+%Y-%m-%d %H:%M:%S"
echo "Start"
#git项目路径
gitPath="/www/wwwroot/【站点根目录】"
#git 网址
gitHttp="【仓库git地址】"

echo "Web站点路径：$gitPath"

#判断项目路径是否存在
if [ -d "$gitPath" ]; then
        cd $gitPath
        #判断是否存在git目录
        if [ ! -d ".git" ]; then
                echo "在该目录下克隆 git"
                sudo git clone $gitHttp gittemp
                sudo mv gittemp/.git .
                sudo rm -rf gittemp
        fi
        #拉取最新的项目文件
        echo "拉取最新文件"
        sudo git reset --hard origin/master
        sudo git pull origin master
        #设置目录权限
        echo "设置目录权限"
        sudo chown -R www:www $gitPath
        echo "End"
        exit
else
        echo "该项目路径不存在"
        echo "End"
        exit
fi
```

**更新：** 在指令语句前加入sudo，授予管理员权限，避免执行失败

gitHttp路径为github代码仓库的地址，需要到代码库中查看(带.git尾缀的地址，即hexo部署时配置 `_config.yml`时填写的地址。)，点击复制键进行复制

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072727.png)

粘贴后格式应该如下	

```
gitHttp="https://github.com/XXXXXX.git"
```

随后点击右下角的保存即可。

### github配置hook

编辑完成后，点击查看密钥

![image-20200227215746441](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072732.png)

复制好密钥以及下方URL的`&`前面的内容（全复制也可以）

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072735.png)



进入github的网站代码库的设置，导航栏选webhook，然后点击Add webhook

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072739.png)

填写内容

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072744.png)

填写好后点击Add webhook。

然后回到面板，点击测试，然后在日志中查看结果。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072749.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072753.png)

同时回到github的webhook界面，编辑刚刚的钩子

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072757.png)

在最下面可以看到成功的信息。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072803.png)

这样以后在本地进行的deploy，服务器最自动钩取github仓库的master分支，实现将博客部署到服务器上。然后使用域名就可以进行访问(不要加https://)。

## 添加SSL证书，开启https协议

**注**：若出现访问拒绝的话，注意是否加了https协议。

没有配置SSL证书的话，用https访问会被拒绝。SSL证书有收费的也有免费的。

宝塔自带免费证书，但要求实名认证。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072807.png)

接下来以个人服务商腾讯云的免费证书为例，

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072812.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072816.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072820.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072824.png)

按步骤填写即可注册证书。添加后下载证书，然后解压。

若关闭了界面，可以在域名管理处下载证书

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072829.png)

打开下载好的文件夹，打开Apache

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072833.png)

打开`.crt`和`.key`结尾的文件。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072836.png)

然后在宝塔面板进入站点的设置，图中点击网站名或者设置都可以

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072840.png)

如图，在SSL界面其他证书里，将`.key`结尾的密钥放入左边，`.crt`结尾的证书放入右边，保存，然后强制HTTPS，即可开启https协议。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072844.png)



# 将博客源代码同步到服务器（舍弃）

## 更新（必看）：

本来是想的利用hexo-admin实现在服务器上开启后台管理，然后就能实现理想中的功能：

1. 本地操作完博客后，源代码+静态页面+文章都可以同步到服务器上

2. 服务器操作完博客后，源代码+静态页面+文章也都同步到本地

这样的话，我可以在本地尝试修改主题与配置，满意后进行推送同步到服务器。在没有hexo与git环境时（如临时用其他电脑或者用手机），然后又不能安装或者不想安装的话，可以通过hexo-admin后台来写文章并deploy，等到了自己的电脑上直接克隆就可以完成同步了。

但在配置时发现了一个问题，hexo-admin提供的deploy功能貌似仅支持以hexo开头的命令，如`hexo d`、`hexo new "文章名" `，我试图加入git命令然后就报错了。

这就导致我能成功将本地的源代码、静态页面推送到服务器，但是用hexo-admin新建然后写的文章是没办法自动保存到github上来克隆到本地的。再考虑到安装插件的问题，一些功能需要安装一些插件（如音乐播放器、live2D、加入视频等等）。插件是不会被推送的，若想推送插件的话，每次推送都要等待很长时间。

综上，故暂时舍弃源代码同步到服务器，让服务器仅保存静态页面就行了。所以下面的内容可以不用看了。

PS：关于能否使用git命令的问题已经提交到github上的Issues，如果有解决办法的话希望能留言告诉我。

## 在服务器上部署hexo

关于CentOS的安装git、Node.js我遇到一些问题，参考了下面两篇文章完美解决，故这里就不说安装方法了，直接看这两篇就行了。

CentOS安装Git参考链接：
https://www.cnblogs.com/imyalost/p/8715688.html

**注**：Hexo需要10版本以上才能支持，默认安装的话版本开头为6，需要安装最新版本才可以，我就用默认安装Node.js的方法结果最后hexo安装失败。

CentOS安装最新版Node.js参考链接：

https://www.jianshu.com/p/4a9449506924

安装hexo指令：

```
npm install hexo-cli -g
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324072854.png)

警告不用理会。

## 克隆保存在github上的博客代码

通过cd命令切换到想保存博客根目录的文件夹下，例如我打算把博客的根目录放在 /www下，则输入`cd /www`，

然后克隆在github上的博客源代码，例如我的命令为

`git clone https://github.com/lluuiq/lluuiq.github.io.git`，后面是仓库地址，改为自己的。

```
git clone 【仓库地址】
```

这样在输入该指令的文件夹下会出现【yourusername】.github.io的文件夹，里面放着博客的源代码。

若想改个名字的话，在包含根目录的文件夹下（我的是/www）输入下面指令

```
mv 【yourusername】.github.io 【newname】
```

我将文件夹名称改为wa2000，下面的wa2000文件夹都是博客根目录。

在服务器上的hexo根目录已经建成，接下来就是同步github上的源代码仓库，使得当github仓库的文件更新时，服务器上的博客源代码也会同步更新。

## 服务器上的hexo同步github

### 宝塔与webhook安装

步骤同 [部署到服务器](#部署到服务器)

### 设置webhook

与上方内容相同，但需要更改的是分支名选择存放博客目录的分支

个人的配置（参照修改）

git项目路径：`gitPath="/www/wa2000"`

git网址：`gitHttp="https://github.com/lluuiq/lluuiq.github.io.git"`

分支名：`source`

```
#!/bin/bash
echo ""
#输出当前时间
date --date='0 days ago' "+%Y-%m-%d %H:%M:%S"
echo "Start"
#git项目路径
gitPath="【你的博客根目录地址】"
#git 网址
gitHttp="【你的仓库地址】"

echo "Web站点路径：$gitPath"

#判断项目路径是否存在
if [ -d "$gitPath" ]; then
        cd $gitPath
        #判断是否存在git目录
        if [ ! -d ".git" ]; then
                echo "在该目录下克隆 git"
                git clone $gitHttp gittemp
                mv gittemp/.git .
                rm -rf gittemp
        fi
        #拉取最新的项目文件
        git reset --hard origin/【你的分支名】
        git pull
        #设置目录权限
        chown -R www:www $gitPath
        echo "End"
        exit
else
        echo "该项目路径不存在"
        echo "End"
        exit
fi
```

添加webhook后，参考上方内容与仓库进行链接即可。

### 创建站点

如图点击添加站点。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073316.png)

添加域名可以加前缀，但加了前缀也要加入对应的解析。根目录后面一定要是public文件夹，生成的静态页面会保存在该文件夹中，只有将该文件夹设为根目录网站才会正常显示，最后点击提交即可创建。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073320.png)

然后回到服务器，安装必要包

```
npm install hexo --save
npm install --save hexo-deployer-git
```

输入github的用户名与密码

```
git config --global user.email "【github邮箱】"
git config --global user.name "【github用户名】"
```

### 配置SSH

配置SSH免去每次推送都要帐号密码，任意地方输入下方指令，【注释】部分可用自己邮箱，github,也可以不加`-C`

```
ssh-keygen -t rsa -C "【注释】"
```

中间都按回车就行了，然后到ssh存放的地方

```text
cd ~/.ssh
vim id_rsa.pub
```

打开id_rsa.pub后，复制里面的公钥（用finalshell的话直接在下方的文件目录里双击打开也可以）

然后到如图地方添加公钥

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073333.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073337.png)

然后到仓库的地方，复制ssh地址

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073342.png)

![mark](http://blogimg.wa2000.cn/blog/20200223/pTndRV7uRMpW.png?imageslim)

（若本来就是ssh地址则跳过）打开根目录的配置文件_config.yml，将deploy下的repository改为ssh地址。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073349.png)

在博客的根目录下生成静态页面并尝试推送到github

```
hexo clean
hexo g
hexo d
```

注：若出现下方情况则使用下方命令删除`.user.ini`

```
chattr -i 【.user.ini路径】
rm -rf 【.user.ini路径】
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073354.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073400.png)

若出现下方情况则修改ssh配置

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073406.png)

```
vim /etc/ssh/sshd_config
```

找到 RSAAuthentication与PubkeyAuthentication，将注释去掉，并确定AuthorizedKeysFile后面为`.ssh/authorized_keys`且可用。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073410.png)

然后重启ssh服务。

```
/sbin/service sshd restart
```

再次执行`hexo d`可能会出现下方警告

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073413.png)

该警告是让你将github的IP加入host，可以无视，也可以加进去去掉警告。

```
vim /etc/hosts
```

然后在里面加入`【警告中的IP地址】 github.com`，保存并退出即可。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073417.png)

清除、生成、推送都成功后，重启宝塔面板

```
/etc/init.d/bt restart
```

重启后，在本地使用推送将博客源代码推到github时，服务器上会自动拉取进行同步。

接下来就是在服务器上开启远程后台管理了。

# 开启后台管理（舍弃）

使用hexo-admin插件开启后台管理功能，可以通过网页进入后台管理文章，也可以通过内置的脚本实现部署与推送。

## 放行4000端口

到宝塔面板的安全里放行4000端口，说明随意填。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073800.png)

以腾讯云为例，到服务器的管理处放行4000端口。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073648.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073809.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073824.png)

**注意**：`hexo s`命令不支持https，在输入网站时不要加https

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073828.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073834.png)



## 测试推送

[git操作官方文档](https://git-scm.com/docs)，或者百度git指令查询详细用法。

在根目录处执行下方执行指令

```
git add .
git commit -m "【更新说明，随便填】"
git push origin 【博客源代码分支名】
```

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073840.png)

出现上方提示说明可以进行推送。

如果保存源代码的分支不是默认的，要在`git push`后面空一格加上`origin 【博客源代码分支名】`

若提示

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073843.png)

则输入

```
git remote add origin 【github仓库的ssh地址】
```

## 编写脚本

在根目录创建一个文件夹存放脚本（直接放根目录也行，但后面记得更改配置的路径），名称随意，我用admin作为文件夹名，deploy作为脚本名。然后进入创建的文件夹，新建并编辑一个脚本文件

我的代码为`mkdir admin`与`vim deploy.sh`

```
mkdir 【新建的文件夹】
cd 【创建的文件夹】
vim 【脚本名】.sh
```

在脚本文件中输入下方指令，“save blog”里面是更新说明，自定义填写。

```
#!/usr/bin/env sh
hexo g
hexo d
```

然后按ESC，接着输入`:wq`保存并退出。

这样当用后台管理时，会先生成静态页面，再进行部署，部署完成后会将源代码推送到github。

可自行修改需要的命令，例如加入`hexo clean`，也可以加一些其他自己需要的命令。

为刚刚脚本授予权限

```
chmod +x 【脚本名】.sh
```

然后执行该脚本看看效果，如果一切顺利，则可以进行下一步。效果大概如图：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073849.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073853.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073856.png)

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073901.png)

脚本配置好后，开启开机自动启动`hexo s`命令来启动后台，因为hexo-admin

在创建的存放脚本的文件夹中新建自启脚本（同样名称自定义）

```
cd 【存放脚本的文件夹】
vim 【自启脚本文件名】.sh
```

然后输入命令，cd后面的路径要换成自己的博客根目录路径，例如我的为`cd /www/wa2000`

```
#!/bin/bash
cd 【博客根目录路径】
hexo s
```

写完后同样按ESC，输入`:wq`保存并退出

添加权限

```
chmod +x 【自启脚本名】.sh
```

然后返回服务器的根目录，打开`etc/rc.d/rc.local`

```
cd ~
vim /etc/rc.d/rc.local
```

在下面添加脚本路径，如我的脚本存放目录为`/www/blog/admin/server.sh`，添加效果如下

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073906.png)

然后保存并退出。

执行下方命令授权

```
chmod +x /etc/rc.d/rc.local
```

然后重启服务器

```
reboot
```

稍等片刻进入`http://【域名】:4000`，若能进入，说明配置成功。

## 安装hexo-admin并配置

参考文档：[Easy Hexo](https://easyhexo.com/4-High-order-hexo-gamer/4-1-remote-editing/#三、在本地安装-hexo-admin)	[hexo-admin官网](https://jaredforsyth.com/hexo-admin/)

服务器上进入博客根目录，然后输入命令安装hexo-admin

```
npm install --save hexo-admin
```

安装完成后即可通过`http://【域名】:4000/admin` 进入后台。接下来进行一些配置。

进入后台的设置界面，点击红框内的链接。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073910.png)

如图，填入登陆后台用的用户名与密码，secret能为密码进行加密，随意填自己喜欢的短语就行。

![image-20200223201005011](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073919.png)



将生成的代码拷贝到博客根目录下的配置文件`_config.yml`中，并添加deployCommand

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073925.png)

deployCommand的内容单引号内为一条指令

`./admin/deploy.sh`指运行保存在admin文件夹内的deploy.sh，将路径改为自己的脚本运行指令即可。

保存，然后重启服务器。

# 关于网站备案的琐事

到购买服务器/域名的服务商那里有详细的备案流程说明，这里仅记录个人备案遇到的坑。以腾讯云举例。

> [腾讯云备案流程](https://cloud.tencent.com/document/product/243/18958)

1. 国家规定服务器需要购买至少3个月才能备案

   学生套餐优惠只能购买三次，一次最短购买一个月时长，最长为一年时长，本来抱着试试的心态只买了一个月，结果发现居然要至少3个月才能备案，于是只能再去用学生套餐来延长时长，本来三次机会，结果花了两次机会只买了一年一个月，如果确定想用大陆服务器并且想长时间使用的话，建议一次购买最长时长，10元/月算非常便宜了。

2. 审核时间长

   首先需要先为域名进行实名认证，实名认证后备案需要申请幕布进行拍照(给你邮过去，免邮)，等幕布到了以后按要求拍照并上传，填写关于网站的资料以及服务器的资料，最后提交。

   大概腾讯那边审核一两天，然后腾讯帮你提交到审核局审核个10天左右(最晚一个月，个人经历时间为10天左右)，审核通过后会给你工信部备案号，但还要到[全国互联网安全管理服务平台](http://www.beian.gov.cn/portal/index.do)再提交一次备案，不过这个审核较快，一天就通过了。通过后会给你联网备案号。

   以百度为例![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324073929.png)上面的为工信部备案号，下面的为联网备案号。

3. 关于在**全国互联网安全管理服务平台**备案

   **注意**：里面有一个为网站填写信息的，有个选择网站是否为交互类型，如果不是论坛、有注册功能的那种一定要选择否，选是的话需要到当地公安局一趟进行当面审核。这是为了保证网站安全所以需要到公安局进行审核，并且填写大概7-8页厚的表格，所以个人博客的话选否就行了。