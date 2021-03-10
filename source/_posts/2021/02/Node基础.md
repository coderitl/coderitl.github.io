---
title: Node基础
tags:
  - Node
  - Javascript
categories: Node
abbrlink: 14551
date: 2021-02-04 09:21:41
top_img:
cover:
---

### Node基础

####  命令行基础

+ 常用指令
  1. `Win+r`调出`DOS`窗口

  2. `cd`目录名 进入指定目录

  3. `md`目录名 创建一个文件夹

  4. `rd` 目录名 删除一个文件夹

+ 目录

  1. `.`表示当前目录
  2. `..`表示上一级目录

+ 环境变量

####  进程和线程

> 
>
> 进程: 进程负责为程序的运行提供必备的环境
>
> 线程: 线程计算机中的最小的计算单位，线程负责执行进程中的程序
>
> Node的服务器是单线程的: Node 处理请求时是单线程,但是在后台拥有一个I/O线程池
>
> 

####  Node 简介

+ 简介

  ```javascript
  1. Node.js 是一个能够在服务器端运行 Javascript 的开放源代码、跨平台 Javascript 运行环境。
  2. Node 采用Google开发的 V8 引擎运行 js 代码，使用事件驱动、非阻塞和异步I/O模型等技术来提高性能、可优化应用程序的传输量和规模。
  ```



####  Node 安装使用

+ 安装  <a href="https://nodejs.org/en/">点击前往 Node 官网</a>

+ 检测

  ```javascript
  node --version
  ```

  + 成功显示版本号

  + 安装失败错误代码`2502,2503`

    1. 安装权限不足
       + 以管理员身份运行`powershell: windows+x `
       + 输入运行安装包命令`msiexec/package [ D:\Program Files\nodejs\replace-your-node-path  node-v10.13.0-x64.msi your-node-version`

    2. 安装验证失败

       ```bash
       添加系统环境变量
       
       找到系统中的 node.exe 的路径添加系统环境变量后退出执行:
       
       windows+r: cmd  node -v
       
       ```

       <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/nodepath.png" width="600">

