---
title: 通过Windows对外暴露WSL2的内部端口
date: 2023-09-22T10:51:27+08:00
tags:
- WSL2
---
> WSL2中所的有监听端都可以在Windows中通过localhost进行访问，但是无法在Windows外在通过Windows本身的IP的进行访问。

# 基本原理
可以通过Windows端代理口功能将WSL2中的端口通过Windows的IP对外暴露。核心命令:
```shell
netsh interface portproxy add v4tov4 `
listenaddress=[WIN_IP] listenport=[WIN_PORT] `
connectaddress=[WSL_IP] connectport=[WSL_PORT]
```
## 原始访问方式
比如我们在WSL中启用了SSH，后续我们可以通过`ssh`命令在Windows中访问WSL：
```shell
# 此时端口默认为22
ssh user_name@localhost
```

## 端口代理
如果想在Windows外访问WSL的SSH服务，我可以们尝试在Windows的Powershell中执行一命令下
```shell
netsh interface portproxy add v4tov4 `
listenaddress=0.0.0.0 listenport=2222 `
connectaddress=localhost connectport=22
```

## 远程访问
如果Windows拥有公网IP如`1.2.3.4`,我们可以在任意位置通过以下命令直接访问WSL中的SSH服务:
```shell
ssh user_name@1.2.3.4 -p 2222
```
