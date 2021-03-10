---
title: MongoDB-安装
tags:
  - Node
  - SQL
  - MongoDB
categories: MongoDB
abbrlink: 28913
date: 2021-02-10 11:39:49
top_img:
---

###  Mongodb-安装与使用

####  Mongodb 安装

1. 下载`Mongodb`和`Mongodn Compass`

   > <a href="https://www.mongodb.com/try/download/community">点击前往 Mongodb  官网</a>
   >
   > <a href="https://www.mongodb.com/try/download/compass">点击前往 Mongodb-compass  官网</a>

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/downloadMongodb.png" width="300">

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/mongodbins.png">

2.  请使用管理员权限安装

   + `accept`
   + `custom` 自定义安装路径,无中文特殊符号的路径下

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/custorm.png" width="400">

   + 默认

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/mongbinstall.png" width="400">

   + `compass`

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/compass.png" width="400s">



####  Compass 安装

+ 双击 安装包安装即可

+ 完成后进入 点击`Start Using Compass`,注意留意用户名以便于其他软件使用

+ 连接

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/connectMongdb.png" width="600">

+ 成功后的标志

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/rightMongodb.png" width="600">

+ 使用`Navicat Premium 15`连接`Mongodb`

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/navMongodb.png" width="600">

+ 启动停止`mongodb`服务

  ```bash
  配置环境变量: path: bin目录下
  
  使用管理员权限启动: net start mongodb
  停止服务: net stop mongodb
  ```

+ 检测是否正确安装

  ```bash
  mongo --version
  
  输出版本信息即为正确安装
  
  ```

  

####  开启验证后使用 `Navcat`

<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/monPassword.png" width="400">