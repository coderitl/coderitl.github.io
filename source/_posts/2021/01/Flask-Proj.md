---
title: Flask-Proj
tags:
  - Python
  - Linux
categories: Flask
abbrlink: 62242
date: 2021-01-22 13:10:06
top_img:
---

###  Flask-Proj

####  虚拟环境及包的安装

+ 创建虚拟环境

+ 下载`Flask`

  ```bash
  pip install flask=='版本号' / pip install flask(自行选择版本号)
  ```

+ `Flask-Proj`开发

+ `requirements`文件

  ```bash
  Python 项目中必须包含一个 requirements.txt 文件 ,用于记录所有依赖包及其精确的版本号,以便在新环境中进行部署操作
  ```

+ 在虚拟环境中使用以下命令将当前虚拟环境中的依赖包以版本号生成至文件中

  ```bash
  pip freeze > requirements.txt
  ```

+ 当需要创建这个虚拟环境的完全副本,可以创建一个新的虚拟环境,并执行以下命令

  ```bash
  pip install -r requirements.txt
  ```



###  项目(Flask_Proj)

####  运行测试

+ 运行

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/proj.png">

+ 配置字符集

  ```bash
  
  app.py:
  	# 配置字符集
  	# -*- coding:utf-8 -*-
  ```


+ 端口号修改

  ```python
  app.run(port='端口号')
  ```

+ 配置文件

  ```python
  # 新建 settings.py, 写入以下配置信息
  
  ENV = 'development' # 开发环境
  DEBUG = True # 开启 debug 模式
  
  # 在 app 导入
  import settings
  
  # 在 app 定义下写如下信息
  app.config.from_object(settings)
  
  
  ```

+ 终端启动方式

  ```bash
  python/python3 app.py
  ```

+ 配置信息无效可通过图像化界面开启`DEBUG`

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/debug.png" width="600">

+ 修改后

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/settingsDebug.png" width="600">

####  路由请求方式限定

+ `POSTMAN` 进行测试

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/postman.png">

+ 添加新的请求方式

  ```python
  # 默认支持 GET 请求
  @app.route('/',methods = ['GET','POST'])
  ```

+ 路由的请求与相应

  ```bash
  response 响应:
  	200 - 请求成功
  	404 - 请求的资源(网页等)不存在
  	500 - 内部服务器错误
  	302 - 重定向
  	301 - 资源(网页等)被永久转移到其他 URL
  ```

