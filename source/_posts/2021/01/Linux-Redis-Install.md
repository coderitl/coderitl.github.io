---
title: Linux-Redis-Install
tags:
  - Redis
  - Linux
categories: Linux
abbrlink: 54343
date: 2021-01-14 19:16:51
top_img:
---

###  Linux-Redis-Install

+ 搜索`Redis`

  ```bash
  yum search redis # 版本较旧
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/redis.png" title="直观显示">

###  源代码构建安装

```bash
Redis 中文文档: http://redisdoc.com/

Redis 官网: https://redis.io
```

+ 进入Redis官网

  ```bash
  获取下载地址
  
  https://download.redis.io/releases/redis-6.0.10.tar.gz
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/RedisUrl.png" width="400" title="点击查看大图">

+ 下载

  ```bash
  wget https://download.redis.io/releases/redis-6.0.10.tar.gz
  ```

+ 解压缩

  ```bash
  gunzip redis-6.0.10.tar.gz 
  ```

+ 解归档

  ```bash
  tar -xvf redis-6.0.10.tar 
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/gunzip.png">

+ 准备工作,进入解压文件夹

  ```bash
  cd redis-6.0.10/
  ```

+ 构建

  ```bash
  make
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/makeRedis.gif" title="构建中····">

+ 指定安装路径

  ```bash
  make PREFIX=/usr/local/redis install # 指定路径
  ```

+ 拷贝`redis`配置文件

  ```bash
  # 根目录下 
  cd ~
  # 进入解压后的 redis 文件见
  cd redis-6.0.10/
  # 拷贝配置文件到指定路径下
  cp redis.conf /usr/local/redis
  # 前往复制路径下
  cd /usr/local/redis
  # 查看文件
  ll (小写 L )
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/pathRedis.png" width="400">

+ 检测`Redis`是否正确安装

  ```bash
  # 所在目录
  /usr/local/redis
  # 版本信息检测
  redis-server --version
  
  # 输出以下信息为正确安装
  
  Redis server v=6.0.10 sha=00000000:0 malloc=jemalloc-5.1.0 bits=64 build=892cf79e664648a0
  
  ```

+ 检测客户端工具是否正确安装

  ```bash
   redis-cli --version
   
   # 输出以下信息为正确安装
   
   redis-cli 6.0.10
  
  ```

+ 检测哨兵

  ```bash
  redis-sentinel --version
  
  # 输出以下信息为正确安装
  
  Redis server v=6.0.10 sha=00000000:0 malloc=jemalloc-5.1.0 bits=64 build=892cf79e664648a0
  
  ```

+ 启动服务(<font color="red">请及时关闭，需要配置所以第一次需要开启</font>)

  + 前台模式(了解内容)

    ```bash
    # 前台式启动服务,交互式环境会被占用 ctrl + c 停止运行
    
    redis-server
    
    # 端口号的小故事 信息隐藏
    ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/finishRedis.png" width="600">

  + 后台式启动(**推荐**)

    ```bash
    redis-server &
    
    # 等一段时间后回车一下,进入 bash
    ```

    + 检测是否在后台运行(检测方法一)

      ```bash
      netstat -nap | grep 6379
      ```

    + `ps`查看进程(检测方法二)

      ```bash
      ps -ef | grep redis
      ```

    + `jobs`(检测方法三)

      <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/threeRedis.png">

  + 如过需要再次放回前台,执行以下命令

    ```bash
    # 根据 jobs 前的编号 [1]+
    
    fg %1
    
    # 编号为那个数字就执行: 
    
    fg %数字
    
    # 快捷键执行
    Redis放回后台: ctrl + z, 会停止进程，回车
    
    执行:
      fg %1
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/ingInfo.png">

+ 关闭`Redis`

  + 方法一

    ```bash
    # 类似于断电,一般不用,否则会造成数据丢失
    ps -ef | grep redis
    
    kill 1056726 # 执行再次按下回车
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/killRedis.png">

  + 方法二

    ```bash
    jobs 
    
    fg %1
    
    ctrl + c
    
    # 最后显示
    1060902:M 14 Jan 2021 20:19:49.435 # Redis is now ready to exit, bye bye...
    ```

  + 方法三（前两者作为了解,正常关机,推荐）

    ```bash
    redis-cli 
    
    shutdown # Redis 关机
    quit
    
    # 搜索不显示 带 grep的
    # ps -ef | grep redis | grep -v grep
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/shutdownRedis.png">

  + 配置配置文件进行后台启动

    ```bash
    # 224 shift+g | 224 gg 快速跳到指定行
    
    224行 # daemonize no
    
    # 修改守护进程
    
    daemonize yes
    
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/dacmon.png" title="直接放入后台运行">

