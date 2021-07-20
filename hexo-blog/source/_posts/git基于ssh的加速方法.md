---
title: git基于ssh的加速方法
tags:
  - github
  - ssh
  - proxy
cover: >-
  https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/photo-1591608516485-a1a53df39498
categories: 工具使用
abbrlink: 4684b22f
date: 2021-07-20 19:20:14
---

> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.cnblogs.com](https://www.cnblogs.com/StevenWind/p/11735352.html)

**背景：**

刚才在使用 github 时，发现直接下载 zip 的时候，速度非常快，但是使用 git clone 时发现速度只有 15kb/s 左右。这一定是不合理。

想着使用梯子，下载速度一定会有所提升，结果发现速度直接使用全局代理是不能有帮助。

所以花了一些时间研究了以下。

**预备知识：**

首先，git clone 有两个种，一种是基于 http 的 (暂把其代号设为 A，便于后续分类讨论)，另一种是基于 ssh 的 (暂把其代号设为 B，便于后续分类讨论)。

使用形式分别为：

　　git clone https://github.com/stevenlovegrove/Pangolin.git

　　gti clone git@github.com:stevenlovegrove/Pangolin.git　　

另外，基于 shadowsocks 的代理，也是有两种方法的，一种是 http(暂把其代号设为 1，便于后续分类讨论)，另一只是 socks5(暂把其代号设为 2，便于后续分类讨论) 的。

如下图我的协议就是 socks5 的。

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/959011-20191026153840907-1303696680.png)

好的，一切准备就绪，因为现在有两种 git 协议 (A,B)，两种代理协议 (1,2)，所以有四种设置方法。

**A1: 基于 http 的 git 与基于 http 的代理**

好的，一切准备就绪，因为现在有两种 git 协议 (A,B)，两种代理协议 (1,2)，所以有四种设置方法。

```
git config --global http.proxy "http://127.0.0.1:1080"
git config --global https.proxy "http://127.0.0.1:1080"


```

**A2: 基于 http 的 git 与基于 socks5 的代理**

```
git config --global http.proxy "socks5://127.0.0.1:1080"
git config --global https.proxy "socks5://127.0.0.1:1080"



```

**B1: 基于 ssh 的 git 与基于 http 的代理**

   修改~/.ssh/config 文件，如在 ubuntu 下使用: gedit ~/.ssh/config

　添加如下内容:

Host github.com  
HostName github.com  
User git  
ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=1080

　添加完毕，记得保存

**B2: 基于 ssh 的 git 与基于 socks5 的代理**

    修改~/.ssh/config 文件，如在 ubuntu 下使用: gedit ~/.ssh/config

　添加如下内容:

Host github.com  
HostName github.com  
User git  
ProxyCommand nc -v -x 127.0.0.1:1080 %h %p

