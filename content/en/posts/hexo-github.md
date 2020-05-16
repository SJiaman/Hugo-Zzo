---
title: "Hexo+GitHub搭建博客"
subtitle: "一个简单的博客搭建"
date: 2019-10-08T16:30:30+08:00
draft: false
hideToc: false
enableToc: false
enableTocContent: true
author: 世今
toc: true
categories: 
- 博客
tags: 
- Hexo
# img: "https://hugo-picture.oss-cn-beijing.aliyuncs.com/images/20191203172524.jpeg"
# bigimg: [{src: "https://hugo-picture.oss-cn-beijing.aliyuncs.com/blog/2019-04-27-080627.jpg"}]
---

  在国庆前一个星期，我准备自己写一个博客网站，于是在网上查了一下怎么写才好，本来想自己一步步的来，但是看了一下网上一些比较好的博客网站，发现他们都是基于某个框架搭建的，于是我也就选了hexo+github来搭建我的博客网站。
  为什么要搭建这个博客网站了？
    一是兴趣来了，想做一个来玩玩；
    二是为了能促进自己学习嘛，虽然不一定写博客，哈哈。

  <!-- more -->

## <span id="inline-toc">1.</span> 过程

  我呢是根据网上的教程一步步来构建的，中途也是遇到了一些小问题，但在网上都能找到解决的办法，所以，只要自己愿意去做，没有困难可以阻挡自己前进的。
##### 大概步骤：

    + 安装Node.js
    + 添加国内镜像源
    + 安装Git
    + 注册Github账号
    + 创建一个以自己账户名.io的仓库
    + 安装Hexo
    + 个性化设置（主题下载与配置）
    + 连接Github与本地，上传代码
    + 写文章、发布文章
    + 绑定域名（可选）
     
  具体过程呢我就不说了网上教程多的是

  附一个比较好的教程链接吧。
  [Hexo 搭建个人博客系列：基础建站篇](http://yearito.cn/posts/hexo-get-started.html)

#### 过程困难点

  + 一安装各种东西，新手可能觉得有些问题
  + 没接触过这种代码可能不知所措，难以下手
  + 一些小bug。。。

  我所遇到的困难呢，主要是配置ssh。
由于我一开始git配置的是gitee,但是当我把git配置到GitHub上后我原来的配置就不能用了，把我折腾了半天，最后在网上找到教程终于弄好了。主要是把ssh配置两个文件，一个gitee,一个GitHub。

[解决方法：](https://my.oschina.net/u/3552749/blog/1678082)

#### 关于域名
  在GitHub上搭建好博客网站后，如果不喜欢自己的域名，可以自己买一个域名来代替原来的域名，而且不需要备案，在阿里云和腾讯云都可以买。域名解析简单。
配置域名步骤：
  1. 在命令行里ping一下GitHub分配给自己的网址
  2. 在域名控制台解析里添加两条记录
     ```
      @	A	默认	IP地址   10 分钟
      www	A	默认	IP地址   10 分钟
      ```
  3. 在自己的source文件夹下创建一个CNAME文件，文件里写如自己的域名
  4. 同步GitHub仓库，然后就可以愉快的用自己域名了

## <span id="inline-toc">2.</span> 总结

  国庆节忙活了好几天，终于把一个基本的博客网站个弄好了，还是有很多的不足之处，慢慢来嘛，万事开头难，现在只需要后期完善，把它弄得好看就行了。不过我也得好好学习下那些技术，才能把它完全弄明白。