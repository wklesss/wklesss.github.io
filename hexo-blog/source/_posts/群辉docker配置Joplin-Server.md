---
title: 群辉docker配置Joplin Server
tags:
  - 群辉
  - nas
  - docker
  - joplin
  - 剪藏
  - 笔记
cover: >-
  https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/photo-1527168027773-0cc890c4f42e
categories: 工具使用
abbrlink: 878a097a
date: 2021-09-07 16:09:56
---

# 群辉Docker配置Joplin Server

## 创建目录、文件

1. 此步骤在docker文件操作目录下进行

   `mkdir joplin` 

   `cd joplin`

2. 创建 docker-compose.yml 文件
   `vim docker-compose.yml`#或者用其他你喜欢的编辑器

```
version: '3'
services:
    db:
        image: postgres:13.1
        ports:
            - "54321:5432" #群辉系统postgres已占用5432端口，这里需要将5432映射到其他端口
        restart: unless-stopped
        environment:
            - APP_PORT=22300
            - POSTGRES_PASSWORD=password #密码
            - POSTGRES_USER=user
            - POSTGRES_DB=joplin
    app:
        image: joplin/server:latest
        depends_on:
            - db
        ports:
            - "22300:22300"
        restart: unless-stopped
        environment:
            - APP_BASE_URL=http://你的域名/
            - DB_CLIENT=pg
            - POSTGRES_PASSWORD=密码
            - POSTGRES_DATABASE=joplin
            - POSTGRES_USER=user
            - POSTGRES_PORT=5432
            - POSTGRES_HOST=db
```

## 创建容器

`docker-compose up -d`

此处将创建joplin_app_1、joplin_db_1两个容器。

![image-20210907162256407](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/image-20210907162256407.png)

## 管理

浏览器使用<http://你的域名/>进入管理页面

首次登陆邮箱为：admin@localhost 密码为：admin

成功进入管理页面

<img src="https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/image-20210907163105367.png" alt="image-20210907163105367" style="zoom:80%;" />

点击user按钮，在账户管理页面修改email以及password

## 同步

1. joplin进入设置 <kbd>Ctrl</kbd>+<kbd>，</kbd> 
2. 同步选项：
   - 同步目标：Joplin Server (Beta)
   - Joplin 服务器 URL: http://你的域名/
   - Joplin Server 邮箱：你的管理页面邮箱
   - Joplin 服务器密码：你的管理员邮箱

<img src="https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/image-20210907163411965.png" alt="image-20210907163411965" style="zoom:80%;" />

