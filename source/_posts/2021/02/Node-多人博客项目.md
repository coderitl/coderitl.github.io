---
title: Node-多人博客项目
tags:
  - Node
  - Node实战案例
categories: Node
abbrlink: 29171
date: 2021-02-18 10:05:56
top_img:
cover:
---



###  Node-多人博客项目



####  day01-案例初始化

1. 建立项目所需的文件夹

   + `public`静态资源存放目录
   + `model` 数据库操作存放目录
   + `route`路由存放目录
   + `views`模板

2. 初始化项目描述文件

   ```bash
   npm init -y
   ```

3.  下载项目所需的第三方模块

   ```bash
   npm install express mongoose art-template express-art-template
   ```

4.  创建网站服务器

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/nodeBlog.png">

5.  模块化路由

   ```javascript
   /***************** home *********************/
   
   /****************************/
   // home.js: 首页展示路由
   /****************************/
   
   // 实现模块化路由
   const express = require("express");
   const home = express.Router();
   
   // 创建二级路由
   home.get("/", (req, res) => {
     res.send("欢迎来到博客首页");
   });
   
   module.exports = home;
   
   
   /***************** admin *********************/
   
   /****************************/
   // admin.js 用户管理路由
   /****************************/
   
   // 实现模块化路由
   const express = require("express");
   const admin = express.Router();
   
   // 创建二级路由
   
   // 创建登录路由
   admin.get("/login", (req, res) => {
     res.render("admin/login");
   });
   
   
   
   // 将路由对象作为模块成员进行导出
   module.exports = admin;
   
   ```

   ```javascript
   app.js: 
   
       // 引入路由
       const home = require("./Node-Blog/route/home");
       const admin = require("./Node-Blog/route/admin");
   
       // 为路由匹配请求路径
       app.use("/home", home);
       app.use("/admin", admin);
   
   ```

   > `模板中的文件的相对路径是相对于浏览器的请求路径的,外联资源使用绝对路径 /`

6. 模板引擎配置使用

   ```javascript
   app.js:
   
       /***************************/
       // 配置模板引擎
       /***************************/
   
       // 告诉 express 框架模板所在的位置 'views 默认参数'
       app.set("views", path.join(__dirname, "Node-Blog", "views"));
       // 告诉 express 框架模板的默认后缀是什么 'view engine 默认参数'
       app.set("view engine", "art");
       // 当渲染后缀为 art 的模板时,所使用的模板引擎是什么
       app.engine("art", require("express-art-template"));
   
   ```

7. 开放静态资源文件

   ```javascript
   app.js:
   
   	// 开放静态资源文件
       const pathname = path.join(__dirname, "Node-Blog", "public");
       app.use(express.static(pathname));
   
   ```

   