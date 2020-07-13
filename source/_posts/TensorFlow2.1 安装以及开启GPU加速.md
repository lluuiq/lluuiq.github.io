---
title: TensorFlow2.1 安装以及开启GPU加速
comments: true
toc: true
top: false
mathjax: false
categories:
  - - 笔记
tags:
  - TensorFlow2
  - 神经网络
date: 2020-07-03 05:00:19
---

记录下TensorFlow2的安装以及开启GPU加速功能。

使用Anaconda3的conda进行安装。

<!--more-->

## 查看GPU驱动版本与升级

首先确定系统环境变量path里有下方路径，没有的话添加进去。

```
C:\Program Files\NVIDIA Corporation\NVSMI
```

然后在终端运行 `nvidia-smi`

![image-20200703051133275](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703051133275.png)

这里可以看到我的`NVIDIA-SMI`版本为382.05 需要升级

打开 `GeForce Experience`更新驱动。

![image-20200703051745498](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703051745498.png)



## 安装tensorflow-gpu并配置

1. **使用conda创建一个虚拟环境并安装tensorflow-gpu**

```
conda create -n tf2 tensorflow-gpu
```

其中 -n 后面的 `tf2`是环境的名称，可自定义。

中间出现输入 Y/N 的时候可以检查一下要安装的包，确认一下tensorflow版本为2.1。

并不推荐换国内源安装，我换源安装结果显示的是tensorflow1.x版本。

<br>

2. **安装完成后 启用新环境**

```
conda activate tf2
```

3. **在新环境中安装一下ipython**

```
pip install ipython
```

4. **安装 nb_code，使得 jupyter notebook可以切换kernel**

首先关闭tf2环境，在tf2环境时输入

```
conda deactivate
```

然后安装nb_code

```
pip install nb_conda
```

接着修改一下配置文件，`Anaconda3\Lib\site-packages\nb_conda\envmanager.py`

找到如下所示的代码块

![image-20200703110217107](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703110217107.png)

修改为 

```python
return {
	"environments": [root_env] + [get_info(env) for env in info['envs'] if env !=root_env['dir']]
}
```

然后就可以打开jupyter notebook切换kernel了。

## jupyter notebook 测试tensorflow

在新建notebook时选择环境

![image-20200703110452754](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703110452754.png)

或者在已有的notebook中修改环境

![image-20200703110527821](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703110527821.png)



查看版本：

```python
import tensorflow as tf
tf.__version__
```

![image-20200703105923890](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703105923890.png)

查看是否启用加速

```
from tensorflow.python.client import device_lib
print(device_lib.list_local_devices())
```

![image-20200703105858744](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703105858744.png)

## pycharm测试tensorflow

新建一个project，选择已存在的环境，可以看到当前指定的为默认环境，而不是tf2环境，在后方点击 `...` 图标选择。

![image-20200703111052850](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703111052850.png)

我这里点开后自动选择了虚拟环境，如果没有参考该路径选择自己的。并勾选全工程生效。

![image-20200703111141985](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703111141985.png)

等待更新

![image-20200703111209025](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703111209025.png)

输入

```python
import tensorflow as tf
print(tf.__version__)
```

执行后即可看到运行成功。

![image-20200703111414478](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703111414478.png)

![image-20200703111421743](C:\Users\84452\AppData\Roaming\Typora\typora-user-images\image-20200703111421743.png)

