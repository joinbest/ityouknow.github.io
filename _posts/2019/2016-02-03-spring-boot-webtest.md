---
layout: post
title: 理解下所谓的ssh隧道
copyright: Linux
category: ssh
tags: [ssh]
---


# 一.含义

client为了访问到server的服务，但是由于防火墙的阻拦，client没有办法通过正常访问来进行,这就用到了ssh隧道。

**那么ssh隧道本质上其实就是端口转发**,它能够将其他TCP端口的网络数据通过SSH链接来转发,并提供相应的加解密服务.

# 二.功能

ssh的端口转发有两大功能

1. 加密ssh client和ssh server之间的通讯数据
2. 突破防火墙的限制完成一些之前无法建立成功的TCP连接

# 三.Linux下应用的案例

1. mysql 的server端运行着mysql服务但是只监听着127.0.0.1,在client端搭建ssh隧道亦可访问

> ssh -N -f -L 3306:localhost:3306 $server_ip

```bash
-1：强制使用ssh协议版本1；
-2：强制使用ssh协议版本2；
-4：强制使用IPv4地址；
-6：强制使用IPv6地址；
-A：开启认证代理连接转发功能；
-a：关闭认证代理连接转发功能；
-b：使用本机指定地址作为对应连接的源ip地址；
-C：请求压缩所有数据；
-F：指定ssh指令的配置文件；
-f：后台执行ssh指令；
-g：允许远程主机连接主机的转发端口；
-i：指定身份文件；
-l：指定连接远程服务器登录用户名；
-N：不执行远程指令；
-o：指定配置选项；
-p：指定远程服务器上的端口；
-q：静默模式；
-X：开启X11转发功能；
-x：关闭X11转发功能；
-y：开启信任X11转发功能。
```

**1.在client上的应用客户端首先将数据发送到本地的3306端口**

**2.client上的ssh客户端将本地3306端口收到的数据发送到server端的ssh server上**

**3.ssh server会解密收到的数据并且将它转发到监听的3306端口**



![1562152091037](C:\Users\Join\AppData\Roaming\Typora\typora-user-images\1562152091037.png)

[具体解释可以参考这篇文章](ssh隧道 - 简书
https://www.jianshu.com/p/20600c91e656)













