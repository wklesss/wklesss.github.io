---
title: 快速搭建多终端同步的hexo博客
categories: 工具使用
tags:
  - hexo
  - github
  - blog
cover: 'https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520183938.jpeg'
abbrlink: dc1a6467
date: 2021-05-19 00:19:53
---
最终实现的效果是在 GitHub 上只需要一个仓库，实现可在多终端同步自己的个人博客。

废话不多说，下面直入主题。

1. 前提条件

-------

*   拥有自己的 GitHub 账号
*   本地终端安装了 git
*   安装了 Nodejs

2. github 上创建个人主页

-----------------

在自己的主页上新建一个仓库，仓库的名字要和自己的用户名保持一致。如我的用户名是 kakadee, 那么仓库的名字应该是 kakadee.github.io。这样该仓库地址即默认作为你 git 的个人主页。其他选项按默认的进行。

![20210519004925](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520182236.png)

3. 从远程拉取仓库到本地

-------------

这时候你 git 上的仓库是一个空的项目或者只含有一个 README.md. 在你本地合适的文件夹 clone 你的项目。

这里我使用 SSH 的方法 clone，当然也可以使用 HTTPS 的方法，只要能拉下来代码就可以。

```
git clone git@github.com:kakadee/kakadee.github.io.git
```

4. 本地 hexo 配置 （核心）

------------------

### 创建 hexo 分支

此时在本地上使用`git branch`查看只有`master`一个分支。  
使用`git checkout -b hexo`创建`hexo`分支并将其作为默认分支。

![22](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520175419.jpeg)

### 备份原始的. git 文件

执行`ll -a`查看该目录下所有文件，发现有一个`.git`的文件夹。该`.git`文件夹会在后面 hexo 安装的过程中被覆盖，导致没法 push 到 hexo 分支, 所以要先备份一下并在最后恢复。

![33](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520175416.jpeg)

执行如下命令进行备份。

```
cp -r .git .origingit
```

![4](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520175410.jpeg)

### 安装 hexo 并初始化

依次执行如下命名：

```
npm install hexo
hexo init
npm install
npm install hexo-deployer-git --save
```

执行完毕后文件夹如下：

![20210519005145](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520182320.png)

可以看到原来的`.git`文件夹已经不见了，所以这时候要将`.git`文件由`.origingit`复制回来。

```
cp -r .origingit .git
```

这样就不会影响之后的 push 了。

### 修改_config.yml 中的 deploy 参数

![20210519005151](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520182401.png)

repository 中填写自己 git 仓库的地址（https 的也可以）。  
branch 应该设置为 master.  
需要注意的是，在配置所有的_config.yml 文件时（包括 theme 中的），在所有的冒号: 后边都要加一个空格，否则执行 hexo 命令会报错。

### 将 hexo 分支 push 到远程 hexo 分支上

依次执行:

```
git add .
git commit -m "xxx"
git push origin hexo
```

此时 hexo 配置文件都被 push 到远程的 hexo 分支上了。

> 5. 生成静态页面并部署

此时，只剩最后一步就大功告成了。

执行`hexo g -d`将静态页面部署到`master`分支上。  
那么此时可以看到 repo 上有两个分支，一个 hexo:

![77](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520175433.jpeg)

一个 master:

![8](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520175436.jpeg)

分别存储配置文件和静态页面，perfect！  
进入 [https://kakadee.github.io/](https://kakadee.github.io/)  
既可以看到自己的个人博客页面了。  

![2](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520175440.jpeg)

5. 日常上传博客流程

-----------

在本地对博客进行修改（添加新博文、修改样式等等）后，即可通过下面的流程进行管理。  

1. 依次执行`git add .`、`git commit -m "..."`、`git push origin hexo`指令将改动推送到 GitHub（此时当前分支应为 hexo）；  
2. 执行`hexo g -d`发布网站到 master 分支上。

> 以后的操作全都在 hexo 分支上执行，不需要切换到 master 分支。

6. 其他终端上传博客

-----------

如果你想在另一个电脑上上传你自己的博客，那么你只需要如下做即可：  

1. 从 repo 仓库上将项目代码 clone 到本地。  
2. 此时本地只有`master`分支，切换到`hexo`分支。

```
git checkout -b hexo origin/hexo
```

![10](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520175445.jpeg)

此时查看拉下来的 repo 有没有`.deploy_git`文件夹，如果有的话，删除并重新安装本地的 hexo-deployer。

```
rm -r .deploy_git
npm install hexo-deployer-git --save
```

搞定，之后按照步骤 5 即可完成上传。

7. 参考

-----

[https://www.zhihu.com/question/21193762](https://www.zhihu.com/question/21193762)  
[http://blog.csdn.net/zoeyyeoz/article/details/51143613](http://blog.csdn.net/zoeyyeoz/article/details/51143613)