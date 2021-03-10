---
title: Python-Conda虚拟环境
tags:
  - python
  - conda
categories: Python
abbrlink: 21973
date: 2021-01-18 14:08:26
top_img:
---

###  Python-Conda虚拟环境

+ 创建虚拟环境

  + 默认位置

    + 查看当前环境有哪些虚拟环境

      ```bash
      conda info --envs
      ```

    + 创建

      ```bash
      # 创建虚拟环境
      conda create -n ENV python==3.6(ENV 是新建虚拟环境名称)
      ```

    + 获取虚拟环境位置

      ```bash
      
      # 进入 conda 安装位置
      where conda
      cd D:\ProgramData\Anaconda3\envs (your-path)
      # 进入创建的虚拟环境 ENV
      cd envs/your-venv
      ```

    + 激活虚拟环境

      ```bash
      cd Scripts
      
      activate your-venv-name
      
      ```

    + 退出虚拟环境

      ```bash
      deactivate env-name
      ```

    + 删除虚拟环境

      ```bash
      conda remove -n your-env-name --all
      ```

###  Windows Python2 虚拟环境

+ 指定位置

  ```bash
  创建目录
  mkdir your-proj-name
  
  cd your-proj-name
  
  ```

+ 依赖安装

  ```bash
  # 先进行安装
  
  pip install virtualenv
  ```

+ 创建虚拟环境

  ```bash
  # 创建虚拟环境
  virtualenv venv-name
  ```

+ 激活虚拟环境

  ```bash
  
  # 进入创建的虚拟环境文件夹
  cd venv-name
  
  # 激活虚拟环境
  # 进入 Scripts 文件夹
  cd Scripts
  # 激活
  activate venv-name
  ```

+ 删除虚拟环境

  ```bash
  直接删除相应目录
  ```

+ 成功后

  ```bash
  (your-venv-name)path:
  ```


###  Windows Python3 虚拟环境

+ 创建虚拟环境

  ```bash
  # cmd --> 进入指定位置 
  python -m venv new-venv-name
  ```

+ 激活虚拟环境

  ```bash
  # 显示
  dir
  # 进入 new-venv-name
  cd new-venv-name
  
  cd Scripts
  
  activate  new-venv-name
  
  ```

+ 环境测试

  ```bash
  # 安装 Flask
  pip instll flask
  ```

  + 进入`Python`交互式环境

    ```bash
    # 进入交互式环境
    python 
    # 导包
    import flask
    # 无显示正确
    ```

+ `Pycharm`使用

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/flaskVenv.png" width="600">

###  Flask项目使用虚拟环境

+ 使用

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/aloneVenv.png" width="600">

+ 项目测试

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/rightFlask.png">