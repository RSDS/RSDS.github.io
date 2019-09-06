---
title: windows10 在vmware安装ubuntu
date: 2019-09-05 16:47:14
tags:
photos: /images/vmware安装ubuntu与docker/安装vmwaretools.jpg
---

<!-- <img src="/images/vmware安装ubuntu与docker/安装vmwaretools.jpg" width = "900" height = "600" alt="git" align=center /> -->


#### 安装vmware, ubuntu 与vmtools
- **0，vmware使用15 与 ubuntu 使用 18，安装过程略，参考**
<!-- more -->
- **1，打开虚拟机VMware Workstation，启动Ubuntu系统，菜单栏 - 虚拟机 - 安装VMware Tools，不启动Ubuntu系统是无法点击“安装VMware Tools”选项的，如下图：**

![](/images/vmware安装ubuntu与docker/安装vmwaretools.jpg)
- **2，桌面新建vmtools文件夹，并复制vmware tools到刚创建的文件夹中，再在文件夹中提取.**

![](/images/vmware安装ubuntu与docker/复制vmtools镜像到刚创建文件夹中.jpg)
- **3，我们切换root用户(`sudo su`)进入到刚刚提取到的vmware-tools-distrib文件夹下，然后执行命令：`./vmware-install.pl`：**
  
![](/images/vmware安装ubuntu与docker/进入解压缩文件夹并执行命令.jpg)
- **4，一路yes直到出现enjoy安装完毕，屏幕自适应就完成了:**

![](/images/vmware安装ubuntu与docker/一路yes直到出现enjoy安装完毕.jpg)

#### 更改ubuntu源，[参考](https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/)
``` bash
apt-get update
cp /etc/apt/sources.list /etc/apt/sources.list.bak
gedit /etc/apt/sources.list
```
将清华镜像添加进sources.list文件中
``` bash
apt-get update
```