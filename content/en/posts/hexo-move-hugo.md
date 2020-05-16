---
title: "Hexo迁移到Hugo"
subtitle: ""
date: 2020-04-25T16:30:30+08:00
draft: false
author: 世今
toc: true
categories: 
- 博客
tags: 
- Hugo
img: 
bigimg: 
---

前几天完成了hexo向hugo的迁移，记录一下过程。

## <span id="inline-toc">1.<span> 原因
   + hugo比hexo更快，文章多后就会有差异
   + hugo是用go写的，正好我正准备学习go，所以就当学习

## <span id="inline-toc">2.<span> hexo和hugo的差异
在hugo的官网上hugo是这样介绍的

 **The world’s fastest framework for building websites**

确实是这样，hugo不管在安装和使用上都要比hexo简单一点，更容易上手，hugo与hexo类似，但比hexo更高效、简洁、扩展性强。

### 在安装上

hugo只需要一个二进制文件即可，而hexo必须安装一些其他依赖。

---

更多hugo信息请看hugo官网[https://gohugo.io/](https://gohugo.io/)

## <span id="inline-toc">3.<span>hugo的使用

### 一、首先你的电脑必须安装

    + Git
    + Go(https://golang.google.cn/)

### 二、源码安装

1. 到GitHub上下载关于自己电脑配置的版本https://github.com/gohugoio/hugo/releases，下载
2. 在自己电脑下的任意位置，创建一个文件目录，创建一个bin文件来，把文件解压
   ```
     ~/Hugo $ tree -L 1
    .                   
    ├── bin/    
        ├── hugo.exe
        ├── ..   
    ├── sites/ # 存放网址
    ```      

3. 把带有Hugo.exe的目录添加到环境变量
4. 使用hugo version检查安装是否成功

### 三、创建站点

```hugo new site blog``` 创建一个名为blog的站点

```go
~/blog $ tree -L 1
.                     # 说明             Hexo
├── archetypes/     # 文章模板          scaffolds/
├── assets/         # Hugo 管道
├── config.toml     # 配置文件          _config.yml
├── content/        # 文章目录          source/_posts/
├── data/           # Hugo 数据文件     source/_data/
├── layouts/        # 布局模板
├── public/         # 生成的静态文件     public/
├── resources/      # Hugo 缓存
├── static/         # 网站的静态文件     source/
└── themes/         # 主题目录          themes/


```

#### 添加一个主题

在官方网站上有很多种主题可以选择，挑一个自己喜欢的主题

**然后把主题里的exampleSite里的文件复制在根目录**

```
cd blog;\
git init;\
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke;\

# Edit your config.toml configuration file
# and add the Ananke theme.
echo 'theme = "ananke"' >> config.toml
```

#### 添加一篇新文章

``` 
hugo new posts/my-first-post.md
```

#### 查看运行效果

```
hugo server
```

### 四、主题配置

主题配置在config下的.toml下的文件中配置，详细配置就不说了，根据自己的情况配置，更多的主题修改可在layout里修改

### 五、配置GitHub Pages

这部分网上教程非常多，首先在 GitHub 上创建一个 Repository，命名为 username.github.io

把 config.toml 的 basaeURL 修改为 https://usrname.github.io/

然后进入你的 public 目录按照正常 Git 命令操作即可

```
$ cd public
$ git init
$ git remote add origin https://github.com/username/username.github.io.git
$ git add -A
$ git commit -m "first commit"
$ git push -u origin master
```

第一次初始化时可能会叫配置用户名和密码：

```
git config --global user.name "xxx"

git config --global user.email "xxx@xxx.com"
```

之后更新文章并生成好静态页面以后，就可以使用 Git push 来同步了

```
$ cd public
$ git add .
$ git commit -m "add blog post"
$ git push
```

关于 Git 的使用说明，可以参考网络上的一大堆教程，这里不再重复。

#### 编写自动化脚本

在根目录下创建deploy.sh，输入如下：

```
#!/bin/sh

# If a command fails then the deploy stops
set -e

printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public

# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site $(date)"
if [ -n "$*" ]; then
	msg="$*"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master
```

此后，编写文章后，双击脚本运行自动上次到GitHub。

## <span id="inline-toc">4.<span> 下一步计划

  采用阿里云OSS+CDN加速+全站https
  让网站飞起来🍻