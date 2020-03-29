---
title: python3_GUI基础(tkinter)
comments: true
toc: true
top: false
categories:
  - - 笔记
    - python
tags:
  - python
  - GUI
  - tkinter
date: 2020-03-28 11:43:27
---

python3的GUI编程笔记，使用tkinter库

<!-- more -->

## 导包

python的tkinter库是自带的，无需安装，直接导入即可

```python
from tkinter import *
```

## 创建窗口

```python
window = Tk()
```

设置窗口的名称

```python
window.title('窗口的名称') 
```

通过mainloop()来运行

```python
# 进入一个死循环来监听事件
window.mainloop()
```

![image-20200328122847732](https://gitee.com/lluuiq/blog_img/raw/master/img/20200328122851.png)

改变窗口大小与位置

```python
# 窗口的大小 宽x高, 'x' 为字母x， +700表示打开窗口时距屏幕左边的距离，-700则距离右边的距离，+300的为距屏幕上方的距离，-300为距屏幕下方的距离
window.geometry('400x200+700+300')
```

![image-20200328125411881](D:\blog\source\_posts\新建文章.assets\image-20200328125411881.png)

**注**：接下来创建组件都要放在mainloop()前面，让mainloop()最后运行

即GUI代码应该为：

```
【导包】
......
......
创建组件以及监听事件等代码块
......
......

【窗口名】.mainloop()
```

## 创建按钮

```python
btn = Button(
    master=window,  # 指定容器
    text='按钮上的文本',
    fg='red',  # 文本的颜色
    font='Arial',  # 文本的字体

    # 设置宽度与高度，未设置则自适应
    height=1,  # 按钮的高度
    width=11,  #按钮的宽度

    padx=10, #按钮的x轴内边距
    pady=10, # 按钮的y轴内边距
    activebackground= 'green', #鼠标点击时按钮的背景色
    activeforeground = 'blue', # 鼠标点击时按钮文本的颜色
    bd = 3, # 按钮边框的大小，越大则按钮越突出
    bg = 'gray', #按钮的背景色
    # image =  # 按钮背景改为图片

    # 按钮的3D效果,默认FLAT
    relief= FLAT, # FLAT、SUNKEN、RAISED、GROOVE、RIDGE
    # 按钮的状态，默认NORMAL
    state = NORMAL,

    wraplength = 100, # 每行最多显示多少字
    #当文本多行时的对齐方式
    justify = CENTER, # LEFT, RIGHT, CENTER
)

# 用pack()将组件压缩放在窗口中
btn.pack()
```

## 创建消息框