+ 使用

  ```javascript
  node 文件名.js
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/helloNode.png" width="400">

+ 模块化

  ```javascript
  - 在 Node 中 一个 js 文件就是一个模块
  - 在 Node 中,每一个 js 文件中的 js 代码都是独立运行在一个函数中
  
  模块分成两大类:
      核心模块:
          1. 由 Node 引擎提供的模块
          2. 核心模块的标识就是模块的名称
      文件模块:
  	1. 由用户自己创建的模块
          2. 文件模块的标识就是文件的路径(绝对路径、相对路径)
  			
  			相对路径使用  . 或 .. 开头
  ```

+ 外部模块引入

  ```javasc
  在 node 模块中,通过 require() 函数来引入外部的模块
      
      require() 可以传递一个文件的路径作为参数, node 将会自动根据该路径来引入外部模块
  
      使用 require() 引入模块以后,该函数会返回一个对象，这个对象代表是引入的模块
      
      exports 向外部暴露变量和方法
  	只需要将需要暴露给外部的变量或方法设置为 exports 的属性
  	
  ```

+ `exports`使用

  ```javascript
  A.js: exports.x = 'Hello World 模块的 x '
  
  B.js: 
  
  	引入 A 模块: var md = require('file-path/A');
  					console.log(md.x) // B模块输出: Hello World 模块的 x
  
  exports 是 module.exports 的别名(地址引用关系),导出对象最终以 module.exports 为准。
  
  ```

+ `global`

  ```javascript
  在 node 中有一个全局对象 global 它的作用和网页中 window 类似
  
  在全局中创建的变量都会作为 global 的属性保存
  
  在全局中创建的函数都会作为 global 的方法保存
  
  当 node 执行模块中的代码时,它会首先在代码的最顶端,添加如下代码
  function(exports,require,modelm__filename,__dirname{
            
            在代码最底部,添加如下代码
            }
  ```

#### 包（package）

+ `package`
  1. `CommonJS` 的包规范允许我i们将一组相关的模块泽合到一起，形成一组完整的工具
  2.  `CommonJS` 的包规范由包结构和包描述文件两个部分组成

+ 包结构: 用于组织包中的各种文件

  ```javascript
  包实际上就是一个压缩文件,解压后还原为目录。符合规范的目录,应该包含如下文件:
  
      - package.json 描述文件
      - bin 可执行二进制文件
      - doc 文档
      - test 单元测试
       
  ```

+ 包描述文件: 描述包的相关信息，以供外部读取分析

+ `npm(Node Package Manager)`

  ```javascript
  npm search package-name // 搜索
  
  npm install package-name // 下载
  
  ```

+ 配置`cnpm`

  ```javascript
  // 安装 cnpm
  npm install -g cnpm --registry=https://registry.npm.taobao.org || npm install --global cnpm
  
  // 常用命令
  安装包
  cnpm i <pkg>  或者 cnpminstall <pkg>  或者  cnpm i <pkg>@<version>  或者  cnpminstall <pkg>@<version>
  
  卸载包
  cnpm uninstall <name> 或者 cnpm uninstall <name>@[<version>]
  
  查看当前项目下的包列表
  cnpm ls
  
  查看全局包列表
  cnpm ls －g
  
  清理缓存
  cnpm cache clean
                                                  
  ```





###  Node



####  系统模块



#####  读写文件

+ `fs`

  ```javascript
  
  fs 是 file-system 的简写 就是文件系统的意思
  
  在 node 中如果想要进行文件操作，就必须引入 fs 这个核心模块
  
  fs.readFile('文件路径/文件名称',['文件编码'],callback)
  ```

+ 文件读取

  ```javascript
    第一个参数就是要读取的文件路径
    第二个参数就是回调函数
          成功
              data 数据
              error null
          失败
              data null
              error 错误对象
  ```

  ```javascript
  // 引入 fs 模块
  var fs = require('fs');
  // 文件读取
  fs.readFile("./b.txt", function (error, data) {
    if (error) {
      console.log("读取文件失败");
      return;
    } else {
      console.log(data.toString());
    }
  ```

+ 写文件

  ```javascript
  第一个参数: 文件路径
  第二个参数: 文件内容
  第三个参数: 回调函数
  
  error
  	成功: 
  		文件写入成功
          error --> null
  	失败: 
  		文件写入失败
          error 就是错误对象
     
   fs.writeFile('文件路径/文件名称','数据',callback);

  ```
  
  ```javascript
  var fs = require('fs');
  fs.writeFile('./file-name','write-content',function(error){
      if(error){
          console.log('写入失败');
      }else{
          console.log('文件写入成功···');
      }
})
  ```

+ 系统模块`path`路径操作

  ```javascript
  path.join('路径','路径',····)
  ```

  ```javascript
  // 主要是由于系统不同使用的路径分隔符不同
  // 拼接如下路径 public/img/avatar
  
  const path = require("path");
  const filepath = path.join("public", "img", "avatar");
  
  console.log(filepath);
  
  ```

+ 相对路径、绝对路径

  ```javascript
  1. 大多数情况下使用绝对路径,因为相对路径有时候相对的是命令行工具的当前工作目录
  2. 在读取文件或者设置文件路径时都会选择绝对路径
  3. 使用 __dirname 获取当前文件所在的绝对路径
  ```

+ 第三方模块

  ```javascript
  别人写好的m具有特定功能,我们能直接使用的模块即第三方模块，由于第三方模块都是由多个文件组成并且被放置在一个文件夹中,所以又名包名。
  
  https://www.npmjs.com/
  ```

  

####  第三方模块

+ 第三方模块`nodemon`,很有必要安装使用,修改内容将会实时刷新,无需重新启动

  ```bash
  # 下载 
  npm install nodemon --global
  
  #检测安装
  nodemon -v
  
  # 使用
  nodemon node-fils-name.js
  
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/nodemon.png" width="600">

+ 第三方模块`nrm`

  ```bash
  nrm(npm registry manager): npm 下载地址切换工具 npm 默认下载地址在国外,国内下载速度慢
  
  # 安装 nrm
  npm install nrm -g
  # 显示可用下载列表
  nrm list
  # 使用可用 镜像
  nrm use taobao
  #  * 代表当前在用镜像
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/nrm.png" alt="下载失败" width="600">

  + 解决方案(未尝试)

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/nrmresult.png">

+ 第三方模块`gulp`

  1. `gulp`能做什么

     ```bash
     项目上线 HTML CSS JS 文件压缩
     语法转换(es6,less)
     公共文件抽离
     ```

  2. `gulp`使用步骤

     + 项目中下载`gulp`库文件,要使用项目中根目录下执行`npm install gulp`

     + 在项目根目录下新建`gulpfile.js`文件，只能是这个文件名
     + 重构项目的文件夹结构 `src` 目录放置源代码文件 `dist`目录放置构建后文件
     + 在 `gulpfile.js`文件中编写任务
     + 在命令行工具中执行`gulp`任务

  3.  `gulp`中提供的方法

     + `gulp.src()`获取任务要处理的文件
     + `gulp.desc()`输出文件
     + `gulp.task()`建立gulp任务
     + `gulp.watch()`监控文件的变化

     + 使用`gulp`

       <img src='https://gitee.com/wang_hong_bin/repo-bin/raw/master/gulp.png'>

       ```javascript
       " npm install gulp "
       
       // 引入 gulp
       const gulp = require("gulp");
       // 使用 gulp.task() 方法建立任务
       // 参数: 1.任务的名称
       // 参数: 2. 任务的回调 
       gulp.task("first", () => {
         // 获取要处理的文件
         gulp
           .src("./src/css/index/style.css") // src: 目录自定义 自动会生成
           // 将处理后的文件输出到 dist 目录，dest输出
           .pipe(gulp.dest("./dist/css/index")); // dist: 目录自定义 自动会生成
       });
       // 全局安装命令工具 npm install gulp-cli -g
       ```

       + 下载命令工具,全局安装(全局安装: 多个项目都会使用, 库文件则不同)

         ```bash
         # 安装
         npm install gulp-cli -g
         # 检测
         gulp -v
         # 使用
         gulp task-name [Eg. first]
         ```

         <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/gulpfirst.png">

     + `gulp`插件
       1. `gulp-htmlmin` html 文件压缩
       2.  `gulp-csso`压缩css
       3. `gulp-babel`JavaScript语法转换
       4. `gulp-less`语法转换
       5. `gulp-uglify`压缩混淆 JavaScript
       6. `gulp-file-include`公共文件包含
       7. `browsersync` 浏览器实时同步

     + 使用插件

       ```bash
       下载插件文档: https://www.npmjs.com/package/gulp-htmlmin
       
        npm install --save gulp-htmlmin
        
       ```

       + 新建压缩 html 任务(先了解,等待后续补充)

         ```javascript
         // 引入 gulp
         const gulp = require("gulp");
         // 引用插件
         const htmlmin = require("gulp-htmlmin");
         
         
         // html 任务 压缩 html
         // 建立任务
         gulp.task("htmlmin", () => {
           return (
             gulp
               // 获取处理任务路径
               .src("./src/*.html")
               // 压缩 html 文件中的代码 collapseWhitespace 压缩空格? true 是 pipe( 任务事件 )
               .pipe(htmlmin({ collapseWhitespace: true }))
               // 输出
               .pipe(gulp.desc("dist"))
           );
         });
         ```

       + 原 `html `文件格式

         <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/yuanhtml.png" width="600">

       + 压缩后

         <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/htmlmin.png">

       + `构建`任务

         ```javascript
         // 构建任务  所有任务 通过 gulp default 全部执行
         gulp.task('default',['htmlmin','first']);
         
         ```

         

####  package.json

> 
>
> `node_modules` 无需传输，使用`npm install ` 会自动前往 `package.json` 寻找依赖下载
>
> 项目描述文件,记录当前项目的项目信息,例如: 项目名称 版本 作者` github` 地址 当前项目依赖了那些第三方模块 使用 `npm init -y` 生成
>
> 

+ `npm init -y`

  ```bash
  {
    "name": "node-day03", 
    "version": "1.0.0",
    "description": "",
    "main": "gulp-demo.js",
    "dependencies": { # 项目依赖
      "gulp": "^4.0.2",
      "gulp-file-include": "^2.3.0",
      "gulp-htmlmin": "^5.0.1"
    },
    "devDependencies": {}, # 开发依赖 --save 
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC" # 开放源代码协议
  }
  
  ```

+ 开发依赖
  1. 在项目的开发阶段需要依赖，线上运营阶段不需要依赖第三方包，称为开发依赖
  2.  使用 `npm install` 包名 `--save-dev` 命令将包名添加到`package.json`文件的 `devDependencies`字段中

+ `package-lock.json`文件的作用
  1. 锁定包的版本,确保再次下载时不会因为包版本不同产生问题
  2.  加快下载速度, 因为该文件中已经记录了项目所依赖第三方包的树状结构和包的下载地址，重新安装时只需下载即可,不需做额外工作

+ 命令别名

  ```javascript
  package.json: 
      "scripts": {
          "test": "echo \"Error: no test specified\" && exit 1",
          "build": "nodemon app.js"
        }
         
  
  "build": "命令"
  
  "build": "nodemon app.js"
  
  # 执行
  npm run 别名 Eg. npm run build
  
  ```



####   服务器端基础概念

+ 网站服务器

  ```bash
  能够提供网站访问服务的机器就是网站服务器,它能够接受客户端的请求,能够对请求做出响应。
  ```

+ URL

  ```bash
  统一资源定位符,又叫 URL(uniform ResourceLocator) 是专门标识 Internet 网上资源位置而设的一种编址方式
  ```

+ URL 的组成

  ```bash
  输出协议://服务器 ip或域名:端口/资源所在位置标识
  
  https://lovobin.github.io:80/2021/02/Node%E5%9F%BA%E7%A1%80/
  
  http: 超文本传输协议, 提供了一种发布和接受 HTML 页面的方法
  
  ```

  

####  简单的 http 服务



+ 搭建简单的服务器

  ```javascript
  // 加载 http 核心模块
  var http = require("http");
  // 使用 http.createServer() 方法创建一个 Web 服务器 返回一个 server 实例
  var server = http.createServer();
  
  /*
      当客户端请求过来,就会自动触发服务器的 request 请求事件,  然后执行第二个参数: 回调处理
  */
  server.on("request", function (request, response) {
    console.log("收到客户端的请求了··" + request.url);
  
    /*
        response 对象有一个方法 write 可以用来给客户端发送响应数据
        write 可以使用多次,但是最后一定要使用 end 来结束响应 否则客户端会一直等待
        */
    response.write("响应···");
    // 告诉客户端 我的话说完了 你可以直接呈递给用户
    response.end();
  });
  
  // 绑定端口号
  server.listen(3031, function () {
    console.log("服务器启动成功，可以通过 http://127.0.0.1:3000/ 进行访问了");
  });
  
  ```

+ 请求路径获取响应

  + 普通文本响应

    ```javascript
    // 引入 http 模块
    var http = require("http");
    // 创建 server
    var server = http.createServer();
    // 发送
    server.on("request", function (request, response) {
        console.log("收到请求了: " + request.url);
        // 根据不同的请求的路径,响应不同的内容
        var url = request.url;
        if (url === "/") {
            response.end("index Page");
        } else if (url === "/login") {
            response.end("user login");
        } else if (url === "/register") {
            response.end("user register");
        } else {
            response.end("response ·····");
        }
    });
    // 绑定端口号
    server.listen(3101, function () {
        console.log("服务器启动成功···可以通过127.0.0.1:3031 来访问了");
    });
    
    ```

  + 响应 `json`数据类型

    ```javascript
    // 引入 http 模块
    var http = require("http");
    // 创建 server
    var server = http.createServer();
    // 发送
    server.on("request", function (request, response) {
        // 配置响应编码
        response.setHeader("Content-Type", "[text/plain 根据类型变化可选];charset=utf-8");
        console.log("收到请求了: " + request.url);
        // 根据不同的请求的路径,响应不同的内容
        var url = request.url;
        // 定义json 类型数据
        var products = [
            {
                brand: "xiaomi",
                price: 6699,
                color: "blue",
            },
            {
                brand: "iPhone",
                price: 9988,
                color: "purple",
            },
            {
                brand: "huawei",
                price: 9988,
                color: "blue",
            },
        ];
        // 响应的内容只能是 二进制数据或者字符串
        if (url === "/products") {
            console.log(JSON.stringify(products));
            response.end(JSON.stringify(products));
        }
    });
    // 绑定端口号
    server.listen(3101, function () {
        console.log("服务器启动成功···可以通过127.0.0.1:3031 来访问了");
    });
    
    ```

+ 常见`Content-Type`类型

  ```javascript
  常见的媒体格式类型如下：
      text/html  HTML格式
      text/plain 纯文本格式
      text/xml  XML格式
      image/gif gif图片格式
      image/jpeg jpg图片格式
      image/png png图片格式
  ```



####  HTTP 协议

+ http 协议的概念

  ```bash
  超文本传输协议(英文: HyperText Transfer Protocol 缩写: HTTP) 规定了如何从网站服务器传输超文本到本地浏览器,它基于客户端服务器加构工作,是客户端服务器加构工作,是客户端和服务器端请求和应答的标准。
  ```

+ 报文

  ```bash
  在 HTTP 请求和响应的过程中传递的数据块就叫报文m包括要传送的数据和一些附加信息,并且要遵循规定好的格式。
  ```

+ 请求报文

  1. 请求方式

     + `GET`
     + `POST`

  2.  请求地址

     ```javascript
     server.on('request',(req,res)=>{
         req.headers // 获取请求报文
         req.url // 获取请求地址
         req.method // 获取请求方式
     })
     ```

     

####  HTTP 请求与响应处理

+ GET 参数请求处理

  ```javascript
  // http请求与响应.js
  const http = require("http");
  const server = http.createServer();
  // 处理 url
  const url = require("url");
  // req: request res: response
  server.on("request", (req, res) => {
    res.writeHeader(200, {
      "content-type": "text/plain;charset=utf8",
      hello: "world",
    });
  
    // 请求参数处理 http://127.0.0.1:3031/?username=zhangsan&age=18
    console.log(req.url); // /?username=zhangsan&age=18
    // 字符串截取可以获取参数
    // 内置模块
    console.log(url.parse(req.url));
    /*
      1. 要解析的 url 地址
      2. 将查询的参数解析成对象形式
  
      url.parse(req.url,true)
    */
    let params = url.parse(req.url, true).query;
    console.log("params: ", params);
  
    console.log("params-username:", params.username, "params-age:", params.age); // zhangsan 18
    res.end("请求成功");
  });
  server.listen(3031, (error) => {
    console.log("可以通过 127.0.0.1:3031/ 来访问服务器了····");
  });
  
  
  // 路径判断问题
  let {query,pathname}=url.parse(req.url,true);
  console.log(query.username,query.age);
  if(pathname=='/index' || pathname=='/'){
      res.end('index home')
  }
  
  ```

  

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/getParse.png" width="400">

+ POST 参数请求处理

  ```javascript
  // post请求参数.js
  // http请求与响应.js
  const http = require("http");
  const server = http.createServer();
  // 处理请求参数模块 post 请求转换为 对象数据
  const queryString = require("querystring");
  // req: request res: response
  server.on("request", (req, res) => {
    // 编码处理
    res.writeHeader(200, {
      "content-type": "text/plain;charset=utf8",
    });
    // post 参数是通过事件的方式接受的
    // data 当请求参数传递的时候触发 data 事件
    // end 当参数传递完成的时候触发 end 事件
    // username=aidou&password=123
    let postParams = "";
    req.on("data", (params) => {
      postParams += params;
    });
    req.on("end", () => {
      console.log(postParams);
      let querystr = queryString.parse(postParams);
      console.log(querystr); // { username: 'aidou', password: '123' }
    });
    res.end("ok");
  });
  server.listen(3031, (error) => {
    console.log("可以通过 127.0.0.1:3031/ 来访问服务器了····");
  });
  
  ```

  

####  路由

> 路由是指客户端请求地址与服务器端程序代码的对应关系

+ 路由处理

  ```javascript
  const http = require("http");
  const server = http.createServer();
  const url = require("url");
  server.on("request", (req, res) => {
    res.writeHeader(200, {
      "content-type": "text/html;charset=utf8",
    });
    // 获取请求方式
    const method = req.method.toLowerCase();
    console.log(method); // GET---  toLowerCase() ---> get
    // 获取请求地址
    const pathname = url.parse(req.url).pathname;
    console.log("pathname: ", pathname); // pathname:  /index
    if (method == "get") {
      if (pathname == "/" || pathname == "/index") {
        res.end("<h1> return get index home page </h1>");
      } else {
        res.end("<h1>Not Found GET</h1>");
      }
    }
    if (method == "post") {
      if (pathname == "/" || pathname == "/index") {
        res.end("<h1> return post index home page </h1>");
      } else {
        res.end("<h1>Not Found POST</h1>");
      }
    }
  });
  
  server.listen(3031, (error) => {
    console.log("ok");
  });
  ```

+ 静态资源访问

  ```javascript
  服务器端不需要处理,可以直接响应给客户端的资源就是静态资源，例如 css javascript image 文件等
  ```

  + 获取访问路径
  
    ```javascript
    # 获取 pathname  
    url.parse(req.url).pathname
    ```
  
  + 获取当前文件的绝对路径
  
    ```javascript
    # path 模块
    
    path.join(__dirname, "public" + pathname)
    
    ```

+ 静态资源读取

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/pathnameDefault.png">

  ```javascript
  # app.js
      const http = require("http");
      const url = require("url");
      const path = require("path");
      const fs = require("fs");
  
      const server = http.createServer();
  
      server.on("request", (req, res) => {
        res.writeHead(200, {
          "content-type": "text/html;charset=utf8",
        });
        // 响应文件路径
        let pathname = url.parse(req.url).pathname;  
        
          #   pathname = pathname == "/" ? "/default.html" : pathname; 更新显示判断
          
        // 绝对路径获取 url
        let realPath = path.join(__dirname, "public" + pathname);
        fs.readFile(realPath, (error, data) => {
          if (error != null) {
            res.end("读取失败···");
            return;
          } else {
            res.end(data);
          }
        });
      });
  
      server.listen(3031, (error) => {
        console.log("ok");
      });
  
  ```

+ `mime`模块

  ```bash
  npm install mime
  const mime = require('mime');
  
  let type = mime.getType(realPath);
  res.writeHead(200,{
  	'content-type': type
  });
  
  ```

  

####  同步`API`和异步`API`

1. 同步API

   > 只有当前 `API` 执行完成后,才能继续执行下一个 `API`

2.  异步 API

   > 当前 API 的执行不会阻塞后续代码的执行

3. 比较

   ```javascript
   
   
   // 同步 sync
   console.log("before···");
   setTimeout(() => {
    // 异步 async 
     console.log("last···");
   }, 20);
   console.log("after···");
   
   
   ```

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/async.png" width="400">

4.  同步 `API` 和异步` API `的区别

   > 
   >
   > 同步 API 可以从返回值中拿到 API 的执行结果,但是异步 API 是不可以的
   >
   > 同步 API 从上到下依次执行，前面代码会阻塞后面代码的执行。（会等待循环结束后才会执行后面的代码）
   >
   > 异步 API 不会等待 API 执行完成后再向下执行代码
   >
   > 

   ```javascript
   ------------------------------------- 1 ----------------------------------
   // 同步函数返回值问题
   function sum(n1, n2) {
     return n1 + n2;
   }
   const value = sum(2, 3);
   console.log(value); // 5
   
   // 异步函数返回值问题
   function getMsg() {
     setTimeout(() => {
       return "异步执行";
     }, 20);
   }
   const msg = getMsg();
   console.log("return msg result: ", msg); // undefined
   
   ---------------------------------- 2: 同步 -------------------------------------
   
   for (var i = 0; i < 10; i++) {
       console.log(i); // 同步会等待循环结束后才会执行后面的代码
   }
   console.log('for 循环后面的代码');
   
   ---------------------------------- 3: 异步 -------------------------------------
       
   console.log("code start running···············");
   setTimeout(() => {
     console.log("0.2 start code············");
   }, 20);
   
   setTimeout(() => {
     console.log("0 start code············");
   }, 0);
   console.log("code running end·············");
   
       
   ```

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/until.png" width="500">

5. 回调函数

   ```javascript
   作用: 可以拿到异步函数的返回值
   
   // TODO: 异步函数通过回调函数获取返回值
   function getData(callback) {
     setTimeout(() => {
       callback({
         msg: "hello node js",
       });
     });
   }
   getData(function (data) {
     console.log(data);
   });
   
   ```

   

####  Promise 

> promise 出现的目的是解决 Node.js 异步编程中回调地狱的问题。

+ promise的基本使用方法

  ```javascript
  const fs = require("fs");
  let promise = new Promise((resolve, reject) => {
    // 读取文件
    fs.readFile("D.txt", "utf8", (error, data) => {
      if (error) {
        reject(error);
      } else {
        resolve(data.toString());
      }
    });
  });
  
  promise
    .then((result) => {
      console.log(result);
    })
    .catch((error) => {
      console.log(error);
    });
  ```

+  顺序读取文件

  ```javascript
  // 难以维护 
  const fs = require("fs");
  fs.readFile("./A.txt", "utf8", (error, data) => {
    console.log(data.toString());
    fs.readFile("./B.txt", "utf8", (error, data) => {
      console.log(data.toString());
      fs.readFile("./C.txt", "utf8", (error, data) => {
        console.log(data.toString());
      });
    });
  });
  
  ```

+ 解决`Node.js`回调地狱问题

  {% folding Node回调地狱问题 %}
  
  ```javascript
  // promise 的基础使用 解决Node.js 的回调地狱
  
  function p1() {
    return (promise1 = new Promise((resolve, reject) => {
      // 读取文件
      fs.readFile("A.txt", "utf8", (error, data) => {
        if (error) {
          reject(error);
        } else {
          resolve(data.toString());
        }
      });
    }));
  }
  
  function p2() {
    return (promise2 = new Promise((resolve, reject) => {
      // 读取文件
      fs.readFile("B.txt", "utf8", (error, data) => {
        if (error) {
          reject(error);
        } else {
          resolve(data.toString());
        }
      });
    }));
  }
  
  function p3() {
    return (promise3 = new Promise((resolve, reject) => {
      // 读取文件
      fs.readFile("C.txt", "utf8", (error, data) => {
        if (error) {
          reject(error);
        } else {
          resolve(data.toString());
        }
      });
    }));
  }
  
  
  p1()
    .then((r1) => {
      console.log(r1);
      return p2();
    })
    .then((r2) => {
      console.log(r2);
      return p3();
    })
    .then((r3) => {
      console.log(r3);
    });
  ```
  
  {% endfolding %}

####  异步函数

> 异步函数就是异步编程语法的终极解决方案,它可以让我们将异步代码写成同步的形式让代码不再有回调函数嵌套，使代码变得清晰明了。

+ `async` 关键字

  1. 普通函数定义前加`async`关键字  普通函数就变成异步函数

  2.  异步函数默认返回 `promise`对象

  3.  在异步函数内部使用 `return` 关键字进行结果返回 结果会被包裹再 `promise`对象中 return 关键字代替了 `resolve()`

  4.  在异步函数内部使用 `throw` 关键字抛出程序异常

  5.  调用异步函数再链式调用 `then `方法获取异步函数执行结果

  6.  调用异步函数再链式调用 `catch`方法获取异步函数执行的错误信息

     ```javascript
     // 异步函数
     async function fn() {
       throw 'throw error infomation';
       return "return result data";
     }
     console.log(fn()); //默认输出: Promise { undifined }
     
     
     // then方法 catch方法
     fn()
       .then((data) => {
         console.log(data); // 成功: Promise { 'return result data' }
       })
       .catch((error) => {
         console.log(error); //失败: Promise { <rejected> 'throw error infomation' }
       });
     
     ```

+ `await`关键字

  1. `await`关键字`只能`出现在异步函数中
  2.  `await promise await`后面只能写`promise`对象  写其他类型的 `API` 是不可以的
  3.  `await`关键字是可以暂停异步函数向下执行 知道 `promise`返回结果

  ```javascript
  async function fn1() {
    return "fn1";
  }
  async function fn2() {
    return "fn2";
  }
  async function fn3() {
    return "fn3";
  }
  
  // 顺序执行 异步函数
  async function runFn() {
    let r1 = await fn1();
    let r2 = await fn2();
    let r3 = await fn3();
    console.log(r1, r2, r3);
  }
  
  runFn();
  
  ```

+ 使用异步函数顺序读取文件

  ```javascript
  const fs = require("fs");
  const promisify = require("util").promisify;
  const readFile = promisify(fs.readFile);
  
  async function run() {
    let r1 = await readFile("./A.txt", "utf8");
    let r2 = await readFile("./B.txt", "utf8");
    let r3 = await readFile("./C.txt", "utf8");
    console.log(r1, r2, r3);
  }
  run()
  
  ```

  

####  数据库

+ 概念

  |     术语     |                       解释说明                        |
  | :----------: | :---------------------------------------------------: |
  |  `database`  |    数据库`mongogdb` 数据库软件中可以建立多个数据库    |
  | `collection` |  集合 一组数据的集合 可以理解为 JavaScript 中的数组   |
  |  `document`  |    文档 一条具体的数据 可以理解为 JavaScript 对象     |
  |   `field`    | 字段 文档中的属性名 可以理解为 JavaScript中的对象属性 |

+ 第三方包

  + `使用 Node.js`操作Mongodb数据库需要依赖`Node.js`第三方包`mongoose`

    ```bash
    npm install mongoose
    ```

  + 启动`mongodb`服务

    ```bash
    net start mongodb
    ```

  + 关闭`mongodb`服务

    ```bash
    net stop mongodb
    ```

  + 启动遇到如下错误

    ```bash
    
    ‘环境变量’  bin/
    
    发生系统错误 5。
    
    拒绝访问。
    
    解决: 使用管理员权限启动 mongodb 服务
    
    chdir 命令: 获取 windows 的路径 == pwd
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/adminMon.png" width="600" alt="普通管理员" title="普通管理员">

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/netStartMon.png" width="600" alt="超级管理员" title="超级管理员">

+ `Nodes`连接数据库

  ```javascript
  // 引入 mongoose  模块
  const mongoose = require("mongoose");
  mongoose
    .connect("mongodb://localhost/student", {
      useNewUrlParser: true,
      useUnifiedTopology: true 
    })
    .then(() => {
      console.log("数据库连接成功");
    })
    .catch((error) => {
      console.log(error, "连接失败");
      return;
    });
  
  ```

+ 创建集合

  ```javascript
  创建集合分为两个步骤:
  	1. 对集合设定规则
      2. 创建集合
      创建 mongoose.Schema 构造函数的实例即可创建集合
  ```




####  模板引擎

+ 模板引擎

  ```bash
  模板引擎是第三方模块
  
  让开发者以更加友好的方式拼接字符串,使项目代码更加清晰,更加易于维护。
  ```

+ 模板引擎下载

  ```bash
  npm install art-template
  ```

+ 模板引擎的使用

  ```javascript
  const template = require('art-template');
  const html = template('模板路径',数据);
  ```

+ 模板引擎基础使用

  ```javascript
  // 导入模板引擎
  const template = require("art-template");
  // 引入系统模块 path
  const path = require("path");
  // 路径拼接
  const views = path.join(__dirname, "views", "index.art");
  
  const html = template(views, {
    age: 10,
    name: "Node",
  });
  console.log(html);
  
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/arttemplate.png" width="300">

+ 输出,支持运算符

  1. 标准语法

     ```javasc
     {{ name }}
     ```

  2.  原始语法

     ```javascript
     <%= name %>
     ```

  3.  原文解析

     ```javascript
     app.js:
     	{
             name: "<h3>Node</h3>"
         }
     
     -------------------------------------
     {{@ name }} // 输出: <h3>Node</h3>
      
     <%- name %> // 输出: <h3>Node</h3>
         
     ```

+ 条件判断

  ```javascript
  {{if age>30 }}
  年龄过大
  {{ else if age<15}}
  {{ age }}
  {{/if}}
  ```

+ 循环

  ```javascript
  {{ each 数据}}  {{/each}}
  ```

  

+ 子模板

  ```javascript
  使用子模板可以将网站公共区块(头部、底部)抽离到单独的文件中。
  ```

  ```javascript
  // 标准语法: 引入头部
  {{include './commen/header.art'}}
  // 原始语法: 引入底部
  <% include('./commen/footer.art') %>
  ```

+ 模板继承

  ```javascript
  使用模板继承可以将网站 HTML 骨架抽离到单独文件中,其他页面模板可以继承骨架文件。
  ```

  ```javascript
  // 留坑
  {{block 'name'}} {{/block}}
                     
   // 继承
  {{extend 'path/art-template name'}}
  // 填充
  {{block 'name'}}  填充 {{/block}}
  ```

+ 模板配置

  ```javascript
  1. 向模板中导入变量 template.defaults.imports.变量名 = 变量值;
  2. 设置模板根目录 template.defaults.root = 模板目录;
  3. 设置模板默认后缀 template.defaults.extname='.art'
  ```

+ 路由模块

  ```bash
  npm install router
  ```

  + 使用步骤
    1. 获取路由对象
    2.  调用路由对象提供的方法创建路由
    3.  启用路由,使路由生效

  ```javascript
  
  /*********************************************/
  // 引入路由模块
  const getRouter = require("router");
  // 获取路由对象
  const router = getRouter();
  // TODO:  test 路由
  router.get("/test", (req, res) => {
    res.end("/test");
  });
  
  // TODO: index 路由
   router.get("/index", (req, res) => {
    res.end("/index");
  });
  /*********************************************/
  
  
  server.on("request", (req, res) => {
    // 启用路由 必填参数
    router(req, res, () => {
      console.log("被调用");
    });
    // 启用静态资源 fn 必填参数
      serve(req, res, () => {
      
    });
  });
  
  
  
  ```

+ 第三方模块`serve-static`

  ```bash
  功能: 实现讲台资源访问服务
  ```

  + 下载

    ```bash
    npm install serve-static
    ```

  + 使用步骤

    1. 引入 `serve-static`模块获取创建静态资源服务功能的方法
    2.  调用方法创建静态资源服务并指定静态资源服务目录
    3.  启用静态资源服务功能

  ```javascript
  
  /*********************************************/
  // 引入静态资源模块
  const serveStatic = require("serve-static");
  // 实现静态资源访问 参数为静态资源目录
  const serve = serveStatic(path.join(__dirname, "public"));
  /*********************************************/
  
  
  
  server.on("request", (req, res) => {
  
    // 启用静态资源 fn 必填参数
      serve(req, res, () => {
      
    });
  });
  
  ```

  

####  Express 框架

#####  `express`



```javascript
Express 是一个基于 Node 平台的 web 应用开发框架,它提供了一系列强大的特性,帮助你创建各种 web 应用
```

#####  `Express`下载



```bash
npm install express
```

+ 框架特性

  1. 提供了方便简介的路由定义方式
  2.  对获取 `HTTP `请求参数进行了简化处理
  3.  对模板引擎支持高,方便渲染动态 `HTML` 页面
  4.  提供了中间件机制有效控制 `HTTP` 请求
  5.  拥有大量第三方中间件对功能进行扩展  

+ 使用`express`

  ```javascript
  // 引入 express 框架
  const express = require('express');
  // 创建服务 
  const app = express();
  // 监听端口
  app.listen(3031);
  
  ```

  + `send`方法
    1. `send` 方法内部会检测响应内容的类型
    2. `send` 方法会自动设置 `http` 状态码
    3. `send ` 方法会帮我们自动设置响应的内容类型以及编码

##### 中间件



```javascript
中间件就是一堆方法,可以接受客户端发来的请求，可以对请求做出响应,也可以将请求继续交给下一个中间件继续处理。
```

```javascript
app.use('/index',(req,res,next)=>{
    // 调用 index 走该中间件
    next();
})
```

1. `app.use`匹配所有的请求方式,可以直接传入请求处理函数，代表接受所有的请求

   ```javascript
   app.use((req,res,next)=>{
       console.log(req.url);
       next();
   })
   ```

2.  `app.use`第一个参数也可以传入地址，代表不论什么请求方式,只要是这个请求地址就接受这个请求

   ```javascript
   app.use('/index',(req,res,next)=>{
       console.log(req.url);
       next();
   })
   ```



#####  中间件的应用

1.  路由保护，客户端在访问需要登录的页面时，可以先使用中间件判断用户登录状态,用户如果未登录,直接响应,禁止用户进入需要登录的页面

   ```javascript
   
   // 中间件
   app.use("/admin", (req, res, next) => {
     // 用户没有登录
     let isLogin = true;
     if (isLogin) {
       // true 就是登录 如果登录继续向下执行
       next();
     } else {
       // 如果用户没有登陆.直接对客户端做出响应
       res.send("请登录·········");
     }
   
     app.get("/admin", (req, res) => {
       res.end("你已登陆·····");
     });
   });
   ```

   

2.  网站维护公告,在所有路由的最上面定义接收所有请求的中间件，直接为客户端做出响应，网站正在维护中

3.  自定义`404页面`

   ```javascript
   app.use((req, res, next) => {
     res.status(404).send("当前访问页面不存在");
   });
   ```

   

 #####  错误处理中间件

> 在程序执行的过程中,不可避免的会出现一些无法预料的错误,比如文件读取失败,数据库连接失败,错误处理中间件是一个集中处理错误的地方

+ 基本使用

  ```javascript
  
  app.get("/list", (req, res) => {
    // 抛出异常
    throw new Error("程序发生了未知错误");
   // res.end("程序正常执行");
  });
  // 错误处理中间件
  app.use((err, req, res, next) => {
    res.status(500).send(err.message);
  });
  ```



#####  捕获错误

```javascript
try catch 可以捕获异步函数以及其他同步代码在执行过程中发生的错误,但是不能其他类型的 API 发生的错误。
```

#####  Express 请求处理

+ 构建模块化路由

  ```javascript
  /*******************************/
  // 路由
  index.js:
      // 创建路由对象
      const index = express.Router();
      // 为路由对象匹配请求路径
      app.use("/index", index);
      // 创建二级路由
      index.get("/home", (req, res) => {
        res.send("Blog home Index");
      });
      module.exports = index;
  /*******************************/
  app.js:
  	const index = require('path/index.js');
  	// index/home: Blog home Index
  	app.use('/home',index);
  /*******************************/
  ```

  

#####  GET请求参数处理

> `Express` 框架中使用 `req.query`即可获取 `GET`参数,框架内部会将 `GET`请求参数转换为对象并返回

```javascript
app.get('/index',(req,res)=>{
    res.send(req.url);
  console.log(req.query); // { name: 'zhangsan', age: '10' }
});
```



##### POST 请求参数处理

> 第三方模块: `npm install body-parser`

```javascript
// 引入第三方模块
const bodyParser = require("body-parser");
// 配置
app.use(bodyParser.urlencoded({ extended: false }));

app.post("/index", (req, res) => {
  res.send(req.url);
  console.log(req.body); // [Object: null prototype] { username: 'qw', pwd: 'sa' }
});
```

```javascript
// 解释
app.use(bodyParser.urlencoded({ extended: false }));

// 拦截所有请求参数
extended: false 方法内部使用 querystring 模块处理请求参数的格式
extended: true 方法内部使用第三方模块 qs 处理请求参数的格式

```



##### Express 路由参数

```javascript
app.get("/index/:id", (req, res) => {
  console.log(req.params); 
});
```



#####  Express 静态资源处理

+ 静态资源

  ```javascript
  通过 Express 内置的 express.static 可以方便地托管静态文件,例如 img,css,javascript 文件等。
  ```

  ```javascript
  const pathname = path.join(__dirname, "public");
  // 实现静态资源访问功能
  app.use(express.static(pathname));
  
  // 访问: http://127.0.0.1:3031/[default.html]
  ```

  

#####  模板引擎

1. 模板引擎

   ```javascript
   为了使 `art-template`模板引擎能够更好的和`Express`框架结合,模板引擎官方在原 `art-template` 模板引擎的基础上封装了`express-art-template`
   ```

2.  下载

   ```bash
   npm install art-template express-art-template 
   ```

3.  使用

   ```javascript
   //*********************************
   // 模板引擎的使用
   //*********************************
   
   const express = require("express");
   const app = express();
   const path = require("path");
   
   // 1. 告诉 express 框架使用什么模板引擎渲染什么后缀的模板文件
   app.engine("art", require("express-art-template"));
   // 2. 告诉 express 框架模板存放的位置
   app.set("views", path.join(__dirname, "views"));
   // 3. 告诉 express 框架模板的默认后缀是什么
   app.set("view engine", "art");
   
   // 创建一个路由
   app.get("/index", (req, res) => {
     res.render("index", {
       msg: "message",
     });
   });
   
   app.listen(3031, () => {
     console.log("服务器启动成功··················");
   });
   
   ```

   

###  Node 深入补充



####  系统模块



##### 读取目录树

+ `R`

  {% folding  文件读取 %}
  
  ```javascript
  // 同步读取文件
  let dirs = fs.readdirSync("./");
  console.log(dirs); // 需要捕获异常
  
  -------------------------- 改进 ------------------------------------
  
  //捕获同步执行异常 
  try {
    // 可能出现错误的代码
    let dirtree = fs.readdirSync("./");
    console.log(dirtree);
  } catch (err) {
    // 错误后执行的代码
    console.log("执行出错,请仔细阅读错误信息: ", err);
  }
  ------------------------------------------------------------------
  
  // 异步读取
  fs.readdir("./", (err, data) => {
    // 错误的回调函数优先,在回调函数中第一个参数表示错误对象 默认为 null 如果出现错误 err 就是错误对象
    if (err) {
      console.log("请重新尝试: ", err);
    } else {
      console.log(data);
    }
});
  ```
  
  {% endfolding %}
  
  

#####  创建目录

+ `C`

  ```javascript
  // 创建文件夹
  fs.mkdir("../qf-Node-day02", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("文件夹创建成功");
    }
  });
  ```



#####  更改

+ `U`

  ```javascript
  // 更改文件夹
  fs.rename("../qf-Node-day03", "../qf-Node-day02", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("重命名成功");
    }
  });
  
  ```



#####  删除

+ `D`

  ```javascript
  // 删除文件夹 只能删除空文件夹
  fs.rmdir("../qf-Node-day02", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("文件夹删除成功");
    }
  });
  
  ```



#####  文件读写删除

+ 读写

  ```javascript
  // 文件写入
  fs.writeFile("./writeJs.js", "// Node JS written successfully", (err) => {
    if (err) {
      console.log(err);
    } else {
      fs.readFile("./writeJs.js", (err, data) => {
        if (err) {
          console.log(err);
        } else {
          console.log(data.toString('utf8'));
        }
      });
    }
  });
  ```

+ 删除文件

  ```javascript
  fs.unlink("./writeJs.js", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("文件已删除");
    }
  });
  
  ```



#####  URL

+ `url`

  ```bash
  统一资源定位符
  ```

+ 图解

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/url.png">

+ `url.parse`

  {% folding url.parse %}

  ```javascript
  
  const url = require('url');
  let urlpath = 'https://www.bilibili.com/video/BV13E411y7G4?p=7&spm_id_from=pageDriver';
  let urlparse = url.parse(urlpath);
  
  console.log(urlparse);
  /*
  Url {
    protocol: 'https:',
    slashes: true,
    auth: null,
    host: 'www.bilibili.com',    
    port: null,
    hostname: 'www.bilibili.com',
    hash: null,
    search: '?p=7&spm_id_from=pageDriver',
    query: 'p=7&spm_id_from=pageDriver',
    pathname: '/video/BV13E411y7G4',
    path: '/video/BV13E411y7G4?p=7&spm_id_from=pageDriver',
    href: 'https://www.bilibili.com/video/BV13E411y7G4?p=7&spm_id_from=pageDriver'
  }
  */
  ```

  {% endfolding %}

  + 将对象转换为字符串

    ```javascript
    // 将对象转换为字符串
    let strurl = url.format(urlparse);
    console.log(strurl); //  https://www.bilibili.com/video/BV13E411y7G4?p=7&spm_id_from=pageDriver
    
    ```

  + 获取`url`参数

    ```javascript
    // 获取对象参数的值
    let params = url.parse(urlpath, true).query;
    console.log(params);
    
    ```

+ `quertstring`

  ```javascript
  
  const qs = require("querystring");
  
  // 基本使用
  let str = "p=7&spm_id_from=pageDriver";
  console.log(qs.parse(str)); // [Object: null prototype] { p: '7', spm_id_from: 'pageDriver' }
  
  -------------------------------------------------------------------------------------------------
  
      // 添加参数
  let newStr = "p*7#spm_id_from*pageDriver";
  // * # 为 query 的显示方式,而使用该方式进行解析
  let obj = qs.parse(newStr, "#", "*");
  console.log(obj); // [Object: null prototype] { p: '7', spm_id_from: 'pageDriver' }
  
  ```

+ `stringfy`

  ```javascript
  // stringfy
  let jsonS = { p: "7", spm_id_from: "pageDriver" };
  var jsonStr = qs.stringify(jsonS);
  console.log(jsonStr); // p=7&spm_id_from=pageDriver
  ```

  

+ `nodemailer`

  {% hideBlock 请勿尝-了解知识 %}

  ```javascript
  // npm install nodemailer
  "use strict";
  const nodemailer = require("nodemailer");
  
  // 创建发送邮件对象
  let transporter = nodemailer.createTransport({
    host: "smtp.qq.com", // 发送方邮箱类型: QQ 网易 ···
    port: 465,
    secure: true, //  true for 465, false for other ports
    auth: {
      user: 'xxx@qq.com', // 发送方邮箱地址
      pass: '', // smtp 验证码
    },
  });
  
  // 邮件信息
  let mailobj = {
    from: "<xxx@qq.com>", // 邮件发送地址
    to: "xxx@qq.com",
    subject: "Node 发送邮箱测试", // 标题
    text: "发送成功 Node Message", // text 和 html 选其一作为发送文本
    html: "<h1> 发送成功 Node Message </h1>",
  };
  
  // 发送邮件
  transporter.sendMail(mailobj,(err,data)=>{
      if(err){
          console.log(err);
      }else{
          console.log(date);
      }
  });
  ```

  {% endhideBlock %}



####  Express 路由

+ 路由下载

  ```bash
  npm install router
  ```

  

+ 拆解路由

  {% folding 路由 %}
  
  ```javascript
  
  router: /userRouter
  		userRouter:
  			const express = require("express");
  			const router = express.Router();
  			// user api 
   			router.get('/login',(req,res)=>{
                  res.send({
                      code: 1,
                      ps: 'login ok'
                  });
              });
   		module.exports = router;
  
  
  -------------------------------------------------------------------------    
      
  app.js:
  	const express = require("express");
  	const app = express();
  	// 引入拆分路由
  	const userRouter = require('./router/userRouter');
  	// 使用路由
  	app.use('/user',userRouter);
  	
  解析:
  	app.use('/user',userRouter);
  
  	http:127.0.0.1:3031/user/【截取: 进入 userRouter 中寻找请求路由地址 eg: /login ]
  
  	所以最终请求地址为: 	http:127.0.0.1:3031/user/login
  ```
  
  {% endfolding %}




####  模板引擎

##### 模板引擎下载

```bash
npm install art-template --save 
```

#####  使用模板引擎

```javascript
const template = require("art-template");
const fs = require("fs");
// 读取 art.html 字符串模板
fs.readFile("./public/art.html", (err, data) => {
  if (err) {
    return console.log("读取失败");
  } else {
    // 渲染模板引擎
    let templateRes = template.render(data.toString(),{
        name: "李四"
    });
    console.log(templateRes);
  }
});

