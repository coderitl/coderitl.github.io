---
title: Linux-Mariadb-Install
tags:
  - Linux
  - mysql
categories: Linux
abbrlink: 5863
date: 2021-01-14 18:52:10
top_img:
---

###   Linux-mariadb-Install

+ 搜索

  ```bash
  # 搜索的作用: 显示可安装程序包
  yum search mariadb
  ```

+ 安装

  ```bash
  yum install -y mariadb mariadb-server
  ```

+ 启动服务

  ```bash
  systemctl start mariadb # 3306 端口
  ```

+ 查看端口号是否被占用

  ```bash
  netstat -nap | grep 3306
  
  mysqld # MYSQL Daemon
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/netstat.png">

+ 登录数据库

  ```bash
  mysql -u root -p # 按两下回车,跳过密码
  
  # 显示所有数据库
  show databases;
  # 使用数据库
  use mysql;
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/finishMysql.png" width="500">

+ 配置密码

  ```bash
  update user set password=password('123456') where user='root';
  ```

+ 激活密码

  ```bash
  flush privileges;
  ```

+ 退出

  ```bash
  quit;
  ```

+ 无密码测试登录

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/configpassword.png">