+ 设置口令

  + 方法一(需重启服务)

    ```bash
    # 编辑配置文件
    vim redis.conf
    
    # 1. 进入后按下 Esc, :/\<requirepass  在 790 行,取消注释,修改后面的密码
    # 2. 790 gg | 790 shift + g
    
    # vim 查找 允许正则
    
    # 匹配开头（右斜杠+小于号）
    
    /\<关键字  # :/\<requirepass
    
    ```

  + 方法二

    ```bash
    两种方法前提: 后台运行 Redis服务
    redis-server redis.conf
    # 查看当前密码 默认空
    CONFIG SET requirepass # config get requirepass
    # 设置密码
    config set requirepass your-password
    # 显示 OK
    
    # 客户端工具连接
    redis-cli 
    # 密码认证
    auth 密码
    ```

  + `Redis 5.7`设置密码

    ```bash
    redis-server --requirepass your-password
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/requirepass.png">

+ 启动`Redis`最终方案

  ```bash
  ./bin/redis-server ./redis.conf
  
  # 下图为命令由来解释
  
  # Linux: history 命令使用
  history line-number # 执行历史命令，简化输入 
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/startRedis.png">

+ 检测密码是否设置成功

  ```bash
  # 启动客户端工具
  redis-cli
  # 连接成功后
  ping
  # 出现 (erro) 即为正确
  # 验证密码
  auth your-password
  # 出现 OK 即为登录成功
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/setPassword.png">

+ 性能测试（哔哩哔哩: 狂神说）

  ```bash
  redis-benchmark
  ```

  + 性能测试语法

    ```bash
    redis-benchmark [option] [option value]
    
    # 测试 并发连接 100 指定请求书 10000
    redis-benchmark -h localhost -p 6379 -c 100 -n 10000
    
    ```

  + 结果（分析输出结果）

    ```bash
    ====== PING_INLINE ======
      10000 requests completed in 0.16 seconds
      100 parallel clients
      3 bytes payload
      keep alive: 1
      multi-thread: no
    
    ====== PING_BULK ======
      10000 requests completed in 0.15 seconds # 对我们的 1万个请求进行写入测试
      100 parallel clients # 100 个并发客户端
      3 bytes payload # 每次写入 3 个字节
      keep alive: 1
      multi-thread: no
    
    # -------------------------------
    48.18% <= 1 milliseconds
    99.01% <= 2 milliseconds
    99.82% <= 3 milliseconds
    100.00% <= 3 milliseconds # 所有请求在 3 毫秒处理完成
    68493.15 requests per second  # 每秒处理 68493.15 次请求
    # ------------------------------- 
    
    # 作用: 理解 Redis 的速度
    
    ```

  + 参数

    | 序号 |   选项    | 描述                                       |  默认值   |
    | :--: | :-------: | :----------------------------------------- | :-------: |
    |  1   |  **-h**   | 指定服务器主机名                           | 127.0.0.1 |
    |  2   |  **-p**   | 指定服务器端口                             |   6379    |
    |  3   |  **-s**   | 指定服务器 socket                          |           |
    |  4   |  **-c**   | 指定并发连接数                             |    50     |
    |  5   |  **-n**   | 指定请求数                                 |   10000   |
    |  6   |  **-d**   | 以字节的形式指定 SET/GET 值的数据大小      |     2     |
    |  7   |  **-k**   | 1=keep alive 0=reconnect                   |     1     |
    |  8   |  **-r**   | SET/GET/INCR 使用随机 key, SADD 使用随机值 |           |
    |  9   |  **-P**   | 通过管道传输 <numreq> 请求                 |     1     |
    |  10  |  **-q**   | 强制退出 redis。仅显示 query/sec 值        |           |
    |  11  | **--csv** | 以 CSV 格式输出                            |           |
    |  12  |  **-l**   | 生成循环，永久执行测试                     |           |
    |  13  |  **-t**   | 仅运行以逗号分隔的测试命令列表。           |           |
    |  14  |  **-I**   | Idle 模式。仅打开 N 个 idle 连接并等待。   |           |

