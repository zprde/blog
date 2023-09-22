---
title: 在WSL2中挂载物理硬盘
date: 2023-09-11T11:01:27+08:00
tags:
- WSL2
---

> 在启用WSL2后，希望让其中的Ubuntu能够挂载一块真实的物理硬盘，方便后续的数据操作。

## 查看硬盘ID
第一步右键点击计算机图标，选择“管理”：
![image.png](https://img.zprde.cn/images/2023/09/22/image.png)

在计算机管理中选择“磁盘管理”:
![imagedeed9a817a742962.png](https://img.zprde.cn/images/2023/09/22/imagedeed9a817a742962.png)

之后我们可以在窗口下方看到所有硬盘都被列出，形如“磁盘N”，此时记住我们希望挂载到WSL的硬盘编号。
![image0a96ef5fa99ff257.png](https://img.zprde.cn/images/2023/09/22/image0a96ef5fa99ff257.png)


## 挂载物理硬盘
随后打开控制台，执行一下命令，硬盘将会直接挂载到WSL2内部：
```shell
# 关闭正在运行的WSL实例
wsl --shutdown

# 如果上一步我们选择的硬盘是2，则执行
wsl --mount \\.\PHYSICALDRIVE2

# 再次开启并进入WSL实例
wsl

# 检查WSL中所有硬盘
lsblk
```
随后将看到硬盘被挂载到WSL中，可以进行进一步的使用：
![image0546f30db84a8ed2.png](https://img.zprde.cn/images/2023/09/22/image0546f30db84a8ed2.png)


## 存在的问题
这种挂载方式每次重启WSL之后都需要重复执行，需要进一步将其设置成每次开启WSL实例之前进行自动挂载。


