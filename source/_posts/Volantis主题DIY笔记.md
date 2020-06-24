---

title: Volantis主题DIY笔记
date: 2020-03-17 12:29:46 
comments: true
toc: true
top: false

categories: 
- [笔记]
tags: [hexo]
---

主题首页：[Volantis](https://volantis.js.org/)

记录一些DIY的过程

<!-- more -->

## 主题文件目录

在主题的根目录下。

layout为页面、卡片、各部位的布局代码

source存放css、js、字体、图片等代码与资源

_config.yml为主题配置文件

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023003.png)

## 顶部导航栏

设置顶部导航栏始终显示。

打开source/css/_layout/navbar.styl

找到最下面的代码，将其注释

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200326081504.png)

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

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023005.png)

修改后：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023006.png)

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

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023007.png)

```yml
base: 10px
```

该方法是同时修改卡片之间的距离以及卡片内容与卡片边框之间的距离。

若要分开修改需要到css文件逐一修改，可以用该方法添加一个新的变量来传参。

例如：

在gap中添加一个变量，变量名自定义，这里用**test**示例，后面的大小为要设置的大小。

```yml
test: 10px
```

接着打开source/css/_defines/layout.styl，找到gap的设置

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023008.png)

添加自定义的变量

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023009.png)

```stylus
$test = convert(hexo-config('style.gap.test')) || 16px
```

$test为CSS设置中的变量名，`style.gap.test`中的test为在_config.yml中设置的变量名，||后面为默认值

设置完成后，在对应的CSS设置中仅需要将间距大小改为`$test`，就会使用设置中test的值

## 封面界面去掉搜索

效果如图

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023016.png)

打开layout/_cover/index.ejs

找到如图所示代码，将其注释

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023010.png)

## 添加QQ在线联系

打开_config.yml，搜索social，找到社交功能设置部分

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023011.png)

添加内容如下

```yml
- icon: fab fa-qq
  url: http://wpa.qq.com/msgrd?v=3&uin=【你的QQ号】&site=qq&menu=yes
```

第一次点击会提示未开通，到提示网站登入一次即可。

## 将侧边栏移动到左边

打开layout文件夹，对以下文件统一修改

![image-20200317161443443](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023012.png)

打开一文件后，搜索代码

```ejs
<%- partial('_partial/side') %>
```

将该行代码复制到第一行代码`<%- partial('_pre') %>`的下方，然后将原来位置的代码注释（方便以后若需要的话改回），示例：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023013.png)

然后修改CSS文件，

打开source/css/_layout/main.styl

搜索`.l_main`，找到`padding-right`，将right改为left，使原本的右边距变为左边距

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023014.png)

修改后为

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023015.png)

为适应手机端，还需要修改此处

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023017.png)

若想要手机端的卡片有外边距，则将`padding-right: 0`按需求修改边距 ，例如若想要左右边距都为10px，则应该改成

```
padding-right: 10px
padding-left: 10px
```

效果如图：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023021.png)

若满意现在的效果则到此即可。接下来将侧边栏移动到网页的边缘处，然后让文章列表、其余页面的主要内容居中。

**注：**修改后，在主题的配置文件中的最大宽度max_width将只修改页面内容卡片的宽度

### 进一步修改

首先在_config.yml中修改最大宽度为100%，但注意这样会导致顶部导航栏的宽度也随之变成100%。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023018.png)

打开source/css/_layout/main.styl，将`.body-wrapper`中的`justify-content: space-between`注释。

该语句会使页面内的flex布局为flex项目之间的距离相等，若只有两个项目的情况下会导致一个在最左边，一个在最右边。注释后会采取默认的布局方式即左对齐。

![image-20200326234008039](https://gitee.com/lluuiq/blog_img/raw/master/img/20200326234018.png)

页面内容的修改在该文件中的`.l_main`，将width中的100%调小以更改页面内容的宽度，修改padding-left来更改与侧边栏的距离。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023020.png)

侧边栏的宽度可以在source/css/_defines/layout.styl中进行修改

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023022.png)

## 修改透明度