```





#### 包说明文件

+ `package.json`

  ```bash
  npm init -y
  
  npm install package-name --save
  --save: 可以将包添加到 package.json 中的 dependencies 选项中
  注意: 建议每个项目都有 package.json 文件
  
  ```

  

####  NPM

+ `npm`官网

  <a href="https://www.npmjs.com/">点击前往 npm 官网 </a>

+ `npm`命令行管理工具

  ```bash
  npm install package-name --save
  ```

+ `npm`升级

  ```bash
  npm install --global npm
  ```

  

####  Express

#####  下载

```bash
npm install express
```

#####  使用 

```javascript
const express = require('express');
const app = express();
app.listen('端口号','回调函数');
```

#####   静态资源文件路径开放问题

+ `express`中静态资源路径处理

  ```javascript
  // 开放静态资源路径 访问方式: 127.0.0.1:3031/public/file-name
  app.use("/public", express.static("./public/"));
  
  // 当省略第一个参数的时候可以省略 /public 的方式访问 访问方式: 127.0.0.1:3031/file-name
  app.use(express.static("./public/")); 
  
  // 疑惑: path.join() 暂时理解有误 拼接使用错误
  let filepath = path.join(__dirname,"public")
  
  
  ```

  <img src="https://img-blog.csdnimg.cn/20210228132814369.gif" title="express-开放静态资源路径" width="700">



####  GET请求参数处理案例

+ `app.js`

  {% folding app.js %}

  ```javascript
  const fs = require("fs");
  const url = require("url");
  const template = require("art-template");
  // 创建 express 服务器
  const express = require("express");
  const app = express();
  
  // 开放静态资源路径 访问方式: 127.0.0.1:3031/public/file-name
  // app.use("/public", express.static("./public/"));
  
  // 当省略第一个参数的时候 可以省略 /public 的方式访问
  app.use(express.static("./public/")); // 127.0.0.1:3031/file-name
  
  
  // index router
  app.get("/index", (req, res) => {
    // 读取文件
    fs.readFile("public/index.html", (err, data) => {
      if (err) {
        console.log(err);
      } else {
        let resoult = template.render(data.toString());
        res.send(resoult);
      }
    });
  });
  
  /* ************************************* */
  let comments = [];
  /* ************************************* */
  
  app.get("/pinglun", (req, res) => {
    // 读取 pinglun.html
    fs.readFile("public/pinglun.html", (err, data) => {
      if (err) {
        console.log("文件读取失败");
      } else {
        // 解析 get 参数数据
        let parserObj = url.parse(req.url, true);
        let pathname = parserObj.pathname; //  /pinglun
        console.log(pathname);
        let comment = parserObj.query; // ? 后面的数据 { username: 'asd', message: 'dsadad' }
        // 追加到数组中 服务器端这个时候已经把数据存储好了 接下来就是让用户重新请求 / 首页
        comments.unshift(comment);
  
        // 重定向问题
        // 如何通过服务器让客户端重定向
        // 1. 状态码设置为 302 临时重定向
        // statusCode
        // 2. 在响应头中通过 Location 告诉客户端往哪儿重定向
        // setHeader
        // res.statusCode = 302;
        // res.setHeader("Location", "/");
        // res.send();
        // 模板字符串
        for (let i = 0; i < comments.length; i++) {
          let templateP = template.render(data.toString(), {
            username: comments[i]["username"],
            message: comments[i]["message"],
          });
          res.send(templateP);
        }
      }
    });
  });
  
  // 监听端口号
  app.listen(3031, () => {
    console.log("服务器启动成功··········");
  });
  
  // 缺点: 未能对 get 表单参数进行截取 只能读取一条数据
  
  ```

  {% endfolding %}

+ 实现效果

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/NodeGetData.gif" width="800" title="GET 表单数据处理">

+ 完善`BUG`

  ```javascript
  问题原因: 在模板字符串渲染参数给中对第二个参数传递时理解有误
  
  解决方案；
       let templateP = template.render(data.toString(), {
           // comments --> 参数名称 comments--> 数组 而这个数组包含对象 [{},···]
           comments: comments,
            });
            res.send(templateP);
  
  // 模板字符串
   {{each comments}}
            <tr>
              <td>2021-02-28</td>
              <td>{{$value.username}}</td>
              <td>{{$value.message}}</td>
            </tr>
   {{/each}}
              
  // 缺陷: 未添加重定向
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/fixBug.gif" title="修复第一次由于参数传递错误引起的bug" width="800"> 



