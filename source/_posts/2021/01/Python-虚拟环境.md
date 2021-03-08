---
title: Python-虚拟环境
tags:
  - Python
  - 虚拟环境
categories: Python
abbrlink: 42073
date: 2021-01-03 10:40:03
top_img:
cover:
---

###  虚拟环境

+  虚拟环境的意义

  ```python
  # 虚拟环境(进入虚拟环境工作时的包安装不能添加 sudo ):
     
  什么是虚拟环境:  
  	
      虚拟环境是真实 python 环境的复制版本
  ```

+ 虚拟环境的安装

  ```python
  安装虚拟环境的命令:
        
        sudo pip install virtualenv -- 安装虚拟环境的命令
        
        sudo pip install virtualevwarpper -- 安装虚拟环境扩展包
        
     
  ```

+ 虚拟环境配置

  ```python
    编辑家目录下的 .bashrc 文件 添加下面的语句:
        
           export WORKON_HOME = $HOME/.virtualenv
           
           source/usr/local/bin/virtualevwarpper.sh
     
     使用 source .bashrc 使其生效
     
     创建虚拟环境命令:
        
        mkvirtualenv 虚拟环境名
        
        创建 python3 虚拟环境:
        
           mkvirtualenv -p python3 虚拟环境名
     
     -- 退出虚拟环境:
     
           deactivate
           
     -- 进入虚拟环境工作:
     
        workon 虚拟环境名
     
     -- 删除虚拟环境:
        
        rmvirtualenv 虚拟环境名
        
     -- 安装 Django 框架:
     
        pip install django==1.8.2(可以省略版本)
        
        查看已经安装的 django 版本:
        
           pip freeze
           
              
  ```

+ 创建`Flask`项目

  ```python
  
  ```

+ `Flask` 项目结构分析

  ```python
  
  ```

+ 创建 `Django`项目

  ```python
     
        django-admin startproject 项目名
        
        文件分析:
        
           __init__.py : 说明 xxx 是一个· python 包
           
           settings.py : 项目的配置文件
           
           uris.py : 进行 url 路由配置
           
           wsgi.py : web 服务器和 django 交互的入口
           
           manage.py : 项目的管理文件
        
     一个项目是很多个应用组成的，每一个应用玩成一个待定的特定功能 
        
        常见应用的命令:
        
           python manager.py startapp 应用名
           
           注意: 创建应用时首先进入项目目录
           
           应用下的文件:
           
              __init__.py : 说明目录是一个 python 模块
              
              models.py : 写和数据库项目的内容
              
              views.py : 接受请求,进行处理(定义处理函数,视图函数)
              
              test.py : 写测试代码的文件
              
              admin.py : 网站后台管理相关的文件
              
              建立应用和项目之间的联系,需要对应用进行注册:
              
                 修改(主) settings.py 中的 installed_apps  配置项 添加: "应用名"
                 
           运行开发 web 服务器命令:
              
              python manager.py runserver
  ```

  