使用css两种更改透明度方法，其中透明度取值为0~1，越小则透明程度越高

1. 使用 background-color:rgba(R,G,B,透明度)
2. 使用 opacity: 透明度

若使用rgba，则需要传入RGB颜色代码，并且修改的仅有div元素的背景透明度

若使用opacity，则只需要传入透明度，修改的是整个div元素的透明度（包括图片、文字等也会变透明）

在source/css中创建一个新的stylus文件，名字随意

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324023023.png)

编辑内容，其中颜色代码、透明度自行修改

```stylus
.widget
  background-color:rgba(255,255,255,0.9)

.post
  background-color:rgba(255,255,255,0.9)
```

然后打开source/css/style.styl，插入引用语句

```stylus
@import 'diy_css.styl'
```

同理可以用此方式进行CSS的自定义，可以做到在不修改原本代码的情况下更改css

## 实现pjax

感谢大佬的博客开源，让我能参考源代码进行修改：[Material X主题pjax使用](https://stevenmhy.tk/archives/db1997ec.html) 

感谢大佬的讲解 ：[用pjax让你的页面加载飞起来!](https://sunhang.top/2019/12/20/pjax/)

---

在layout/_partial/head.ejs的末尾 `</head>`的上方引用pjax

![image-20200325222920909](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200325222930.png)

```html
<script src="https://cdn.jsdelivr.net/npm/pjax/pjax.js"></script>
```



在layout/layout.ejs的末尾`</body>`的上方插入代码

```js
<script>
var pjax = new Pjax({
  elements: "a",
  selectors: [
    "title", //pjax加载标题
    ".l_main", //pjax加载主内容
    ".l_side", //pjax加载侧边栏
    ".switcher .h-list", // 使手机端的搜索框与菜单栏生效
  ]
})
</script>
```

![image-20200325224042143](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200325224044.png)

elements选择触发器，即点击什么来触发pjax（只能用a或者form），a为链接。

selectors根据css选择器来选择更新的节点（即当触发elements时哪些内容会刷新，其余部分保持不变）

可以用节点、类、id等选择元素。用法参考：[CSS 选择器](https://www.runoob.com/cssref/css-selectors.html)

这里我设置的为：点击链接，则刷新标题、类为`l_main`与`l_side`的元素（页面内容与侧边栏）会刷新，其余不变。

### pjax优化-自动生成Fancybox

在定义pjax的脚本代码中插入语句（放在\<script>与\</script>中）

```js
//加载fancybox
function LoadFancybox(){
  $(".article-entry").find("img").each(function () {
    //渲染fancy box
    var t = document.createElement("a");
    $(t).attr("data-fancybox", "gallery"),
    $(t).attr("href", $(this).attr("src")),
    $(t).attr("margin","0 auto"),
    $(this).wrap(t)
  })
}

// pjax加载结束后执行函数
document.addEventListener('pjax:complete', function (){
  LoadFancybox();
});

// 窗口监听load(加载、刷新)事件，执行LoadFancybox()函数
window.addEventListener('load',function(){
  LoadFancybox();
});
```

插入后结果如图：

![image-20200327002931652](https://gitee.com/lluuiq/blog_img/raw/master/img/20200327002933.png)

修改后发现实现了fancybox，但是图片不再居中，故进行修改。

打开source/css/_layout/main.styl

搜索`img` 找到位于l_main>post>a下的img，将`display: inline`注释

![image-20200326104120122](https://gitee.com/lluuiq/blog_img/raw/master/img/20200326112446.png)

---

**BUG：**

- 放大图片再关闭后，页面位置与放大前不对应，会返回到放大前一张图片时的位置 。



**更新：**

将原来代码中的`$(t).attr("data-fancybox","gallery"),`中的`"gallery"`改为`""`

![image-20200625071949974](https://gitee.com/lluuiq/blog_img/raw/master/img/image-20200625071949974.png)

---

实现pjax后发现导航栏在点击不同部分时，主题的下划线不会改变，进行修改没有修改成，故直接将CSS代码注释

打开source/css/_layout/navbar.styl 搜索`&:active,&.active` 将该部分代码注释

![image-20200327013730981](https://gitee.com/lluuiq/blog_img/raw/master/img/20200401152132.png)

### pjax刷新评论

**问题**：实现pjax后发现通过pjax刷新页面后评论无法成功加载，推测是因为评论由js脚本引入，pjax刷新页面不会加载js。

**解决思路**：当pjax执行完成后再次调用评论js脚本来生成评论。

在pjax脚本中插入以下代码，其中调用脚本的方式有两种，用哪一个都可以。

```js
function LoadValine(){
    // 两种调用方式，一个调用配置里的js路径，一个调用本地，用哪个都可以
 // $.getScript("<%= theme.comments.valine.js %>", function() {
    $.getScript("/js/Valine.js", function() {
        
      // 生成评论的代码
      var GUEST_INFO = ['nick','mail','link'];
      var guest_info = '<%= theme.comments.valine.meta %>'.split(',').filter(function(item){
        return GUEST_INFO.indexOf(item) > -1
      });
      var notify = '<%= theme.comments.valine.notify %>' == true;
      var verify = '<%= theme.comments.valine.verify %>' == true;
      var valine = new Valine();
      valine.init({
        el: '#valine_container',
        notify: notify,
        verify: verify,
        guest_info: guest_info,
        <% if (page.valine && page.valine.path) { %>
          path: "<%= page.valine.path %>",
        <% } else if (theme.comments.valine.path) { %>
          path: "<%= theme.comments.valine.path %>",
        <% } %>
        appId: "<%= theme.comments.valine.appId %>",
        appKey: "<%= theme.comments.valine.appKey %>",
        placeholder: "<%= (page.valine && page.valine.placeholder) ? page.valine.placeholder : theme.comments.valine.placeholder %>",
        pageSize:'<%= theme.comments.valine.pageSize %>',
        avatar:'<%= theme.comments.valine.avatar %>',
        lang:'<%= theme.comments.valine.lang %>',
        visitor: '<%- theme.comments.valine.visitor %>',
        highlight:'<%= theme.comments.valine.highlight %>'
      })
	});
}
```

然后在监听pjax完成后的函数里调用函数

```js
// 加载pjax后执行的函数
document.addEventListener('pjax:complete', function (){
    LoadFancybox();
    // 调用刚刚设置的函数
    LoadValine();
});
```

结果应该如图：

![image-20200401152044289](https://gitee.com/lluuiq/blog_img/raw/master/img/20200401152053.png)

**源码位置：**`layout\_partial\scripts.ejs`，上述代码中生成评论的部分即红框内的部分

![image-20200401152329756](https://gitee.com/lluuiq/blog_img/raw/master/img/20200401152332.png)

## 添加百度统计

首先到[百度统计](https://tongji.baidu.com/)注册帐号，然后到管理界面，新增网站

![image-20200401125207533](https://gitee.com/lluuiq/blog_img/raw/master/img/20200401152138.png)

新增后，会给一段代码，将其复制，并在外面加上ejs模板的语句

```ejs
<% if (theme.baidu_analytics){ %>
    <script>
        var _hmt = _hmt || [];
        (function() {
          var hm = document.createElement("script");
          hm.src = "https://hm.baidu.com/hm.js?【你的key】";
          var s = document.getElementsByTagName("script")[0]; 
          s.parentNode.insertBefore(hm, s);
        })();
    </script>
<% } %>
```

打`layout\_partial\scripts.ejs`，将该段代码插入到最后

![image-20200401125553039](https://gitee.com/lluuiq/blog_img/raw/master/img/20200401152144.png)

再打开`_config.yml`，加入一条语句

```yml
baidu_analytics: true
```

因为用js文件加载的方式，所以百度统计上的代码检查功能失效，需要手动检查。

保存后，打开网站，按F12打开开发者工具，然后刷新页面，在js文件中看到以hm开头的js文件说明配置成功

![image-20200401125819253](https://gitee.com/lluuiq/blog_img/raw/master/img/20200401152147.png)

