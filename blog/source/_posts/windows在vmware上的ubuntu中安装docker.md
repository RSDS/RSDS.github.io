---
title: windows10在vmware上的ubuntu中安装docker
date: 2019-09-05 14:44:53
tags:
---
### 前言
- win10有了自己的linux子系统，通常的功能可以正常使用，但是子系统的linux内核是经过微软魔改的，无法正常使用docker，所以通过vmware安装ubuntu再安装docker

### 一，安装vmware, ubuntu 与vmtools
#### 0，vmware使用15 与 ubuntu 使用 18，安装过程略，参考
#### 1，打开虚拟机VMware Workstation，启动Ubuntu系统，菜单栏 - 虚拟机 - 安装VMware Tools，不启动Ubuntu系统是无法点击“安装VMware Tools”选项的，如下图：
![](/images/vmware安装ubuntu与docker/安装vmwaretools.jpg)
#### 2，桌面新建vmtools文件夹，并复制vmware tools到刚创建的文件夹中，再在文件夹中提取.
![](/images/vmware安装ubuntu与docker/复制vmtools镜像到刚创建文件夹中.jpg)
#### 3，我们切换root用户(`sudo su`)进入到刚刚提取到的vmware-tools-distrib文件夹下，然后执行命令：`./vmware-install.pl`：
![](/images/vmware安装ubuntu与docker/进入解压缩文件夹并执行命令.jpg)
#### 4，一路yes直到出现enjoy安装完毕，屏幕自适应就完成了:
![](/images/vmware安装ubuntu与docker/一路yes直到出现enjoy安装完毕.jpg)

### 二，更改ubuntu源，[参考](https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/)
``` bash
apt-get update
cp /etc/apt/sources.list /etc/apt/sources.list.bak
gedit /etc/apt/sources.list
```
将清华镜像添加进sources.list文件中
``` bash
apt-get update
```
### 三，安装docker, [参考](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
#### 1，删除旧版本
``` bash
apt-get remove docker docker-engine docker.io containerd runc
```
#### 2，前置安装
``` bash
apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
#### 3, 添加docker官方 GPG key，并校验
``` bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

apt-key fingerprint 0EBFCD88
```
#### 4, 设置docker稳定仓库
``` bash
   add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
#### 5，安装docker
``` bash
apt-get install docker-ce docker-ce-cli containerd.io
```

- 测试docker 是否安装正常
``` bash
docker run hello-world
```
- 安装完docker，需要服务重启 service docker restart
- docker 搜索镜像[官网](https://hub.docker.com/search/?q=kafka&type=image)

#### 6，安装 docker-compose，[参考1](https://docs.docker.com/compose/install/), [参考2](https://github.com/docker/compose/releases), [参考3](https://github.com/wurstmeister/kafka-docker/blob/master/test/docker-compose.yml)
- 现在使用的场景（搭建kafak, hadoop都需要很多依赖工具），为了简化部署，使用docker-compose.yml 一个文件即可设置各组件依赖关系，部署更快速。
``` bash
curl -L https://github.com/docker/compose/releases/download/1.24.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```






#### 命令行代理
``` bash
export http_proxy=http://10.23.60.17:1080
export https_proxy=http://10.23.60.17:1080
```