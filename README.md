###  Hexo-Buffterfly依赖下载

+ `githubcalendar`

  ```bash
  npm i hexo-githubcalendar --save
  # 配置项:
  githubcalendar:
    enable: true
    enable_page: /
    user: lovobin
    layout:
      type: id
      name: recent-posts
      index: 0
    githubcalendar_html: '<div class="recent-post-item" style="width:100%;height:auto;padding:10px;"><div id="github_loading" style="width:10%;height:100%;margin:0 auto;display: block"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"  viewBox="0 0 50 50" style="enable-background:new 0 0 50 50" xml:space="preserve"><path fill="#d0d0d0" d="M25.251,6.461c-10.318,0-18.683,8.365-18.683,18.683h4.068c0-8.071,6.543-14.615,14.615-14.615V6.461z" transform="rotate(275.098 25 25)"><animateTransform attributeType="xml" attributeName="transform" type="rotate" from="0 25 25" to="360 25 25" dur="0.6s" repeatCount="indefinite"></animateTransform></path></svg></div><div id="github_container"></div></div>'
    pc_minheight: 280px
    mobile_minheight: 0px
    color: "['#ebedf0', '#fdcdec', '#fc9bd9', '#fa6ac5', '#f838b2', '#f5089f', '#c4067e', '#92055e', '#540336', '#48022f', '#30021f']"
    api: https://python-github-calendar-api.vercel.app/api
    # api: https://python-gitee-calendar-api.vercel.app/api
    calendar_js: https://cdn.jsdelivr.net/gh/Zfour/hexo-github-calendar@1.21/hexo_githubcalendar.js
    plus_style: ""
    
  ```

+ 浏览器同步刷新插件

  ```bash
  npm install hexo-browsersync --save
  ```

+ 搜索插件

  ```bash
  npm install hexo-generator-search --save
  # 根: 配置项
  search:
    path: search.xml
    field: post
  
  ```

+ 文章加密插件

  ```bash
  npm install --save hexo-blog-encrypt
  
  # 需要加密的文章添加配置项
  ---
  title: Hello World
  tags:
  - 作为日记加密
  date: 2016-03-30 21:12:21
  password: mikemessi
  abstract: 有东西被加密了, 请输入密码查看.
  message: 您好, 这里需要密码.
  wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
  wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
  ---
  
  # 主题配置项
  # Security
  encrypt: # hexo-blog-encrypt
    abstract: 有东西被加密了, 请输入密码查看.
    message: 您好, 这里需要密码.
    tags:
    - {name: tagName, password: 密码A}
    - {name: tagName, password: 密码B}
    wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
    wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
  
  ```

+ `gulp`下载

  