+ `Flask`路由和变量规则

  ```python
  # 路由 route
  这个装饰器其实就是将 rule 字符串跟视图函数进行了数据绑定,通过 add_url_rule() 实现绑定
  
  # 等效写法
  # ------------------- 装饰器 ------------------------------
      @app.route('/',methods = ['GET','POST'])
      def hello_world():
          return 'Hello World!'
   # -------------------- add_url_rule() -------------------
      def index():
      	return '<h1><font color="red">index Text</font></h1>'
  	app.add_url_rule('/index', view_func = index)
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/add_url_rule.png">

  +  路由的变量规则

    ```bash
    通过把 URL 的一部分标记为 <variable_name> 就可以在 URL 中添加变量。标记的 部分会作为关键字参数传递给函数。通过使用 <converter:variable_name> ，可以 选择性的加上一个转换器，为变量指定规则。
    ```

    ```python
    # 默认 str
    @app.route('/getValue/<key>') # 默认 str 不需要添加数据类型
    def getValue(key):
        return data.get(key)
    
    # int
    
    # int 类型
    @app.route('/add/<int:num>')  # 默认 str 不需要添加数据类型
    def add(num):
        result = num + 10
        return str(result)
    
    ```

  + 转换器类型：

    | `string` | （缺省值） 接受任何不包含斜杠的文本 |
    | -------- | ----------------------------------- |
    | `int`    | 接受正整数                          |
    | `float`  | 接受正浮点数                        |
    | `path`   | 类似 `string` ，但可以包含斜杠      |
    | `uuid`   | 接受 UUID 字符串                    |
  
  +  路由的斜杠问题（唯一的 `URL` 问题）
  
     ```python
     ‘/index/’ 
     
     路由中没有斜杠,浏览器访问会报错
     
     路由中有斜杠,访问时没有则会自动重定向
     ```
  
  + `return`
  
    ```python
    return 后面返回的字符串其实也是做了一个 response 对象的封装。最后的返回结果还是 response 对象。
    ```
  
    

###  Jinja2 模板引擎

####  渲染模板函数

1. `Flask` 提供的 `render_template`函数封装了该模板引擎

2.  `render_template` 函数的第一个参数是模板的文件名,后面的参数都是键值对,表示模板中变量对应的真实值。

   ```python
   # 导入 render_template
   from flask import Flask,render_template
   
   # 使用 render_template
   @app.route('/index', methods = ['GET', 'POST'])
   def index():
       return render_template('index.html')
   ```

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/Jinja2.png" width="600">

3. 变量代码块

   ```jinja2
   {# 注释语法 #}
   {{ value1 }}
   
   {# 通常,模板中使用的变量名和要传递的数据的变量名保持一致。 #}
   
   ```

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/jinjaStr.png" width="600">

4. 控制代码块

   + `for`循环

     ```jinja2
     {% for play in my_list %}
         <h1> {{ play }} </h1>
     {% endfor %}
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/forjinja.png">

   + `if`

     ```jinja2
     {% if num>3 %}
     {{ num} }}
     {% endif %} 
     ```

5.  内建过滤器

   + 含义

     ```jinja2
     过滤器:
     
     	过滤器的本质就是函数,有时候我们不仅仅要输出变量的值,我们还需要改变变量的显示甚至格式化,运算等等，而在模板中是不能直接
     	
     调用 Python 中的某些方法m那么就用到了过滤器。
     
     ```

   + 使用方式

     ```jinja2
     
     变量名 | 过滤器
     
     {{ variable | filter_name(*args) }} 
     
     {# 如果没有任何参数传递给过滤器,则可以省略括号 #}
     
     {{ variable | filter_name }}
     
     {# 链式调用 #}
     
     {{ variable | filter_name1 | filter_name2 | ··· }}
     
     https://www.bilibili.com/video/BV17W41177oE?p=14
     
     ```
   
6. 自定义过滤器

   + 方法一

     ```python
     
     # 自定义过滤器 本质是函数
     def replace_str(value):
         value = value.replace('str', '我被替换了···')
         return value.strip()
     
     
     # 过滤器
     app.add_template_filter(replace_str, 'replace')
     
     
     # 使用过滤器 
     
     <p>原格式: {{ msg }} </p>
     <p> 过滤器: <font color="red">{{ msg|replace }} </font> </p>
         
     ```

   + 方法二(装饰器)

     ```python
     @app.template_filter('listreverse')
     def reverse_filter(li):
         temp_li = list(li)
         li = temp_li.reverse()
         return temp_li
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/filter.png">

###  视图

+ `Flask-Response` 对象

+ `Flask-Resquest` 对象

  ```python
  requests 对象 对象可以访问属性,也可以调用方法
  
  request.args.get('key') --> get 请求
  
  request.form --> post 请求
  ```

###  Web 表单

```jinja2
在 Flask 中,为了处理 web 表单,我们一般使用 Flask-WTF 扩展,它封装了 WTForms,并且它有验证表单数据的功能。
```

+ 表单验证

  ```python
  
  @app.route('/reigster', methods = ['GET', 'POST'])
  def reigster():
      # 获取请求方式
      if request.method == 'POST':
          # 获取请求参数
          username = request.form.get('username')  # 获取表单提交的用户名
          password = request.form.get('password')  # 获取表单提交的密码
          repassword = request.form.get('repassword')  # 获取表单提交的密码
          print(''' 
              用户名: {}
              密码: {}
              重复输入: {}
              '''.format(username, password, repassword))
          # 判断参数是否填写 & 密码是否相同
          if not all([username, password, repassword]):
              print('参数不完整')
              flash(u'参数不完整')
          # 判断密码是否相同 不相同输入密码不一致
          elif password != repassword:
              print('两次输入不一致')
              flash(u'两次输入不一致')
          else:
              return 's'
      return render_template('index.html')
  ```

+ 闪现消息

  ```python
  # 消息闪现秘钥
  app.secret_key = 'flask'
  
  # u 解决编码问题
  flash(u'message-info')
  
  # 遍历 flash-message 
    {% for message in get_flashed_messages() %}
          {{ message }}
    {% endfor %}
  ```

+ 重定向

  ```python
  # redirect 源码 
  def redirect(location, code=302, Response=None):
      """Returns a response object (a WSGI application) that, if called,
      redirects the client to the target location. Supported codes are
      301, 302, 303, 305, 307, and 308. 300 is not supported because
      it's not a real redirect and 304 because it's the answer for a
      request with a request with defined If-Modified-Since headers.
  
      .. versionadded:: 0.6
         The location can now be a unicode string that is encoded using
         the :func:`iri_to_uri` function.
  
      .. versionadded:: 0.10
          The class used for the Response object can now be passed in.
  
      :param location: the location the response should redirect to.
      :param code: the redirect status code. defaults to 302.
      :param class Response: a Response class to use when instantiating a
          response. The default is :class:`werkzeug.wrappers.Response` if
          unspecified.
      """
  
  有两次响应:
      
      1. 302 状态码 + location
      
      2. 返回location 请求地址内容
      
  ```

+ 路径反向解析

  ```python
  endpoint = '代号/小名'
  
  url_for()
  
  # -----------------------------------
  
  @app.route('/index', methods = ['GET', 'POST'], endpoint = 'f')
  def index():
      return render_template('index.html')
  
  
  # 使用 Flask-WTF 实现表单
  @app.route('/flaskWtf')
  def flaskWtf():
      return redirect(url_for('f'))
  
  ```

+ `Flask-WTF`

  + 下载

    ```bash
    pip install flask-wtf
    ```

  + 使用
  
    ```python
    # 表单所需
    from flask_wtf import FlaskForm
    from wtforms import StringField, PasswordField, SubmitField
    from wtforms.validators import DataRequired
    
    
    # 定义登录类 
    class LoginForm(FlaskForm):
        username = StringField(u'用户名')
        password = PasswordField(u'密码')
        repassword = PasswordField(u'确认密码')
        submit = SubmitField(u'提交')
    
    @app.route('/login',methods=["GET","POST"])
    def login():
    	login = LoginForm()
        return render_template('index.html',login=login)
        
        
    ```

###  模板: 复用

```python
模板继承 *
include
宏
```

+ 需要模板继承的情况

  ```python
  1. 多个模板具有完全相同的顶部和底部
  
  2. 多个模板具有相同的模板内容,但是内容中部分不一样
  
  3. 多个模板具有完全相同的模板内容
  
  标签:
  
      {% block 名字 %}
  
      {% endblock %}
  
  继承:
      
      {% extends 'html-name.html' %}
  ```

+ 案例

  ```python
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title> {% block title %}base{% endblock %}</title>
      <style>
          {#       #}
          #div1 {
              height: 100px;
              background-color: pink;
              line-height: 100px;
          }
  
          #div1 ul {
              list-style: none;
          }
  
          #div1 ul li {
              float: left;
              padding-right: 20px;
          }
  
          #div2 {
              height: 600px;
              font-size: 60px;
              line-height: 600px;
              text-align: center;
              background-color: skyblue;
          }
  
          #div3 {
              height: 100px;
              line-height: 100px;
              font-size: 20px;
              color: #fff;
              text-align: center;
              background-color: lightseagreen;
          }
      </style>
      {% block mycss %}{% endblock %}
  </head>
  <body>
  <div id="div1">
      <ul>
          <li>首页</li>
          <li>关于</li>
          <li>友情链接</li>
      </ul>
      {#    {% block div1 %}{% endblock %} #}
  
  </div>
  <div id="div2">
      {% block div2 %}
          我是中间部分
          <button> 点击</button>
      {% endblock %}
  </div>
  <div id="div3">
      {% block div3 %}
          版权信息
      {% endblock %}
  </div>
  
  <script>
      var btn = document.querySelector('button');
      btn.onclick = function (){
          alert('点击了···')
      }
  </script>
  {% block myscript %}{% endblock %}
  </body>
  </html>
  ```

+ 模板继承

  ```python
  {# 继承 base.html #}
  {% extends 'base.html' %}
  
  {# 修改title #}
  {% block title %}
      useBase
  {% endblock %}
  
  {# css 预留 #}
  {% block mycss %}
      <style>
          #div2 {
              background-color: deeppink;
          }
      </style>
  {% endblock %}
  
  {# js 事件 #}
  {% block myscript %}
      <script>
          console.log(btn)
      </script>
  {% endblock %}
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/exteds.png">

+ 修改局部内容

  ```python
  
  {# div2 修改内容 #}
  
  {% block div2 %}
      <h1> 修改后的内容 </h1>
  {% endblock %}
  
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/base.png">

+ 外界资源引入方式

  + 方式一(不推荐)

    ```python
    
    {# css 预留 #}
    {% block mycss %}
        <style>
            #div2 {
                background-color: deeppink;
            }
        </style>
        
        {# 普通引入方式 #}
        
        <link rel="stylesheet" href="../static/css/style.css" />
        
    {% endblock %}
    ```

  + 方式二(反向解析)

    ```python
    print(app.url_map)  # 存在该路由规则
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/url_map.png">

    ```python
    
    {# css 预留 #}
    {% block mycss %}
        <style>
            #div2 {
                background-color: deeppink;
            }
        </style>
        {# 反向解析引入 #}
        <link rel="stylesheet" href="{{ url_for('static',filename='css/style.css') }}">
    {% endblock %}
    ```

  + `js`外部资源引入

    ```python
    {# js 事件 #}
    {% block myscript %}
        <script>
            console.log(btn)
        </script>
        
    	{# 反向解析 引入外部js #}
        <script src="{{ url_for('static',filename='js/index.js') }}"></script>
    {% endblock %}
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/jsBase.png">

+ 宏（`macro`）

  + 定义

    ```python
    {# 定义宏 #}
    {% macro fun-name(action,value='默认值'),method='post' %}
        statements
    {% endmacro %}
        
        
    # 定义一个 form 
    {% macro form(action,value='默认值'),method='post' %}
        <p><input type="text" name="username"></p>
        <p><input type="text" name="password"></p>
    {% endmacro %}
    ```

  + 使用

    ```python
       {# 使用宏 #}
       1. 导入
       
           {% import  'maco/maco1.html' as 别名 %}
       
       2. 应用
       	   
           {{ 别名.fun-name('/router',···) }}
           
           
       # 调用 form
        {% import '宏资源路径' as f %}
        {{ f.form('/index',value="注册",method="post") }}
           
    ```

###  Flask-蓝图

+ 拆解

  ```python
  from flask import Flask
  
  # 导入配置文件
  import settings
  
  # 导入蓝图 对象
  from apps.user.view import user_bp
  
  
  def create_app():
      app = Flask(__name__, template_folder = '../templates', static_folder = '../static')  # app 是一个核心对象
      app.config.from_object(settings)  # 加载配置
      # 蓝图
      # 注册蓝图
      app.register_blueprint(user_bp)  # 将蓝图对象绑定到 app 上
      print(app.url_map)
      return app
  
  ```

+ `app.py`

  ```python
  from apps import create_app
  
  
  app = create_app()
  if __name__ == '__main__':
      print(app.url_map)
      app.run(port = 9000)  # 设置端口号最好在启动之前设置
  
  ```


+ `Flask-script`

  + 下载

    ```bash
    pip install flask-script
    ```

  + 使用

    ```python
    from flask_script import Manager
    manager = Manager(app=app)
    
    	manager.run()
    ```

  + 启动方式

    ```python
    python/python3 app.py runserver [-h 0.0.0.0 -p new-port][可选参数]
    ```

###  持久化存储

1. `pymysql`

   ```bash
   pip install pymysql
   ```

2. `Flask-SQLAlchemy`

   ```python
   
   Flask-SQLAlchemy 是一个 Flask 扩展,简化了在 Flask 应用中使用 SQLAlchemy 的操作,SQLAlchemy 是一个强大的关系型数据库
   
   框架,支持多种数据库后台。SQLAlchemy 提供了高层 ORM，也提供了使用数据库原生SQL 的底层功能。
   
   ```

   + 下载

     ```bash
     pip install flask-sqlalchemy # 实现 ORM 映射
     ```

   + 映射相关
   
     ```bash
     pip install flask-migrate # 发布命令的工具
     ```
   
   + 配置数据库连接
   
     ```bash
     # 配置数据库
     # mysql+pymysql://user:password@hostip:port/databasename
     SQLALCHEMY_DATABASE_URI='mysql://root:root@127.0.0.1:3306/student'
     ```
   
     

