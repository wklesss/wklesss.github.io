---
title: wsl2固定ip方案
tags:
  - wsl
  - github
  - 代理
cover: >-
  https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/photo-1563089145-599997674d42
categories: 工具使用
abbrlink: fef49edf
date: 2021-07-27 20:13:46
---

![image-20210727201410270](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/image-20210727201410270.png)

I give you a new idea: Instead of changing the IP, add a designated IP.

In Windows 10, run CMD or Powershell with administrator privilege, and then execute the following two commands:

:: Add an IP address in Ubuntu, 192.168.50.16, named eth0:1
`wsl -d Ubuntu -u root ip addr add 192.168.50.16/24 broadcast 192.168.50.255 dev eth0 label eth0:1`

:: Add an IP address in Win10, 192.168.50.88
`netsh interface ip add address "vEthernet (WSL)" 192.168.50.88 255.255.255.0`

In the future, you will use 192.168.50.16 when you access Ubuntu, and 192.168.50.88 when you access Win10.
You can save the above two lines of commands as a .bat file, and then put it into the boot area, and let it execute automatically every time.

windows10中，以管理员权限运行 CMD 或者Powershell。然后运行以下两条命令

分配IP给wsl：

`wsl -d Ubuntu -u root ip addr add 192.168.50.16/24 broadcast 192.168.50.255 dev eth0 label eth0:1`

分配IP给win10：

`netsh interface ip add address "vEthernet (WSL)" 192.168.50.88 255.255.255.0`

以后你访问Ubuntu时会使用192.168.50.16，访问Win10时会使用192.168.50.88。 可以将以上两行命令保存为.bat文件，然后放入boot区，让它每次都自动执行。



以上方案不会修改电脑原ip地址，只是将系统和wsl连入同一虚拟局域网中。

![image-20210727202405677](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/image-20210727202405677.png)

![image-20210727202431291](https://cdn.jsdelivr.net/gh/wklesss/picture@latest/img/image-20210727202431291.png)