+ 个人案例源码参考

  <a href="https://github.com/lovobin/Bin-HTML5/tree/main/Node/node-day10">  点击前往 查看 



####  模板引擎

#####  下载模板引擎

```bash
// 一次性下载多个包
npm i art-template express-art-template -S

// 单独下载
npm install art-template --save
npm install express-art-template --save

```

#####  配置`art-template`

```javascript
// 配置使用 art-template art-->: 可以修改为支持语法高亮的后缀文件 比如: html 
app.engine('art',require('express-art-template'))

第一个参数: 表示 当渲染以 .art 结尾的文件的时候,使用 art-template 模板引擎

express-art-template 是专门用来在 Express 中把 art-template 整合到 Express 中

必须下载 art-template 原因就在于 express-art-template 依赖了 art-template 

```

#####  使用`art-template`

```javascript
Express 为 Response 响应对象提供了一个方法: render

render 方法默认是不可以使用的,但是如果配置了模板引擎就可以使用了

// html 模板名必须和上面一致的后缀 统一放在 views 目录中 ,views 中有目录就需要根据目录依次书写文件路径 默认 views/
res.render('html模板名',{模板数据});

第一个参数不能写路径,默认会去项目中的 views 目录中查找该模板文件

注意: 在Express中: 开发人员把所有的试图文件都放到 views 目录中

```

