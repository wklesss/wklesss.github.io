---
title: PicGo搭建github图床
categories: 工具使用
tags:
  - 图床
  - github
cover: 'https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520184520.jpeg'
abbrlink: 2513fba4
date: 2021-05-19 01:24:37
---


PicGo 搭建 github 图床
==================

文章链接:[https://xiaowujiang.cn/posts/2513fba4/](https://xiaowujiang.cn/posts/2513fba4/)

#### 1. 下载 [PicGo](https://github.com/Molunerfinn/PicGo/releases) 并安装；

#### 2. 生成 [Github](https://github.com/)token

##### 步骤如下：

*   点击个人中心，选择`Settings`, 打开个人设置页面；

*   在个人设置页面选择`Developer Settings`

[![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210519011957.png)]

*   进入`Developer settings`页后，点击`Personal access tokens`打开新的页面后, 并点击右边的`Generate new token` 生成`token`

[![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210519012111.png)]

*   在生成`token`页面，勾选`repo`

[![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210519012126.png)]

#### 3. 创建公共仓库，用来存放相关资源图片

 在 github 上创建一个仓库，用来存放一些资源

[![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210519012144.png)]

#### 4. 在 PicGo 中配置 github 图床相关信息

* 打开 PicGo 后，先安装一个插件`github-plus`，该插件是用来将图片上传到`gitee`或`github`上，比自带的`github`图床方便 (自带的没有办法删除远程记录)

* 安装完成后，插件配置：

  [![](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210519012158.png)]

  ① 处是需要存放图片的仓库，格式为 `github用户名/ 仓库名`;

  ② 处是存放图片路径的仓库下的分支，默认`master`分支；

  ③ token 为第二步骤上生成的 **github token**；

  ④ 远程仓库存放图片的的路径，可自定义，可不填；

  ⑤ 自定义的图片路径，由于我使用了`jsDelivr`来实现 github 的`cdn缓存`，所以设置了此路径，如果不需要可不填；

  **jsDelivr 路径规则：** `https://cdn.jsdelivr.net/gh/用户名/仓库名@版本号`，我这边版本号设置的是`latest`表示获取最新资源。

  ⑥ origin 表示 仓库可以是 gitee 或`github`, 根据前面的步骤，此处只能是 github；

  ⑦ 将其设置为默认图床

注意事项
====

* 如果仓库需要设置自定义域名，需要将我们的资源提交到一个`gh-pages`分区

* 如果你的自定义域名配置 dns 区分了境外和国内，那么就需要注意，访问该仓库可能会出现 404 的情况

  解决办法：

  *   创建一条新的 cname 解析，添加一个二级域名即可

__EOF__


本文链接：[https://www.cnblogs.com/xiaowj/p/13909613.html](https://www.cnblogs.com/xiaowj/p/13909613.html)  
关于博主：评论和私信会在第一时间回复。或者[直接私信](https://msg.cnblogs.com/msg/send/xiaowj)我。  
版权声明：本博客所有文章除特别声明外，均采用 [BY-NC-SA](https://creativecommons.org/licenses/by-nc-nd/4.0/ "BY-NC-SA") 许可协议。转载请注明出处！  
声援博主：如果您觉得文章对您有帮助，可以点击文章右下角**【[推荐](javascript:void(0);)】**一下。您的鼓励是博主的最大动力！