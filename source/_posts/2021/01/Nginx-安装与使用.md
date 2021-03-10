---
title: Nginx-安装与使用
tags:
  - Nginx
categories: Nginx
abbrlink: 53200
date: 2021-01-13 20:06:57
---



###   Nginx-安装与使用

+ `Nginx`是什么

  ```bash
  Nginx(engine x) 是一个高性能的 HTTP(解决 C10k的问题)和反向代理服务器，也是一个 IMAP/POP3/SMTP 服务器
  
  特点:
  	占用内存少，并发能力强
  	
  ```

+ `Nginx`的优势

  ```bash
  IO 多路复用:
      高并发
      epoll
      异步
      非阻塞
  ```

+ `nginx`目录介绍

  ```bash
  配置目录: /etc/nginx
  执行文件: /usr/sbin/nginx
  日志目录: /var/log/nginx
  启动文件: /var/init.d/nginx
  web 目录: /var/www/html 
  nginx配置文件: /etc/nginx/nginx.conf
  ```

+ 前提: 拥有服务器(推荐阿里云)

+ 连接服务器(`ssh`)

+ 搜索`nginx`

  ```bash
  yun search nginx
  ```

+ 查看已安装软件

  ```bash
  yum list installed
  ```

+ 搜索某个软件是否安装

  ```bash
  yum list installed | grep search-name
  ```

+ 安装`nginx`

  ```bash
  yum install nginx
  ```

+ 查看`nginx`的具体信息

  ```bash
  yum info nginx
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/nginx.png" width="600" height="300" alt="nginx">

+ 检查配置文件

  ```bash
  [sudo] nginx -t [可选参数: 权限不足添加 Centos无需添加sudo]
  
  输出以下信息: 
  
      [root@VM-0-3-centos ~]# nginx -t
      nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
      nginx: configuration file /etc/nginx/nginx.conf test is successful
  
  ```

+ 重新加载配置文件

  ```bash
  nginx -s reload
  ```

+ 启动`nginx`服务

  ```bash
  # 可以启动有缺点
  nginx
  
  # 推荐启动方式
  centos6 / ubuntu: service nginx start # 启动服务
  
  # 高版本 Linux / ubuntu
  systemctl start nginx  # 启动 nginx 服务
  systemctl stop nginx # 关闭 nginx 服务
  systemctl restart nginx # 重启 nginx
  systemctl status nginx # 查看 nginx 状态
  systemctl enable nginx # 开机自启
  systemctl disable nginx # 关闭开机自启
  
  ```

  + 通过公网`IP`访问,进入首页

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/rehatNginx.png" width="600" heihgt="200" alt="nginx">

  + 访问不了的话查看安全组(`添加端口号: 80`,阿里云防火墙只开启 `22`)

+ 停止`nginx`服务

  ```bash
  nginx -s stop
  ```

+ 卸载`nginx`

  ```bash
  yum remove nginx
  ```

+ 静态资源存放路径

  ```bash
  /usr/share/nginx/html [腾讯云]
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/nginxHt.png">

###  Nginx 常见配置

+ 全局段

  ```bash
  配置影响 nginx 全局的指令,一般有运行 nginx 服务器的用户组, nginx 进程 pid 存放路径,允许生成 worker process 数等
  ```

+ `events`段

  ```bash
  配置影响 nginx 服务与用户的网络连接,有每个进程的最大链接数、选取那种事件驱动模型处理连接请求，是否允许同时接受多个网络连接，开启多个网络连接序列化等。
  ```

+ `http段`

  ```bash
  可以嵌套多个 server、配置代理、缓存、日志定义等绝大数功能和第三方模块的配置、如文件引入，mime-type定义，日志自定义，是否使用 sendfile 传输文件、连接超时等时间，单连接请求数等。
  ```

+ `server段`

  ```bash
  配置虚拟主机的相关参数m主要有 IP 地址、端口号、域名
  ```

+ `location段`

  ```bash
  配置请求的处理方式
  ```

###  代理:

+ 正向代理

  ```bash
  在客户端(浏览器)配置代理服务器,通过代理服务器进行互联网访问。
  ```

+ 反向代理

  ```bash
  upstream{
  ···
  }
  ```

###  负载均衡



###  其他安装软件方法

```bash

# 搜索
yum search install-package-name 
# 下载
yum install -y install-package-name 
# 卸载
yum remove -y uninstall-package-name

# 参数意义
-y 遇到自动 yes

# 搜索 python
yum search python3 | grep programing # 源代码构建安装

# 软件更新,更新所有
yum update -y 

```

