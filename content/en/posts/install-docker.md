---
title: "Docker的安装"
subtitle: "Docker在Linux上的安装"
date: 2020-03-26T16:30:30+08:00
draft: false
author: 世今
toc: true
categories: 
- Docker
tags: 
- Docker
img: 
bigimg: 
---
##  什么是Docker

​	Docker 是一个开源项目，诞生于 2013 年初，最初是 dotCloud 公司内部的一个业余项目。它基于 Google 公司推出的 Go 语言实现。 项目后来加入了 Linux 基金会，遵从了 Apache 2.0 协议，项目代码在 [GitHub](https://github.com/docker/docker) 上进行维护。


<!-- more -->

​	Docker 自开源后受到广泛的关注和讨论，以至于 dotCloud 公司后来都改名为 Docker Inc。Redhat 已经在其 RHEL6.5 中集中支持 Docker；Google 也在其 PaaS 产品中广泛应用。

​	Docker 项目的目标是实现轻量级的操作系统虚拟化解决方案。 Docker 的基础是 Linux 容器（LXC）等技术。

​	在 LXC 的基础上 Docker 进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。

为什么选择Docker?

（1）上手快。

​	用户只需要几分钟，就可以把自己的程序“Docker化”。Docker依赖于“写时复制”（copy-on-write）模型，使修改应用程序也非常迅速，可以说达到“随心所致，代码即改”的境界。	

   随后，就可以创建容器来运行应用程序了。大多数Docker容器只需要不到1秒中即可启动。由于去除了管理程序的开销，Docker容器拥有很高的性能，同时同一台宿主机中也可以运行更多的容器，使用户尽可能的充分利用系统资源。

（2）职责的逻辑分类

​	使用Docker，开发人员只需要关心容器中运行的应用程序，而运维人员只需要关心如何管理容器。Docker设计的目的就是要加强开发人员写代码的开发环境与应用程序要部署的生产环境一致性。从而降低那种“开发时一切正常，肯定是运维的问题（测试环境都是正常的，上线后出了问题就归结为肯定是运维的问题）”

（3）快速高效的开发生命周期

​	Docker的目标之一就是缩短代码从开发、测试到部署、上线运行的周期，让你的应用程序具备可移植性，易于构建，并易于协作。（通俗一点说，Docker就像一个盒子，里面可以装很多物件，如果需要这些物件的可以直接将该大盒子拿走，而不需要从该盒子中一件件的取。）

（4）鼓励使用面向服务的架构

​	Docker还鼓励面向服务的体系结构和微服务架构。Docker推荐单个容器只运行一个应用程序或进程，这样就形成了一个分布式的应用程序模型，在这种模型下，应用程序或者服务都可以表示为一系列内部互联的容器，从而使分布式部署应用程序，扩展或调试应用程序都变得非常简单，同时也提高了程序的内省性。（当然，可以在一个容器中运行多个应用程序）



## 一、更新软件

为避免安装软件时，系统的一些包或软件版本过低，我们拿到一台新服务器时会跟新一下系统软件

Ubuntu 更新软件

+ sudo apt-get update;

+ sudo apt-get upgrade

centos更新软件

+ sudo yum update

## 以下在Ubuntu演示：

### 安装docker

+ sudo apt-get install docker.io
+ 查看版本信息  docker -v

把docker添加到用户组，以便当前用户使用docker命令

+ sudo usermod -aG docker $USER

重新登录

docker info 查看信息

### 设置docker镜像仓库源

dockers默认仓库在国外，比较慢，换回国内。

Ubuntu 的是在默认路径，centos有些不是在默认路径

+ sudo vi /etc/docker/daemon.json

添加信息

```
{
 "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

### 安装docker-compose

+ sudo pip install docker-compose -i http://pypi.douban.com/simple --trusted-host pypi.douban.com

查看版本

+ docker-compose -v

### 官方安装文档
#### 文档地址：

+ https://docs.docker.com/install/

#### 官方 Dockerfile
+ nginx: https://github.com/nginxinc/docker-nginx
+ mysql: https://github.com/docker-library/mysql
+ python: https://github.com/docker-library/python
+ redis: https://github.com/docker-library/redis

#### 镜像 Tag 查询
https://registry.hub.docker.com/

