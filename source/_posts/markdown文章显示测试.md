---
title: markdown文章显示测试 
date: 2020-02-20 18:56:45 
mathjax: true # false: 不渲染, true: 渲染, internal: 只在文章内部渲染，文章列表中不渲染
comments: true
toc: true
top: false

categories: 
- [笔记]
tags: [markdown,hexo]
---
# 这是一个测试用的文档，该句也是一级标题

## 这是二级标题

### 这是三级标题

#### 这是四级标题

##### 这是五级标题

接下来是阅读更多 <!--more-->

接下来的测试内容用二级标题标注

## 分隔符：

第一行，接下来加入分隔符

---

第二行，与第一行之间有分隔符

## 加粗：

正常文字 vs **加粗文字**

## 斜体：

正常文字 vs *斜体文字

## 删除线：

正常文字 vs ~~删除线文字~~

## 代码框：

正常文字 vs `代码框内文字`

## 高亮：

正常文字 vs ==高亮==

## 添加注释：

正常的内容正常[^注释]的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容正常的内容。

[^注释]: 注释内容注释内容注释内容

## 角标：

**上角标：**写个X的平方+Y的平方：x^2^+y^2^

**下角标：**写个H2O：H~2~O

## 数学公式：

公式写法：

```
x^2 + x^2 = 2x 
\\
f(x)=\frac{1}{\sqrt{2\pi\sigma}}exp(-\frac{(x-\mu)^2}{2\sigma^2})
```

效果如下：
$$
x^2 + x^2 = 2x 
\\
f(x)=\frac{1}{\sqrt{2\pi\sigma}}exp(-\frac{(x-\mu)^2}{2\sigma^2})
$$

## 列表：

**有序列表：**

1. 第一行

2. 第二行

   1. 第二行的子行1号

   2. 第二行的子行2号

      突然无序的行

      3.忽然有序的行

**无序列表：**

+ 第一行
+ 第二行

## 表格：

| one   | two  | three |
| ----- | ---- | ----- |
| two   |      |       |
| three |      |       |
| four  |      |       |

## 链接：

[百度](https://www.baidu.com)

## 代码块：

markdown原生：

```python
import pandas as pd
import plotly.graph_objs as go
import plotly.offline as py
from plotly import subplots
import random

# 添加isPass列，得分为60及以上的学生设为几个，否则为不及格
df['isPass']=df['score'].apply(lambda x: '及格' if x>=60 else '不及格')
# 将及格的学生赋值给 df_isPass
df_isPass = df[df['isPass'] == '及格']
    
```

Volantis2.2.1主题代码块：

![image-20200326082338331](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200326082340.png)

{% codeblock 标题  lang:python%}
code snippet
{% endcodeblock %}

## emoji：

我:heart:你，:kiss:

## 引用：



正常的内容

> 引用的内容

## 图片测试：

正常内容。

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324021616.png)

正常内容。

## Tab测试：

{% tabs tab-id %}

<!-- tab 第一个tab的名字 -->

```
代码框
```

正常文字

<!-- endtab -->

<!-- tab 第二个tab的名字 -->

正常的文字

插入图片：

![mark](https://cdn.jsdelivr.net/gh/lluuiq/blog_img/img/20200324021616.png)

<!-- endtab -->

{% endtabs %}

---

暂时想到了这么多，如有遗漏希望评论留言帮忙补充(~~估计也不会有人这么闲能看这个测试看到这里~~)，感谢。