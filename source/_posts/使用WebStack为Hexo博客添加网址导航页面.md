---
title: 使用WebStack为Hexo博客添加网址导航页面
comments: true
toc: true
top: false
mathjax: false

categories:
- [笔记]

tags: [hexo,WebStack]

date: 2020-06-13 22:33:21
---

因为经常把一些网站添加到浏览器的书签栏，目前已经多到眼花缭乱了，故想个办法为博客新建一个分页，把一些网址存在博客上，自己浏览器上存一部分。

<!-- more -->

## 说明

WebStack的github地址：[WebStack](https://github.com/hui-ho/WebStack-Laravel)

配置过程中有很多的坑，

WebStack是个开源项目，在查阅使用方法时发现基本都是基于wordpress与typecho进行使用，但个人是用的Hexo，所以想在Hexo上实现它。

基于源代码

需要：

- 解析二级域名到服务器上
- 安装PHP≥7.2

## 在服务器上克隆源代码

克隆地址随意。这里因为我用的是宝塔面板，所以放在了wwwroot下面，若不在这里，后面更改创建站点时的路径。

[![image-20200613085954744](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165334.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165334.png)

## 安装PHP并配置

到宝塔面板的软件商店搜索PHP，然后安装≥7.2的版本即可。这里我安装的是7.4。

[![image-20200613091542878](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165338.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165338.png)

安装好后，点击设置 ，在禁用函数里把proc_open、passthru、putenv删除。这里是我删除过后又重新加回来的，所以看着顺序不一样，找到自己的删除即可。

[![image-20200613110549141](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165340.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165340.png)

然后在安装拓展里，安装fileinfo

[![image-20200613104649606](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165342.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165342.png)

## 创建网站站点

[![image-20200613102751691](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165346.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165346.png)

在 `站点设置/网站目录` 里面修改一下运行目录，改为public，然后保存

[![image-20200613093015517](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165349.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165349.png)

在伪静态里将规则改为laravel5，否则后台是404·

[![image-20200613124010787](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165351.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165351.png)

## 安装依赖包

输入下面这条指令切换composer源为华为源。

```shell
composer config -g repo.packagist composer https://mirrors.huaweicloud.com/repository/php
```

到克隆下来的WebStack-Laravel路径

```shell
cd 你的WebStack-Laravel路径
```

然后执行以下语句安装composer

```shell
rm -rf composer.lock
composer install
```

第一次安装会提示失败，出现下图，提示Carbon版本过低。

[![image-20200613113307204](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165355.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165355.png)

打开WebStack-Laravel文件夹下的composer.json 然后在require代码块里插入以下代码：

注意插入后，原本的最后一句末尾加个逗号。

```shell
"kylekatarnls/laravel-carbon-2": "^1.0.0",
"nesbot/carbon": "2.16.3 as 1.34.0"
```

[![image-20200613110407285](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165357.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165357.png)

然后再次执行

```shell
rm -rf composer.lock
composer install
```

若出现如图所示信息就没问题了，下面连接数据库的信息不用管

[![image-20200613112229847](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165400.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165400.png)

## 编辑配置

在WebStack-Laravel下执行

```shell
cp .env.example .env
```

然后编辑 `.env`，需要修改的配置如下

```shell
APP_ENV=production
APP_URL=站点二级域名（若没开启SSL则使用http）

DB_DATABASE=数据库名
DB_USERNAME=数据库用户名
DB_PASSWORD=数据库密码
```

示例图如下：

[![image-20200613112804677](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165403.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165403.png)

生成KEY，执行

```shell
php artisan key:generate
```

迁移数据，执行

```shell
php artisan migrate:refresh --seed
```

其中提示输入的地方都输入yes即可。最后应该会报错，这时需要修改AppServiceProvider.php

修改`WebStack-Laravel/app/providers/AppServiceProvider.php`：

```php
<?php
 
namespace App\Providers;
 
use App\Observers\SiteObserver;
use App\Site;
use Encore\Admin\Config\Config;
use Illuminate\Support\Facades\Schema;
use Illuminate\Support\ServiceProvider;
 
class AppServiceProvider extends ServiceProvider
{
    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        Schema::defaultStringLength(191);
        Site::observe(SiteObserver::class);
 
        $table = config('admin.extensions.config.table', 'admin_config');
        if (Schema::hasTable($table)) {
            Config::load();
        }
    }
 
    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {
        //
    }
}
```

然后再次执行

```shell
php artisan key:generate
php artisan migrate:refresh --seed
```

------

**这里我出现了一个问题：**

提示我admin_config已存在，应该是之前执行`php artisan migrate:refresh --seed`时导致的 或是在创建站点时初始化导致的。

[![image-20200613121516612](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165407.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165407.png)

故在宝塔面板删除当前的数据库，然后重新创建了一个。

下图为重新创建的，这里貌似宝塔要求数据库名与用户名要相同。

当然这里的数据库名、用户名、密码对应着上述修改 `.env`文件的内容。

[![image-20200613122220972](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165411.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165411.png)

创建好后点击右边的工具确认没有`admin_congfig`，正常来讲应该是全空的。

[![image-20200613122324854](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165413.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165413.png)

然后执行

```shell
php artisan key:generate
php artisan migrate:refresh --seed
```

------

## 为站点赋予权限

打开网站进行查看以及后面一些操作时，会经常提示报错信息，都是XXX拒绝访问等等。

故直接在宝塔上赋予站点目录所有权限。

[![image-20200613124738186](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165418.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165418.png)

## 效果

[![image-20200613130043246](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165420.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165420.png)

## 后台管理

在主页的url后面加上`/admin`即可进入。

[![image-20200613124140962](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165423.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165423.png)

默认的用户名与密码都是admin，进去后可以修改

[![image-20200613124424354](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165427.png)](https://gitee.com/lluuiq/blog_img/raw/master/img/20200619165427.png)

## 清除原有站点（可选）

执行下方语句进行清除。

```shell
php artisan webstack:clean
```