<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/expressarttemplate.png" width="800">

#####  配置`views`目录

```javascript
app.set('views',render函数的默认路径); // 第一个参数必须是 views 
```



####  POST 表单数据处理

+ `app.js`

  {% folding app.js %}

  ```javascript
  // 引入 express 框架
  const express = require("express");
  // 创建服务
  const app = express();
  
  // 配置解析 post 表单的中间件
  const bodyparser = require("body-parser");
  app.use(bodyparser.urlencoded({ extended: false }));
  
  // 路由
  let userRouter = require("./router/userRouter");
  app.use("/user", userRouter); // 127.0.0.1:3031/user/login  通过 user 再进入 userRouter 下寻找对应路由
  
  // 开放静态资源 添加public 的化显示更加直观
  app.use("/public/", express.static("./public/"));
  // 省略 public 则对 url 显示更加简介简洁
  
  // 使用 express-art-template 模板引擎 app.engine('以什么后缀的文件',)
  app.engine("html", require("express-art-template"));
  
  // 监听端口号
  app.listen(3031, () => {
    console.log("Express 服务器启动成功");
  });
  ```

  {% endfolding %}

+ 路由

  ```javascript
  const express = require("express");
  const router = express.Router();
  
  let comments = [];
  
  router.get("/index", (req, res) => {
    res.render("index.html");
  });
  
  router.post("/pinglun", (req, res) => {
    // 通过 req.body 获取post 表单请求数据
    let comment = req.body;
    comments.unshift(comment);
    res.render("pinglun.html", { comments: comments });
  });
  module.exports = router;
  
  ```

