---
title: Linux-Install-Python3
tags:
  - Linux
  - Python
categories: Python
abbrlink: 4118
date: 2021-01-13 20:43:28
top_img:
---

###    Linux-Install-Python

+ 检测`Python`环境是否存在

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/noPython.png">

#####  源代码构建安装`python3.7`

+ `gcc`

  ```bash
  # 检测 gcc
  gcc --version
  # 没有 gcc
  yum install gcc
  # 更新 gcc
  yum update gcc
  ```

  

+ 源代码构建安装 `Python3.7`

  ```bash
   wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tar.xz
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/installPy.png" width="600" height="210">

+ 解压缩和接归档

  ```bash
  # 解压缩
  	xz -d Python-3.7.3.tar.xz 
  # 解归档
  	tar -xvf Python-3.7.3.tar 
  ```

+ 补充依赖库

  ```bash
  yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel libffi-devel
  
  # 有两个可能下载失败 Eg. db4-devel···
  # Error: Unable to find a match: db4-devel libpcap-devel
  ```
  
+ 进入 `Python`源代码目录安装前准备工作

  ```bash
  
  cd Python-3.7.3
  
  # 安装到指定位置
  ./configure --prefix=/usr/local/python37 --enable-optimizations
  # --enable-optimizations 启用优化
  ```

+ 构建和安装

  ```bash
  make && make install
  ```

+ 检测是否安装成功

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/python37.png">

+ 配置环境变量

  + 编辑文件`.bash_profile`(注册 python 环境变量 )

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/bashfile.png">

  + 添加安装时`python`位置

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/pythonPath.png">

    ```bash
    添加: :/usr/local/python37/bin
    ```

  + 激活环境变量

    ```bash
    source .bash_profile
    ```

+ 符号链接

  + 硬链接

    ```bash
    相当于文件备份,但是不会增加磁盘存储，只要引用不为 0, 文件就不会被删除
    
    ln 文件 /路径/文件名.py
    
    ```

  + 软连接

  