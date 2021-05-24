---
title: hexo  使用
categories: 工具使用
tags: hexo
cover: 'https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/20210520184349.jpeg'
abbrlink: 65995f2c
date: 2021-05-19 22:58:38
---
##  常见命令

`hexo new "postName" #新建文章`  
`hexo new page "pageName" #新建页面`  
`hexo generate #生成静态页面至public目录`  
`hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）`  
`hexo deploy #部署到GitHub`  
`hexo help  # 查看帮助`  
`hexo version  #查看Hexo的版本`  

## 缩写：


`hexo n == hexo new`  
`hexo g == hexo generate`  
`hexo s == hexo server`  
`hexo d == hexo deploy`  

## 组合命令：

`hexo s -g #生成并本地预览`  
`hexo d -g #生成并上传`  

## 同步仓库
依次执行:

` git add . `  
`git commit -m "xxx"`  
`git push origin hexo`


## 版本回退
### 本地分支版本回退
1.找到要回退的版本的commit id：   

`git reflog `  or `git online`

2.接着回退版本:

`git reset --hard Obfafd`

0bfafd就是你要回退的版本的commit id的前面几位

### 自己的远程分支版本回退的方法
如果你的错误提交已经推送到自己的远程分支了，那么就需要回滚远程分支了。   
1.首先要回退本地分支：

`git reflog`  or `git online`  
`git reset --hard Obfafd`

2.紧接着强制推送到远程分支：

`git push -f`