+ 字符串转换为对象

  ```javascript
  // 文件中读取的数据一定是字符串
  // 需要手动转换为 对象
  JSON.parse(data).对象名
  ```

  

####  设计路由

| 请求方法 |      请求路径      | get参数 |            post 参数             |       备注       |
| :------: | :----------------: | :-----: | :------------------------------: | :--------------: |
|  `GET`   |    `/students`     |         |                                  |     渲染首页     |
|  `GET`   |  `/students/new`   |         |                                  |  渲染添加学生页  |
|  `POST`  |  `/students/new`   |         |   `name，age，gender，hobbies`   | 处理添加学生请求 |
|  `GET`   |  `/students/edit`  |  `id`   |                                  |   渲染编辑页面   |
|  `POST`  |  `/students/edit`  |         | `id，name，age，gender，hobbies` |   处理编辑请求   |
|  `GET`   | `/students/delete` |  `id`   |                                  |   处理删除请求   |

#####  路由:` 127.0.0.1:3031/students`

<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/routerStudents.png" width="600">

+ 路由规则

  {% folding 路由规则 %}

  ```javascript
  // 二级路由
  
  -------------------- 封装独立模块 stident --------------------
  
  exports.find = (callback) => {
    // 如果要获取一个函数中异步操作的结果 则必须通过回调函数来获取
    fs.readFile(dbpath,'utf8', (err, data) => {
      if (err) {
        return callback(err);
      } else {
        console.log(typeof JSON.parse(data).students);
        // callback 中的参数: 第一个是: 错误对象 第二个是: 数据
        callback(null, JSON.parse(data).students);
      }
    });
  };
  
  
  -------------------------------------------
      
  studentsRouter:
  		
      // 渲染首页
      router.get("/", (req, res) => {
        // 使用封装函数 find()
        Student.find((err, students) => {
          if (err) {
            return res.status(500).send("文件读取失败");
          } else {
            res.render("index.html", {
              students: students,
            });
          }
        });
      });
  ```

  {% endfolding %}

