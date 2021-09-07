---
title: zsh配置
tags:
  - zsh
  - linux
  - terminal
  - mac
  - wsl
  - shell
cover: 'https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/photo-1607877361964-bf792b65e593'
categories: 工具使用
abbrlink: 82d44a65
date: 2021-08-23 17:21:23
---

> 环境为wsl-ubuntu18
>
> ![image-20210907170638965](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/image-20210907170638965.png)

## 准备工作

`sudo apt update &&  sudo apt upgrade`

## zsh安装

在安装 oh-my-zsh 之前，首先需要安装好`zsh`：

```
apt install -y zsh
```

切换 shell 为 zsh：

```
chsh -s /bin/zsh
```

重启终端：

```
# 查看当前shell
echo $SHELL
```

输出`/bin/zsh`表示成功

## oh-my-zsh安装

- Install oh-my-zsh via curl

-  $ ` sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

- Install oh-my-zsh via wget

  $ `sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"`

安装成功出现如下界面

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/v2-fb93443e858f4fe0a7888a0e8eb8c83c_r.jpg)

## 主题配置

`oh-my-zsh`的主题非常丰富，可以用如下命令查看已有主题：

```
ls .oh-my-zsh/themes
```

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/v2-1716810cbaf0ccf2f9f63c887cbbc148_r.jpg)

个人比较喜欢简单的，因此用了`ys`主题，进入`.zshrc`配置文件进行修改

```
vim ~/.zshrc
```

将ZSH_THEME改为`ZSH_THEME="ys"`，`:wq`保存退出

`source .zshrc`使主题生效

## 插件安装

### zsh-autosuggestions

这是一个命令自动补全插件，当你输入命令的几个字母，它会自动根据历史输入进行自动补全，然后按`→`，安装也很简单：

```
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
vim ~/.zshrc
# 加入插件列表
plugins=(
  git
  zsh-autosuggestions
)
source ~/.zshrc
```

### zsh-syntax-highlighting

这个插件的主要作用就是在提高颜值（高亮你的 zsh 可用命令），安装如下：

```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
vim ~/.zshrc
# 加入插件列表
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
)
source ~/.zshrc
```

效果如下图：

![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/v2-c409188909175ad31fe9a1ff15d2b143_r.jpg)

### autojump

这款插件基本上算是必备插件了，在终端操作里面比较常用的算是文件夹之间的切换，这款插件极大地简化了路径跳转的操作，在一键直达的功能下，自动补全也就一般般了哈

先安装：

```
apt install autojump-zsh
chmod 777 /usr/share/autojump/autojump.bash
echo "/usr/share/autojump/autojump.bash" >> ~/.zshrc
source ~/.zshrc
```

效果如下：

<img src="https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/v2-fffd39bdd01464f8df7ad17fa6c7ada0_r.jpg" style="zoom:50%;" />

以前的`cd code`现在可以直接`j c`，路径越长，该插件效果就越明显

### incr

`incr`是一款自动提示插件，功能非常强大，官网演示 demo，感受一下：

<img src="https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/v2-a9a9cc115d4fc56dce323fd3db1e1128_b.gif"  />

安装：

```
wget http://mimosa-pudica.net/src/incr-0.2.zsh
mkdir ~/.oh-my-zsh/plugins/incr
mv incr-0.2.zsh ~/.oh-my-zsh/plugins/incr
echo 'source ~/.oh-my-zsh/plugins/incr/incr*.zsh' >> ~/.zshrc
source ~/.zshrc
```

可以开心的敲命令行了~

