---
title: Linux-git-Install
tags:
  - Linux
  - git
categories: Linux
abbrlink: 49501
date: 2021-01-15 18:49:53
top_img:
---

###   Linux-git-Install

+ 进入`git`

+ 选择适合版本

  > <a href="https://mirrors.edge.kernel.org/pub/software/scm/git/">git-2.21.0.tar.xz</a>

+ 复制一个适合版本的链接

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/gitLinux.png">

  > `https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.21.0.tar.xz`

+ `Linux`下载

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/gitinstall.png">

+ 解压缩

  ```bash
  xz -d git-2.21.0.tar.xz 
  ```

+ 解归档

  ```bash
  tar -xvf git-2.21.0.tar 
  ```

+ 进入解压后的文件夹

  ```bash
  cd git-2.21.0/
  # 源代码构建安装需要 Makefile，查看是否存在
  ls | grep Makefile 
  # 更改安装路径需要文件
  ls | grep configure
  ```

+ 联网需要安装的依赖库,补包

  ```bash
  yum install -y libcurl-devel
  ```

+ 指定安装路径

  ```bash
  # 修改配置文件
  ./configure --prefix=/usr/local/
  ```

+ 构建安装

  ```bash
  make && make install
  ```

+ 测试

  ```bash
  git --version
  # 输出一下信息
  git version 2.21.0
  ```

###  使用git

+ 新建仓库

+ 文件添加

+ 日志信息

+ 误删除

  ```bash
  # 删除 没有添加 git 前缀的删除
  rm -f *
  # 恢复
  git checkout -- .
  ```

+ 版本回退

  ```bash
  git log
  
  git reset  --hard comit-id | git reset  --hard HARD^ # 回退到上一个版本
  
  # --hard
  
  # 未来版本查看
  git reflog
  
  ```

  