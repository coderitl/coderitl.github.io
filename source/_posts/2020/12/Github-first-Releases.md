---
title: Github-first-Releases
tags: git
categories: Git
cover: 'https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/gitTree.png'
abbrlink: 37437
date: 2020-12-21 17:16:47
top_img:
---

###  记录自己的 github-first-releases(开源项目)

+ 演示

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/gitTree.png" title='记录第一次版本发布流程'>

###  如何发布一个版本

1.  进入一个想要发布的仓库

2.  点击仓库右侧`create a new release`

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/cnew.png">

3.  输入发布包的版本号。版本号基于 [Git 标签](http://git-scm.com/book/en/Git-Basics-Tagging),我们建议标签命名，符合[语义版本](http://semver.org/)。一般就是v1.0, v1.2.3这样, 或者对于测试版本, 可以像 v0.2-alpha 或者 v5.9-beta.3(当初忘记前缀了···)

4.  选择发布版本基于哪个目标

5.  如果发布包不稳定，选择`This is a pre-release` 来提醒用户这个是不能用于生产环境的

6.  输入标题和描述

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/infos.png">

7.  点击 `Publish release` 实现版本发布
8. 作为初学者眼中的版本控制(初学时的想法,等待更新····)