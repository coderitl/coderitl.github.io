---
title: Hexo-文章管理
tags: Hexo
categories:
  - Hexo
abbrlink: 4221
date: 2020-12-19 12:56:22
---

###  Hexo-文章管理

+ 新建文章以年月层级划分显示

+ `hexo new [title]`后自动划分

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/HexoPage.png" width="400" title="文章层级划分">

+ 修改跟目录下的配置文件的如下配置

  ```bash
  
  permalink: :year/:month/:title/ # 默认格式 :year/:month/:day/:title/
  
  new_post_name: :year/:month/:title.md # File name of new posts 默认格式 :title.md
  
  # 其他修改请先注释以防错误自己无法恢复
  
  ```

###  Hexo-Buffterfly  下拉菜单添加

+ 效果预览

  {% folding  下拉菜单 %}

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/books.png">

  {% endfolding %}

+ 通过命令生成想要的`page`页名称

  ```bash
  hexo new page "Your page Name"
  ```

+ 在主题的配置文件中添加菜单

  ```bash
    在读书籍: 
      - JavaScript || /Javascript/ || fas fa-address-book
      - Node || /NodeBooks/ || fas fa-book-open
  ```

  {% note primary no-icon  %}

  一级导航显示名称:

  ​	-  这个名称任意起 || /(`hexo new page "Your page Name"`)/ ||  图标(可选)

  ​	-  这个名称任意起 || /(`hexo new page "Your page Name"`)/ ||  图标(可选)

  {% endnote %}