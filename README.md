# wklesss.github.io
## hexo博客根目录
[这是网站](https://wklesss.github.io/)

# 更换电脑后操作
```bash
sudo npm install hexo-cli -g
```

但是已经不需要初始化了，

直接在任意文件夹下，

```bash
git clone git@………………
```

然后进入克隆到的文件夹：

```bash
cd xxx.github.io/hexo-blog
npm install
npm install hexo-deployer-git --save
```

生成，部署：

```
hexo g -d
```


然后就可以开始写你的新博客了

```bash
hexo new newpage
```


Tips:

不要忘了，每次写完最好都把源文件上传一下

```bash
git add .
git commit –m "xxxx"
git push 
```

如果是在已经编辑过的电脑上，已经有clone文件夹了，那么，每次只要和远端同步一下就行了

```bash
git pull
```

> 参考：
>
> [使用hexo，如果换了电脑怎么更新博客？](https://www.zhihu.com/question/21193762)