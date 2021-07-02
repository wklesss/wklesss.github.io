---
title: linux安装python3.9
tags:
  - linux
  - python
cover: 'https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210702105845.jpeg'
categories: 工具使用
abbrlink: '324e8246'
date: 2021-07-02 10:56:21
---

# 安装环境

![image-20210702111815035](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210702111815.png)

#### 1. 查看当前 python 版本

![image-20210702110010149](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210702110010.png)

可以看到执行 python3，默认是3.8.10

#### 2. 安装依赖包

```
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc make libffi-devel

```

#### 3. 下载源码包

```
wget https://www.python.org/ftp/python/3.9.5/Python-3.9.5.tgz

```

我是下载的最新的 python3.9，如果想安装其他版本，去 [python 官网下载页面](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.python.org%2Fdownloads%2F)下载对应的版本即可。 但是这个下载链接比较慢，我是用迅雷下载到本地之后，再 scp 到服务器的。

#### 4. 解压安装

```
# 解压压缩包
tar -zxvf Python-3.9.5.tgz

# 进入文件夹
cd Python-3.9.5

# 配置安装位置
./configure prefix=/usr/local/python3

# 安装
make && make install

```

如果最后没提示出错，就代表正确安装了，在 / usr/local / 目录下就会有 python3 目录

#### 5. 添加软连接

```
#添加python3的软链接 
ln -sf /usr/local/python3/bin/python3.9 /usr/bin/python3 

#添加 pip3 的软链接 
ln -sf /usr/local/python3/bin/pip3.9 /usr/bin/pip3

```

![image-20210702112333874](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210702112333.png)

