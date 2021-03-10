---
title: gitcalendar 挂掉新修复
tags:
  - hexo
  - Butterfly
  - gitcalendar
categories: Butterfly
abbrlink: 54057
date: 2021-02-06 17:00:37
---

###  gitcalendar 挂掉新修复

+ 异常 - 数据不显示 报错

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/gitcalendar.png">



###  Vercel 使用

> <a href="https://vercel.com/dashboard">点击前往 Vercel 官网</a>

1. 注册账号（`github`）
2. 使用 Vercel 新建 `API`
3.  部署错误删除该部署

<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/deleteProj.png" width="400">

<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/20210206172348.png" width="600">



<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/deleteV.png" width="600">



4.  使用小冰老师提供的`API`导入,获取链接

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/other.png" width="400">

5.  获取部署后的 此格式地址`python-github-calendar-api-zeta.vercel.app`

6.   主题配置文件中添加如下

   ```bash
   gitcalendar:
     enable: true
     simplemode: true
     user: lovobin
     apiurl: python-github-calendar-api-zeta.vercel.app
     color: "['#e4dfd7', '#f9f4dc', '#f7e8aa', '#f7e8aa', '#f8df72', '#fcd217', '#fcc515', '#f28e16', '#fb8b05', '#d85916', '#f43e06']"
     
   ```

7. 个人修改了`js  api`前缀

   ```bash
   var githubapiurl = "https://python-github-calendar-api-zeta.vercel.app/api?/" + calendar.user;
   ```

8. 修复后 数据丢失

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/newG.png"  width="400">

9.  使用 Vercel  进行博客部署

   > <a href="https://learnmore.vercel.app/">Vercel 博客部署地址</a>

10. 更新部署

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/vercel.png" width="600">
    
    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/updateVercel.png" width="600">