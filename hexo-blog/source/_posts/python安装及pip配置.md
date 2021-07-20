---
title: python安装及pip配置
tags:
  - Python
  - pip
  - ubuntu
cover: >-
  https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/photo-1526925539332-aa3b66e35444
categories: 工具使用
abbrlink: fc64799c
date: 2021-07-20 21:08:13
---

> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.cppcns.com](http://www.cppcns.com/jiaoben/python/369691.html)

> 这篇文章主要介绍了 Ubuntu16 安装 Python3.9 的实现步骤，文中通过示例代码介绍的非常详细，对大家的学习或者工作具有一定的参考学习价值，需要的朋友们下面随着小编来一起学习学习吧

这篇文章主要介绍了 Ubuntu16 安装 Python3.9 的实现步骤，文中通过示例代码介绍的非常详细，对大家的学习或者工作具有一定的参考学习价值，需要的朋友们下面随着小编来一起学习学习吧

我是使用源码编译的方式安装的，网上有的可以添加 ppa 源进行在线安装，但我试[编程客栈](http://www.cppcns.com/ "编程客栈")了行不通，所以还是采用源码安装

### 1、安装编译依赖项

```
sudo apt install -y wget build-essential libreadline-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev

```

有的博文说在这一步需要升级`pip`，但我认为没必要，因为安装好 `[python](http://www.cppcns.com/jiaoben/python/ "python")`后里面有最新的`pip`，修改软链接即可

### 2、下载源码包

下载你需要安装的包，官网下载会特别慢，我是用手机先从官网下载之后传到电脑上的，速度快很多

```
wget https://www.python.org/ftp/python/3http://www.cppcns.com.9.0/Python-3.9.0b4.tgz
 
tar -zxvf Python-3.9.0b4.tgz # 解压源码包

```

### 3、编译安装

进入到刚才解压的包目录中

```
#编译参数设置
./configure --prefix=/usr/local/python3
 
#编译
make
 
#安装
sudo make install

```

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210720211343.png)

出现这个提示表示安装成功，下面设置软链接

### 4、设置软链接

执行`ll /usr/local/python3/bin`查看安装后的可执行文件，其中`python3`是指向`python3.9`的软链接，`pip3`和`pip3.9`里面的内容一样，只需要在`/usr/bin/`目录下添加这两个文件的软链接即可

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/obipjhvkr0q.jpg)

执行`ll /usr/bin | grep python`先查看之前`python`对应软链接，每个人情况都不一样，但设置方法是一样的，删除原来的软链接，然后重新指定即可  

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/f2b3j1somvq.jpg)

```
sudo rm python
sudo rm python3 #并不会删除 python2.7 和 python3.5
 
sudo ln http://www.cppcns.com-s /usr/local/python3/bin/python3.9 /usr/bin/python3
sudo ln -s /usr/local/python3/bin/python3.9 /usr/bin/python
 
#为 pip 设置软链编程客栈接
sudo ln -s /usr/local/python3/bin/pip3.9 /usr/bin/pip3
sudo ln -s /usr/local/python3/bin/pip3.9 /usr/bin/pip

```

执行`ll /usr/bin | grep python`和`ll /usr/bin | grep pip`查看设置后的软链接，设置 ok  

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/p4rh02bndfp.jpg)  

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/i1shlnlr0y3.jpg)

### 5、pip 错误处理

安装完成以后还有个事就是在使用`pip`安装第三方库会出现问题，执行`pip list`，如下：  

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/4nobu3ajbc1.jpg)  

意思是在执行`lsb_release -a`这个命令出现问题，`lsb_release`这个文件在目录`/usr/bin`下

有的博文说删了这个文件就 ok，不删也可以，执行`sudo vi /usr/bin/lsb_release`将第一行中的`python3`改为`python3.5`，因为之前的`python3`是指向`python3.5`的，让它使用原来的解释器即可。然后再执行`pip list`，已经没有问题了

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/l3rm0vpmifm.jpg)  
![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/mvcop2qiuao.jpg)

### 6、添加第三方库安装源

玩`python`需要安装很多的第三方模块，直接用`pip`下载安装会比较慢，可添加国内镜像源地址，下载的文件时一样的，但速度会快很多。配置方法：

a. 找到下列文件，如果不存在，之间创建相应目录和文件即可

b. 在上述文件中添加或修改：

```
[global] 
index-url=http://pypi.douban.com/simple/
[install]
trusted-host=pypi.douban.com

```

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/eev2ozkeneg.jpg)
