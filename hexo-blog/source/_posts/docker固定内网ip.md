---
title: docker固定内网ip
tags:
  - docker
  - linux
  - terminal
  - pt
  - shell
cover: 'https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/202206091443862.png'
categories: 工具使用
abbrlink: 3b7b10e0
date: 2022-06-09 14:53:18
---

# docker固定内网ip，分离代理，解决pt走代理的问题

## 创建网络

服务器或nas通过ssh登录，`sudo -i`取得root权限，输入以下命令：

```bash
docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.2 -o parent=ovs_eth0 bridge-host
```

其中:

`macvlan`：驱动

`subnet=192.168.1.0/24` ：网段

`gateway=192.168.1.2`：网关地址

`parent=ovs_eth0`：物理网卡名称，可通过 `ip addr`查询

`bridge-host`：自定义网络名称

## 创建容器

### docker run

```bash
docker run -itd --name tr --network bridge-host --ip=192.168.1.15 chisbread/transmission:latest
```

### docker-compose

```dockerfile
version: "3"
services:
  tr-bz:
    image: chisbread/transmission:latest
    container_name: tr-bz 
    restart: unless-stopped
    networks:
      default:
        ipv4_address: 192.168.1.15
    environment:
      - PUID=1026
      - PGID=100 
      - TZ=Asia/Shanghai
      - USER=admin
      - PASS=admin
      - PEERPORT=51413
      - RPCPORT=12005
    volumes:
      - 
      
networks:
  default:
    external:
      name: bridge-host

```



这样就可以将自定义网络中的网关地址修改为主路由地址，并分配独立的ip，防止不需要走代理的容器在旁路由内出现各种问题

> 参考：
>
> [群晖docker安装宝塔面板并启用独立内网ip](https://www.gitloc.com/archives/82.html)
>
> [docker-compose 使用自定义网络并绑定 IP](https://www.cnblogs.com/nnylee/p/11428567.html)
