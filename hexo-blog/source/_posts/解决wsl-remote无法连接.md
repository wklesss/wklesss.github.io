---
title: 解决wsl-remote无法连接
tags:
  - wsl
  - ubuntu
  - vscode
cover: >-
  https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/photo-1607799131608-9a22dd60e25e
categories: 工具使用
abbrlink: dc809001
date: 2021-07-20 19:48:45
---

### 环境

系统：windows10  
linux 子系统：ubuntu18.04 LTS  
vscode：1.42.1  
remote-wsl：0.42.3

### 问题

在连接 linux 子系统时报错：

```
sh: 1: /mnt/c/Users/li/.vscode/extensions/ms-vscode-remote.remote-wsl-0.42.3/scripts/wslServer.sh: Permission denied
VS Code Server for WSL closed unexpectedly.

```

### 解决方案

打开 linux 子系统，执行下列命令切换到 scripts 目录：

```
cd /mnt/c/Users/XXX/.vscode/extensions/ms-vscode-remote.remote-wsl-0.42.3/scripts

```

其中`XXX`为你的用户名  
然后执行命令：

```
chmod +x *

```

再次连接即可成功。

### 参考

[cant connect to wsl-remote](https://github.com/microsoft/vscode-remote-release/issues/2126)