+ 模板字符串

  {% folding 模板字符串 %}
  
  ```javascript
   <div class="container">
        <!-- 超链接 a 进行页面跳转 href=[/students/new]  实现第二个路由 -->
        <p>
          <a href="/students/new" class="btn btn-info">添加学生</a>
        </p>
  
        <table class="table table-bordered">
          <thead>
            <th>ID</th>
            <th>姓名</th>
            <th>年龄</th>
            <th>性别</th>
            <th>爱好</th>
          </thead>
          <tbody>
            {{each students}}
            <tr>
              <td>{{ $value.id }}</td>
              <td>{{ $value.name }}</td>
              <td>{{ $value.gender }}</td>
              <td>{{ $value.age }}</td>
              <td>{{ $value.hobbies }}</td>
            </tr>
            {{/each}}
          </tbody>
        </table>
      </div>
```
  
  {% endfolding %}
  
  

#####  路由: `http://127.0.0.1:3031/students/new`用于学生信息添加

+ 渲染效果

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/addstudent.png">

+ 路由规则

  ```javascript
  // 添加按钮点击跳转: get: 127.0.0.1:3031/students/new 渲染添加学生页
  router.get("/new", (req, res) => {
    res.render("new.html");
  });
  
  ```

+ 模板字符串

  ```html
  <div class="container">
        <h2 class="sub-header">添加学生信息</h2>
        <!-- 第三个路由参数处理： post: /students/new -->
        <form action="/students/new" method="post">
          <div class="form-group">
            <label for="exampleInputEmail"> 姓名 </label>
            <input
              type="text"
              class="form-control"
              id="exampleInputEmail"
              name="name"
            />
          </div>
  
          <div class="form-group">
            <label for=""> 性别 </label>
            <div>
              <label class="radio-inline">
                <input type="radio" name="gender" id="inlineRadio1" value="0" />男
              </label>
              <label class="radio-inline">
                <input type="radio" name="gender" id="inlineRadio2" value="1" />女
              </label>
            </div>
          </div>
  
          <div class="form-group">
            <label for="age">年龄</label>
            <input class="form-control" type="number" id="age" name="age" />
          </div>
          <div class="checkout">
            <label> 爱好 </label>
            <input class="form-control" type="text" name="hobbies" />
          </div>
          <div class="btn">
            <button type="submit" class="btn btn-info"> 添加学员信息 </button>
          </div>
        </form>
      </div>
  ```

