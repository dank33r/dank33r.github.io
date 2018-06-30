---
title: WIN10环境下安装Tensorflow
date: 2018-06-29 23:22:30
tags: Tensorflow
categories: 人工智能
---

官方安装指南：https://www.tensorflow.org/install/install_windows

官方链接对于Tensorflow在Windows10平台的安装已经介绍的比较详细了，这里只是强调几个需要注意的地方。
1. Anaconda可以安装最新版本，而不是像以前所说必须安装Python3.5版。Anaconda需要在CUDA安装完成后再安装。
2. CUDA需要安装9.0版，如果没有安装VS那么不需要勾选和VS编译环境集成的选项，否则会安装失败。
3. CUDA安装完成并不需要用户手工设置%PATH%，这点和安装指南不同。
4. Cudnn的安装文件需要手工复制到CUDA安装目录。
<!--more-->
5. Tensorflow在Anaconda中的安装过程如下
```
> conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
> conda config --set show_channel_urls yes
> conda create -n tensorflow-gpu python=3.6
> conda activate tensorflow-gpu
> python -m pip install --upgrade pip
> pip install -i https://pypi.tuna.tsinghua.edu.cn/simple --upgrade tensorflow-gpu
```