---
title: Linux-MYSQL 安装
tags:
  - linux
  - mysql
abbrlink: 10285
date: 2021-01-03 11:21:33
Categories:
top_img:
cover:
---

###  Linux-MYSQL 安装

```bash

CentOS7安装MySQL以及密码修改

```

+ 下载并安装`MySQL`官方的 `Yum Repository`

  ```bash
  # 安装用的Yum Repository
  	
  	wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
  	
  ```

+ yum 安装

  > ```bash
  > # yum 安装
  > 
  > 	yum -y install mysql57-community-release-el7-10.noarch.rpm
  > 	
  > ```
  >
  > <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210103122153.png">

+ MYSQL服务器安装

  > ```bash
  > # MYSQL 服务器安装
  > 
  > 	 yum -y install mysql-community-server
  > 	 
  > ```
  >
  > <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210103122400.png">

+ `MySQL`数据库设置

  ```bash
  # 启动 mysql
  
   systemctl status mysqld.service
   
  # 此时MySQL已经开始正常运行，不过要想进入MySQL还得先找出此时root用户的密码，通过如下命令可以在日志文件中找出密码
  
  grep "password" /var/log/mysqld.log
  
  ```

  

+ 进入`MYSQL`数据库

  ```bash
  
  mysql -u root -p
  
  # 输入初始密码，此时不能做任何事情，因为 MySQL 默认必须修改密码之后才能操作数据库：
  
  ```

+ 修改密码

  ```bash
   ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
  ```

+ 报错

  ```bash
  # 这里有个问题，新密码设置的时候如果设置的过于简单会报错
  
  #原因是因为MySQL有密码设置的规范，具体是与validate_password_policy的值有关:
  
  # MySQL完整的初始密码规则可以通过如下命令查看：
  	
  	SHOW VARIABLES LIKE 'validate_password%';
  
  #密码的长度是由validate_password_length决定的
  
  修改:
  	set global validate_password_policy=0;
  	set global validate_password_length=1;
  	
  # 但此时还有一个问题，就是因为安装了Yum Repository，以后每次yum操作都会自动更新，需要把这个卸载掉;
  
  	yum -y remove mysql57-community-release-el7-10.noarch
  	
  	
  
  ```

+ `MYSQL` 允许外部链接

  ```bash
  mysql -u root -p # 是以权限用户root登录
  
  use mysql; # 选择mysql库
  
  select 'host' from user where user='root'; # 查看mysql库中的user表的host值（即可进行连接访问的主机/IP名称）
  
  update user set host = '%' where user ='root';# 修改host值（以通配符%的内容增加主机/IP地址），当然也可以直接增加IP地址
  
  flush privileges; # 刷新MySQL的系统权限相关表
  
  select 'host'  from user where user='root';
  
  ```

  ```bash
  
  重起 mysql 服务即可完成。
  
  打开 mysql配置文件vi /etc/mysql/mysql.conf.d/mysqld.cnf :
  
      将bind-address = 127.0.0.1注销​
  
      bind-address = 0.0.0.0 # 表示允许任何主机登陆MySQL
  
      port=3306 # 表示MySQL运行端口为3306
  
  ```

  ```bash
  支持root用户允许远程连接mysql数据库
  
  grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option;
  
  flush privileges;
  
  /etc/init.d/mysql start
  
  ```

+ 密码及权限设置

  ```bash
  mysql5.6
      grant all privileges on *.* to root@'%' identified by "mysql_pwd" with grant option;
      grant all privileges on *.* to root@'localhost' identified by "mysql_pwd" with grant option;
      grant all privileges on *.* to root@'127.0.0.1' identified by "mysql_pwd" with grant option;
      drop database if exists test;
      use mysql;
      delete from user where not (user='root');
      delete from db where user='';
      UPDATE user SET password=PASSWORD('mysql_pwd') WHERE user='root' AND host='127.0.0.1' OR host='%' OR host='localhost';
      delete from user where password='';
      flush privileges;
      select user,password,host from mysql.user;
      exit;
  
  
  mysql5.7:
      grant all privileges on *.* to root@'%' identified by "mysql_pwd" with grant option;
      grant all privileges on *.* to root@'localhost' identified by "mysql_pwd" with grant option;
      grant all privileges on *.* to root@'127.0.0.1' identified by "mysql_pwd" with grant option;
      drop database if exists test;
      use mysql;
      delete from user where not (user='root');
      delete from db where user='';
      delete from user where authentication_string='';
      update mysql.user set authentication_string=password('mysql_pwd') where user='root' AND host='127.0.0.1' OR host='%' OR host='localhost';
      flush privileges;
      select user,authentication_string,host from mysql.user;
      exit;
  ```

  

> 转载自: https://www.cnblogs.com/shaozhu520/p/12830607.html