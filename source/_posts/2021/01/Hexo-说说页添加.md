---
title: Hexo 说说页添加
tags:
  - Hexo
  - Butterfly
categories: Butterfly
abbrlink: 37885
date: 2021-01-01 16:19:12
---



###  主题升级

+ `Butterfly` 主题更新了

+ 升级步骤

  ```bash
  进入主题目录下:
  	# 查看下仓库 我的仓库信息将会是 jerry 的 buffterfly
  	
  	git remote -v 
  ```

+ 仓库信息

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210101165527.png">

+ 执行升级

  ```bash
  git pull 
  ```

+ 主题版本号

  ```bsh
  tag: 3.5.1
  ```

###  Hexo 说说页添加

+ 效果预览

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/shuoshuo.png">

###  Artitalk 具体实现

+ 引用

  > <a href="https://artitalk.js.org/doc.html#%F0%9F%8C%88-leancloud-%E7%9A%84%E7%9B%B8%E5%85%B3%E5%87%86%E5%A4%87"> Artitalk.js](https://artitalk.js.org/)
  >
  > </a>

###  步骤剖析

```bash
1. 前往 LeanCloud 国际版，注册账号。

国际版: https://console.leancloud.app/#/apps(英文页面)

使用国际版的理由: 因为国际版的 LeanCloud 不需要配置 serverurl，所以推荐使用国际版，速度没有区别，如果使用国内版的 LeanCloud 别忘了填写 

serverurl 即可
```

- 右上角显示`国际版`

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210101163320.png">

```bash
2. 注册完成之后根据 LeanCloud 的提示绑定手机号和邮箱。
```

+ 不弹出添加方法

  {% tabs card-1 %}

  <!-- tab 配置手机号 -->

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210101163822.png">

  <!-- endtab -->

  <!-- tab 配置邮箱 -->

  该页面左侧导航栏

  <!-- endtab -->

  {% endtabs %}

  

```bash
3. 绑定完成之后点击创建应用，应用名称随意，接着在结构化数据中创建 class，命名为 shuoshuo

注意: shuoshuo  [改名字很重要 也可以不是 shuoshuo 进行自定义名称]

```

```bash
4. 在你新建的应用中找到结构化数据下的用户。点击添加用户，输入想用的用户名及密码。
```

```bash

5. 回到结构化数据中，点击 class 下的 shuoshuo。找到权限，在 Class 访问权限中将 add_fields 以及 create 权限设置为指定

用户，输入你刚才输入的用户名会自动匹配。为了安全起见，将 delete 和 update 也设置为跟它们一样的权限。

注意: 注意权限第五步,就按照上述规定执行即可
```

```bash
6. 然后新建一个名为atComment的class，权限什么的使用默认的即可。
```

```bash

7. 点击 class 下的 _User 添加列，列名称为 img，默认值填上你这个账号想要用的发布说说的头像url，这一项不进行配置，说说头像

会显示为默认头像 —— Artitalk 的 logo。

```

```bash
8. 在最菜单栏中找到设置-> 应用 keys，记下来 AppID 和 AppKey ，一会会用。
```

```bash
9. 最后将 _User 中的权限全部调为指定用户，或者数据创建者，为了保证不被篡改用户数据已达到强制发布说说。

注意: 指定用户名与密码谨记,因为发布需要
```

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210101164559.png">



###  Hexo Buffterfly的`_config.yml` 搜索 [`artitalk`]

```bash
添加：
	appID: 
	appKey: 
```

###  新建页面 `根据shuoshuo`这个类同名【自定义就是用自定义类名  必须同名】

###  Typora 下的添加信息

+ yml

  ```yml
  ---
  title: shuoshuo
  type:  shuoshuo
  noDate: 'true'
  comments: 'false'
  img: https://cdn.jsdelivr.net/gh/cungudafa/img/images/food.jpg
  ---
  ```

+ 标题栏下

  ```javascript
  
  {% raw %}
  <!-- 引用 artitalk -->
  <script type="text/javascript" src="https://unpkg.com/artitalk"></script>
  <!-- 存放说说的容器 -->
  <div id="artitalk_main"></div>
  <script>
  new Artitalk({
      appId: '', // Your LeanCloud appId
      appKey: '' // Your LeanCloud appKey
  })
  </script>
  {% endraw %}
  ```

###  说说美化(等待中)