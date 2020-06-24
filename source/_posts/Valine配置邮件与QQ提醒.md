---
title: Valine配置邮件与QQ提醒
comments: true
toc: true
top: false
mathjax: false

categories:
  - - 笔记
    - 博客

tags:
  - Valine
date: 2020-05-29 22:33:21
---

valine在配置好后没有邮件提醒功能，需要到[LeanCloud](https://www.leancloud.cn/)登陆控制台进行一系列设置。

最开始是只想配置个邮件提醒，但直到看到了这位大佬的博文

[Valine评论之Valine-admin配置攻略](https://www.antmoe.com/posts/2380732b/index.html)

该版本基于Valine-admin的二次开发，加入了微信提醒、QQ提醒功能。

因为个人常用QQ，微信很少登陆，故只配置了QQ提醒功能。微信提醒的配置方法与QQ类似。

QQ消息推送机器人：[Qmsg酱](https://qmsg.zendee.cn/)

本文基于上述配置攻略博文，详细记录自己的配置过程。请先确定自己已经配置好了基础的valine评论服务。

<!-- more -->

## 获取Qmsg酱的key

进入官网[Qmsg酱](https://qmsg.zendee.cn/)，使用QQ号一键登录即可。

在首页如下

[![image-20200528185730555](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015227.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015227.png)

添加完成后，打开你添加的QQ号，**添加机器人为好友**

选了哪个就加哪个为好友，添加好友后是自动通过的，不加好友怎么收到提醒呢。

------

接下来到右上角点击文档，

[![image-20200528185920380](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015233.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015233.png)

[![image-20200528190006620](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015242.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015242.png)

复制接口地址后面的key值， 即`send/` 后面的所有字符，可以暂时将该key记录在笔记本等位置，稍后配置要用。

## 配置valine实例

### 云引擎部署

[Leancloud官网](https://leancloud.cn/)，进入后登陆到自己的控制台。进入自己创建的应用。然后进入云引擎/部署

[![image-20200528191403112](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015251.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015251.png)

大佬二次开发的valine-admin-server的github地址：https://github.com/sviptzk/Valine-Admin-Server

在下面的部署中的Deploy from中填入该地址。

**注：若是打算自己定义邮件通知的模板或者QQ提醒的模板的，fork一份到自己的github来修改。**

**这样填入的地址使用fork到自己github中的地址，后面修改模板时修改代码即可。**

[![image-20200528191440296](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015255.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015255.png)

填入后点击部署。出现如下所示的log信息（最后提示1个实例部署成功）即可。

[![image-20200528015231941](https://gitee.com/lluuiq/blog_img/raw/master/img/20200528015233.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200528015233.png)

### 设置变量

进入到云引擎/设置中

[![image-20200528191931864](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015307.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015307.png)

在页面中添加新变量

[![image-20200528191921578](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015310.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015310.png)

首先添加几个基本变量：

括号中说明根据使用情况来选填，没有括号的为必填项。

| 变量名        | 变量值                                                       | 变量值举例                                |
| ------------- | ------------------------------------------------------------ | ----------------------------------------- |
| ADMIN_URL     | 博客网址                                                     | [https://lluuiq.com](https://lluuiq.com/) |
| QMSG_KEY      | （使用QQ提醒必填）之前获得的Qmsg的key                        | 7b04XXXXXXXXfc5                           |
| QQ            | （使用QQ提醒必填）Qmsg中添加的自己的QQ号                     | 844520941                                 |
| QQ_SHAKE      | （想在提醒时被戳一下就设置）是否开启QQ提醒时戳一戳           | true                                      |
| SENDER_NAME   | 发件人昵称                                                   | lluuiq                                    |
| SITE_NAME     | 博客网站名称                                                 | lluuiq’s Blog                             |
| SITE_URL      | 网站地址                                                     | [https://lluuiq.com](https://lluuiq.com/) |
| SMTP_SERVICE  | SMTP服务器提供商                                             | 163                                       |
| SMTP_PASS     | SMTP授权码                                                   | CSTXXXXXXXOUC                             |
| SMTP_USER     | 用于发邮件的邮箱，需要与SMTP服务商对应                       | [lluuiq@163.com](mailto:lluuiq@163.com)   |
| TEMPLATE_NAME | 邮件模板                                                     | custom2                                   |
| TO_EMAIL      | （在valine评论填邮箱的情况下好像没什么用，但是可以加上用于后面自定义邮件模板时使用）博主的收件邮箱 | [mail@lluuiq.com](mailto:mail@lluuiq.com) |

一些说明：

- **ADMIN_URL**：开启网页后台管理功能才需要添加的变量，若不需要通过网页来管理的话可以不加，因为可以登陆LeanCloud来进行管理，开启方法后面介绍。

- **QQ**：自己接收消息的QQ号，要存在之前获取key时添加的QQ列表中

- **SMTP_SERVICE**：这是valine支持的一些服务商：[Supported](https://nodemailer.com/smtp/well-known/#supported-services)，选择对应的服务商后，要更改对应的发件邮箱与授权码，关于授权码的获取方法各个服务商的直接百度即可，后面我以网易163的举例。

  关于为什么使用网易，我使用QQ邮箱结果发件一直`550 mail content denied`，被腾讯服务器当成垃圾广告邮件给退回，故换成了163邮箱。想使用QQ邮箱来接收消息的话，可以设置163邮箱的自动转发。

- **SMTP_PASS**：163为例的获取方法，点击[获取SMTP授权码，并设置自动转发（以163举例）](https://lluuiq.com/post/202005290137/?t=1593036314039#获取SMTP授权码，并设置自动转发（以163举例）)跳转到下方查看。

- **TEMPLATE_NAME**：valine自带的主题有默认default、彩虹rainbow，该版本新增的有custom1、custom2，其中custom2的样式如下：

  [![image-20200528193512145](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015313.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015313.png)

  当然，如果是fork的主题的话，这个是可以自行修改的，后面再讲自己的修改过程。

</br>

**注意事项：**

我没有配置垃圾过滤、微信提醒。以及并没有使用自定义服务商（我配置的总是失败，想使用自定义服务商的可以参考原博文进行配置 ）。

每次修改变量后，点击保存后是**不会生效**的。需要重新部署一次云引擎（回到[云引擎部署](https://lluuiq.com/post/202005290137/?t=1593036314039#云引擎部署)，不用重新填github地址，直接点击部署即可）。

配置完成后并且重新部署后，即可尝试在valine评论里发送一条评论来进行尝试。



博主收到的效果：

[![image-20200528201032449](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015319.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015319.png)

[![image-20200528201058382](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015322.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015322.png)

访客收到的效果：

[![image-20200528201143027](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015325.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015325.png)

这是默认的模板，若需要修改的话后面有介绍。

## 休眠策略配置

LeanCloud现在每天必须停机6个小时，并且若30分钟内无访问会自动休眠。

详细的配置方法还是建议参考原文[Valine评论之Valine-admin配置攻略](https://www.antmoe.com/posts/2380732b/index.html) 。

#### 自动唤醒任务

登陆该网址：https://cron-job.org/

注册帐号后，创建任务。

[![image-20200528231230639](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015327.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015327.png)

[![image-20200529011449656](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015603.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015603.png)

第一个title 就是给这个任务起个名字，随意填

第二个http链接输入LeanCloud的后台管理地址，例如我通过`https://abc.lluuiq.com`来进入后台，则填进去

时间使用自定义，然后日、星期、月都全选（先选中第一个，然后拉到最下面按shift点一下最后一个）

小时我选择的是7点到23点，详细根据自己需要来设置，总之中间要有6小时的时间让LeanCloud停机

分钟可以使用ctrl键来选择多个，我设置的是0、10、20、30、40、50，即在0分、10分、20分。。的时候访问一次后台。

这样设置的结果就是每天的7:00开始到晚上12:00，每隔10分钟进行一次访问来唤醒机器。

[![image-20200529011825115](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015333.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015333.png)

最后如果要保存日志则勾选Save responses，创建任务即可。

创建完成后，任务列表会出现目前进行的任务。

[![image-20200529011908143](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015336.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015336.png)

点击右方的History可以查看历史状态的信息

[![image-20200529011955085](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015338.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015338.png)

前面有对号的标志即表示成功访问了后台，后面可以看到具体的时间以及状态码等等。

#### 重发邮件任务

使用LeanCloud自带的定时任务来完成即可。进入云引擎/定时任务

[![image-20200529012155255](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015340.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015340.png)

创建定时任务，

[![image-20200529012305308](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015342.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015342.png)

关于Cron表达式，因为我设置的是每天7点到晚上12点之间来不停唤醒机器，所以我的表达式为

```
0 5 7 * * *
```

秒 分 时 天 月 星期，假如Cron表达式为 a b c d e f

则在 e月份的第d天的c时b分a秒，且仅为星期f时进行该任务。 *表示全部。

所以我的表达式意思为 在每天的7点05分0秒时，进行resend_mails函数，即检测未发送的邮件进行补发。

这样就解决了在0点到7点机器停机时假如有回复不能进行提醒的问题。

（目前仅是理论，因为并未实际测试过）

#### 更新

上述配置已成功。7点05收到了邮件补发。

[![image-20200529070819358](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529070827.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529070827.png)

查看日志可以发现

[![image-20200531142051117](https://gitee.com/lluuiq/blog_img/raw/master/img/20200531142056.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200531142056.png)

[![image-20200531141847831](https://gitee.com/lluuiq/blog_img/raw/master/img/20200531141900.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200531141900.png)

## 获取SMTP授权码，并设置自动转发（以163举例）

登陆[163邮箱](https://mail.163.com/)，注意登陆的邮箱必须要是变量SMTP_USER填的值。

在设置里可以找到`POP3/SMTP/IMAP`

[![image-20200528194857850](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015346.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015346.png)

随便开启一个服务，主要是需要SMTP服务，IMAP与POP3无所谓。

我记得是开启时就会获得授权码，该授权码即为SMTP_PASS的值。

[![image-20200528195001992](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015348.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015348.png)

也可以在下面添加新的授权码

[![image-20200528200300874](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015350.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015350.png)

在设置里的常规设置中,找到自动回复/转发

[![image-20200528194813459](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015352.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015352.png)

[![image-20200528200338330](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015354.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015354.png)

填写转发到哪个邮箱，然后验证一下即可。若打算在该邮箱内保留邮件，则勾选保留原邮件。

[![image-20200528200356454](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015356.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015356.png)

配置好后返回 [设置变量](https://lluuiq.com/post/202005290137/?t=1593036314039#设置变量)继续配置即可。

## ====以下有需要则看====

## 开启网页后台管理

需要有个域名，进入设置里的域名绑定

[![image-20200528202131169](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015358.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015358.png)

这里因为我已经绑定过，所以显示的不一样，总之点击绑定新域名的那个按键。

[![image-20200528202237785](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015401.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015401.png)

二级域名可以自定义 ，例如 abc.lluuiq.com，我的域名是lluuiq，二级域名为abc。

这里就填个abc.lluuiq.com，稍后到域名管理处进行解析。

[![image-20200528202409331](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015402.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015402.png)

填好后大概会稍等一会，然后会给出CNAME记录值。记录值为`CNAME:`后面的内容，即

```
kkfwnugs.cn-n1-cname.leanapp.cn
```

[![image-20200528202542704](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015405.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015405.png)

接下来到域名管理处进行解析CNAME

[![image-20200528202747129](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015407.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015407.png)

解析完成后，并且在设置变量中有添加ADMIN_URL的话，即可通过 `https://绑定的云引擎域名` 来进行访问

需要注意的是开启了自动管理SSL才能使用https访问，否则只能通过http访问。

在访问之前，先登陆`https://绑定的云引擎域名/sign-up`注册一个管理员帐号

[![image-20200528211613911](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015409.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015409.png)

邮箱是SMTP设置的邮箱，无法修改。

登录名使用只读里面的邮箱（登陆时要输入邮箱，我用自定义的昵称无法登陆，并且只能让登录名等于只读中的邮箱才有效。。），密码自定义。这样登录名即为SMTP的邮箱，密码为自定义的密码。

确认设置后，再通过`https://绑定的云引擎域名`来登陆，即可访问后台。

[![image-20200528212716610](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015412.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015412.png)

管理界面如图所示，样式可以更改，参考[修改右键、QQ提醒的模板](https://lluuiq.com/post/202005290137/?t=1593036314039#修改右键、QQ提醒的模板)去修改后台管理的即可。

[![image-20200528212738206](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015414.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015414.png)

## 修改邮件、QQ提醒的模板

### 说明

修改的前提是在[云引擎部署](https://lluuiq.com/post/202005290137/?t=1593036314039#云引擎部署)中使用的github地址是fork的地址。

克隆fork的代码仓库到本地，对文件进行修改。

[![image-20200528214044654](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015419.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015419.png)

- public/stylesheets中的css文件是 views/comments.ejs的样式表
- template内的文件夹名即[设置变量](https://lluuiq.com/post/202005290137/?t=1593036314039#设置变量)中的`TEMPLATE_NAME`的值，引入对应的模板。这里我copy了一份custom2文件夹重命名为lluuiq来进行自定义，保证原本样式的情况下来修改。
- check-spam.js为过滤邮件的脚本，基本不用管。
- send-mail.js中设置QQ提醒的模板，并且可以修改发送邮件时的一些设置和邮件标题
- 其余的能不动就不动。

**其余说明：**

- 最好copy一份主题文件到新的文件夹中来对副本进行修改，这样能保持原主题的内容。
- 详细的修改可以自己尝试，可以重写一份页面来全面替换，这里例举个人对原有的主题进行修改的内容。
- 以下出现的process.env.XXX 表示获取云引擎设置的变量名内容。
- <%=XXX%>为获取send-email.ejs里的对应代码块的变量。notice.ejs获取站长提醒的，send.ejs获取访客提醒的。
- 修改完后，要提交和push到github上，然后LeanCloud的云引擎再重新部署才能生效。

### 修改发送邮件的标题

#### 站长邮件提醒

打开utilities/send-mail.js

[![image-20200528214657413](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015427.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015427.png)

站长自己发的评论不需要通知的内容为 comment.get(“mail”)来获取新评论的邮箱，如果是站长自己的邮箱则不发送邮件，毕竟自己回复别人干嘛发邮件来提醒自己。（QQ也不会提醒）

这里因为我设置了163邮箱的转发，所以SMTP_USER=163邮箱，但自己使用的不是这个邮箱。所以如果不进行其他设置的话，这段代码不会生效。这也是为什么当时加了TO_EMAIL变量指向自己的邮箱。当判定获取的邮箱为自己的邮箱时，就不会再进行提醒。

如果设置的SMTP_USER邮箱与自己接收提醒的邮箱为同一个，那么TO_EMAIL就可以去掉，这部分就不用管了。

------

第二个红框的部分，emailSubject为邮件的主题，可以根据自己的喜好来进行修改。

我在修改主题的下方的变量名中添加了一个变量senderName来获取LeanCloud中的SENDER_NAME变量，用来当自己的昵称，可以放在邮件提醒里的称呼中，也可以放在结尾的 `@2020 lluuiq` 中。

其余的部分为LeanCloud的日志输出内容，可以不用管，想修改输出信息的可以进行修改。

#### 访客邮件提醒

还是在utilities/send-mail.js中，代码块在下方，注意和站长提醒的类似，但代码是不一样的。

[![image-20200528215622357](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015430.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015430.png)

站长被@不需要提醒，是当访客回复自己时不触发这个回复提醒（毕竟站长提醒那里已经发一次了）。

第二个红框同上来修改 发送给访客的 邮件的 主题。

其余同上为输出日志，想修改的自行修改即可。

### 修改QQ提醒的模板

还是utilities/send-mail.js里。

[![image-20200528220435859](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015433.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015433.png)

第一个红框的部分为戳一戳功能，基本不用修改。

第二个红框的部分为QQ机器人发送消息的模板，**这里是我修改之后的样子**，原来的样式是有一堆QQ表情的，我给删除了，并添加一些语句。[CQ:face,id=63]为鲜花表情，详细的id可以百度搜索。

$(text) 获取评论内容、$(url) 获取文章地址 、axios.get() 调用Qmsg接口 。。。等这样的内容就不用修改了。

最后一个红框是输出日志，不管就行了。

微信的模板修改与QQ的同理，找到对应的内容进行修改即可。

</br>

我修改后的简约提醒模板如图：

[![image-20200531142340361](https://gitee.com/lluuiq/blog_img/raw/master/img/20200531142344.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200531142344.png)

### 修改发送邮件的内容模板

#### 说明

内容模板都在template/主题文件夹 中，若在原主题上进行修改则进入对应文件夹修改ejs文件就行了。这里我copy的custom2来进行修改的。

[![image-20200528221841902](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015436.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015436.png)

notice.ejs为发送给自己的评论提醒模板。

send.ejs为发送给访客的评论回复模板。

#### 站长提醒

进入notice.ejs

[![image-20200528223121881](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015438.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015438.png)

其中需要说明的是<%=sendName%>，为获取在[站长邮件提醒](https://lluuiq.com/post/202005290137/?t=1593036314039#站长邮件提醒)里设置的sendName变量。

注意notice.ejs获取的是站长邮件提醒的代码块的内容。

稍后的send.ejs获取的是访客邮件提醒的代码块内容，也就是说如果访客邮件提醒的代码块里没有设置这个变量。那么send.ejs里使用<%=sendName%>是无效的，并且不会发送邮件给访客。（当初发现没有发邮件找了好久的原因，后来才发现是没在访客的代码块里添加该变量）

[![image-20200528224442093](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015441.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015441.png)

部分获取评论内容的东西就不用修改，修改一些自己想要的样式什么的就行了。

从这里再往下基本都是CSS，修改样式的。

效果图：

[![image-20200528230358526](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015443.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015443.png)

#### 访客提醒

进入send.ejs

代码内容与notice.ejs几乎一模一样，但是要注意的这里的内容是让访客看到的，根据自己喜好来修改或添加想让访客收到回复时看到的内容就行了。

[![image-20200528224731789](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015446.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015446.png)

Dear <%=pname%>为 Dear 访客昵称。

我删掉了原来的h3标签，因为显得过于冗余了，直奔主题显示曾经的评论、收到的回复。

[![image-20200528225041802](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015449.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015449.png)

这里在页脚处添加了一些信息，注意copy原来的<p>标签语句后把id去掉，html里的id只能有一个。

效果图：

[![image-20200528230322245](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015451.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200529015451.png)