+ 异步函数`save`封装

  ```javascript
  
  exports.save = (student, callback) => {
    fs.readFile(dbpath, "utf8", (err, data) => {
      if (err) {
        return callback(err);
      } else {
        let students = JSON.parse(data).students;
        // 处理 id: 获取数组的最后一个 再加 1
        student.id = students[students.length - 1].id + 1;
        // 添加数据
        students.push(student);
        // 把对象数据转换为字符串
        let result = JSON.stringify({ students: students });
        // 把字符串保存到文件中
        fs.writeFile(dbpath, result, (err) => {
          if (err) {
            // 错误 就返回错误对象
            return callback(err);
          } else {
            // 成功就不报错 返回空对象
            callback(null);
          }
        });
      }
    });
  };
  
  ```



#####  路由:`post: 127.0.0.1；3031/students/new`

+ 路由规则

  ```javascript
  // 处理添加学生请求 post: 127.0.0.1:3031/students/new
  router.post("/new", (req, res) => {
    // 1. 获取表单数据 post: body-parser
    let formdata = req.body;
    // 2, 处理  将数据保存到 db.json 文件中
    // 预处理: 由于文件都是字符串非对象 所以只能先行读取 在追加 追加结束后再对文件进行写入操作
    // 具体操作: 1. 先读取出来 转成对象 2. 然后往对象中 push 数据 3. 然后把对象转换为 字符串 然后把字符串再次写入文件
    // 3. 发送响应 res.body
    Student.save(formdata, (err) => {
      if (err) {
        return res.status(500).send("{'error': 'not found'}");
      } else {
        res.redirect("/students");
      }
    });
  });
  
  ```

+ 效果预览

  ![Node](https://img-blog.csdnimg.cn/20210303154910327.gif#pic_center)



#####   `json`数据

```json
{
  "students": [
    { "id": 1, "name": "张三", "gender": 0, "age": 10, "hobbies": "打游戏" },
    { "id": 2, "name": "张三", "gender": 0, "age": 10, "hobbies": "打游戏" },
    { "id": 3, "name": "张三", "gender": 0, "age": 10, "hobbies": "打游戏" },
    { "id": 4, "name": "张三", "gender": 0, "age": 10, "hobbies": "打游戏" },
    { "id": 5, "name": "张三", "gender": 0, "age": 10, "hobbies": "打游戏" },
    { "id": 6, "name": "张三", "gender": 0, "age": 10, "hobbies": "打游戏" },
    { "id": 7, "name": "张三", "gender": 0, "age": 10, "hobbies": "打游戏" }
  ]
}

```

