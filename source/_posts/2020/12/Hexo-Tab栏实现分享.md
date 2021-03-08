---
title: Hexo-Bufftery-Tab栏实现分享
tags: Hexo
categories: Hexo
abbrlink: 60159
date: 2020-12-20 13:58:51
---

###  Hexo-Bufftery-Tab栏实现分享

> 内容推荐糖果屋教程，写这篇只是为了个人实现

+ 官方文档查看详细信息

  > <a href="https://butterfly.js.org/posts/4aa8abbe/#Tabs">点击进入官方文档 https://butterfly.js.org/posts/4aa8abbe/#Tabs</a>

+ 渲染效果

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/Hexotabs.png" title="Tabs实现">

+ (`主题下`)配置文件添加如下

  ```bash
  
  # tabs
  tabs:
    enable: true
    transition:
      tabs: true
      labels: true
    border_radius: 0
  ```

+ 实现语法剖析(`id很重要不重复类似于主键`)

  ```yml
  语法:
  
  {%  tabs id %}
  # 第一块区域
  
      <!-- tab 文本信息 -->
  
          ** this is Tab1**
  
      <!-- endtab -->
  
  # 第二块区域
  
      <!-- tab -->
  
          ** ww**
  
      <!-- endtab -->
  
  # 第三块区域
      <!-- tab -->
  
          asa
  
      <!-- endtab -->
  
  {% endtabs %}
  ```

+ 分栏实现一

  {%  tabs  tab-1  %}

  <!-- tab -->

  `名称a`下的内容展示

  <!-- endtab -->

  

  <!-- tab 名称-b -->

  `名称b`下的内容展示

  <!-- endtab -->

  

  <!-- tab 名称-c -->

  `名称c`下的内容展示

  <!-- endtab -->

  {% endtabs %}



+ 分栏实现二

  {%  tabs tab-2  %}

  <!-- tab 名称-a -->

  `名称a`下的内容展示ss

  <!-- endtab -->

  

  <!-- tab 名称-b -->

  `名称b`下的内容展示

  <!-- endtab -->

  

  

  <!-- tab 名称-c -->

  `名称c`下的内容展示

  <!-- endtab -->

  {% endtabs %}



###  容器的其他类型：

####  1. 更新`folding`添加

```yml
{% folding 参数（可选）, 标题 %}

![](图片路径)

{% endfolding %}{% folding 参数（可选）, 标题 %}
```

{% folding  cyan,折叠 %}

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/hellowWorld.png" width="500" title="实现容器类需要文件支撑,除了Buffterfly 内置可以直接使用,其他容器在 糖果屋有具体教程可提供方案">

{% endfolding  %}

####  2. 隐藏容器

```yml
在主题文件夹下添加:  hideBlock: true (不添加报错)

{% hideBlock 点击查看,bg,color %}

替换文本 --> 显示后文本

{% endhideBlock %}

```



{% hideBlock 点击查看,bg,color %}

显示后文本

{% endhideBlock %}

####  3. 外挂标签`Tip`

+ `success`

  {% tabs testTip-1 %}

  <!-- tab success -->

  + 效果预览

    <div class='tip success faa-flash animated'><p>success<p></div>

  <!-- endtab -->

  

  <!-- tab markdown实现 -->

  ```html
  <div class='tip success faa-flash animated'><p> 替换文本 <p></div>
  ```

  <!-- endtab -->

  

  {% endtabs %}


  + `error`

    {% tabs error-1 %}

    <!-- tab error -->

    + 效果预览

      <div class='tip error faa-flash animated'><p> 替换文本 <p></div>

    <!-- endtab -->

    <!-- tab markdown实现 -->

    <div class='tip error faa-flash animated'><p> 替换文本 <p></div>

    <!-- endtab -->

    {% endtabs %}

    

  + `warning`

    {% tabs warn-1 %}

    <!-- tab warning -->

    + 效果预览

      <div class='tip warning faa-flash animated'><p> 替换文本 <p></div>

    <!-- endtab -->

    <!-- tab markdown实现 -->

    ```html
    <div class='tip warning faa-flash animated'><p> 替换文本 <p></div>
    ```

    <!-- endtab -->

    

    {% endtabs %}



####  4.  `note`

+ 主题配置中开启`note`

  ```bash
  note:
  	# style 改变如下显示类型  
    # Note tag style values:
    #  - simple    bs-callout old alert style. Default.
    #  - modern    bs-callout new (v2-v3) alert style.
    #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
    #  - disabled  disable all CSS styles import of note tag.
    style: simple
    icons: true
    border_radius: 3
    # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
    # Offset also applied to label tag variables. This option can work with disabled note tag.
    light_bg_offset: 0
  ```

+  类型

  1. {% note info %}  info 提示标签符 {% endnote %}

  2. {% note default %} default 提示标签符 {% endnote %} 
  3. {% note primary no-icon %} primary 提示标签符 {% endnote %} 
  4. {% note success %} success 提示标签符 {% endnote %} 
  5. {% note warning %} warning 提示标签符 {% endnote %}
  6.  {% note danger %} danger 提示标签符 {% endnote %}

+ 各类型语法（`一 一 对应`）

  ```bash
  1. {% note info %}  info 提示标签符 {% endnote %}
  2. {% note default %} default 提示标签符 {% endnote %} 
  3. {% note primary no-icon %} primary 提示标签符 {% endnote %} 
  4. {% note success %} success 提示标签符 {% endnote %} 
  5. {% note warning %} warning 提示标签符 {% endnote %}
  6. {% note danger %} danger 提示标签符 {% endnote %}
  ```

  注意: `note` 的 `style`可以改变如下显示

####  5.  复选列表 checkbox

```
{% checkbox 纯文本测试 %}
{% checkbox checked, 支持简单的 [markdown](https://guides.github.com/features/mastering-markdown/) 语法 %}
{% checkbox red, 支持自定义颜色 %}
{% checkbox green checked, 绿色 + 默认选中 %}
{% checkbox yellow checked, 黄色 + 默认选中 %}
{% checkbox cyan checked, 青色 + 默认选中 %}
{% checkbox blue checked, 蓝色 + 默认选中 %}
{% checkbox plus green checked, 增加 %}
{% checkbox minus yellow checked, 减少 %}
{% checkbox times red checked, 叉 %}
```

{% checkbox 纯文本测试 %}
{% checkbox checked, 支持简单的 [markdown](https://guides.github.com/features/mastering-markdown/) 语法 %}
{% checkbox red, 支持自定义颜色 %}
{% checkbox green checked, 绿色 + 默认选中 %}
{% checkbox yellow checked, 黄色 + 默认选中 %}
{% checkbox cyan checked, 青色 + 默认选中 %}
{% checkbox blue checked, 蓝色 + 默认选中 %}
{% checkbox plus green checked, 增加 %}
{% checkbox minus yellow checked, 减少 %}
{% checkbox times red checked, 叉 %}

####  6.  时间线

```
{% timeline 升级小助手 %}

{% timenode 2020-07-24 [2.6.6 -> 3.0](https://github.com/volantis-x/hexo-theme-volantis/releases) %}

1. 如果有 `hexo-lazyload-image` 插件，需要删除并重新安装最新版本，设置 `lazyload.isSPA: true`。
2. 2.x 版本的 css 和 js 不适用于 3.x 版本，如果使用了 `use_cdn: true` 则需要删除。
3. 2.x 版本的 fancybox 标签在 3.x 版本中被重命名为 gallery 。
4. 2.x 版本的置顶 `top: true` 改为了 `pin: true`，并且同样适用于 `layout: page` 的页面。
5. 如果使用了 `hexo-offline` 插件，建议卸载，3.0 版本默认开启了 pjax 服务。

{% endtimenode %}

{% timenode 2020-05-15 [2.6.3 -> 2.6.6](https://github.com/volantis-x/hexo-theme-volantis/releases/tag/2.6.6) %}

不需要额外处理。

{% endtimenode %}

{% timenode 2020-04-20 [2.6.2 -> 2.6.3](https://github.com/volantis-x/hexo-theme-volantis/releases/tag/2.6.3) %}

1. 全局搜索 `seotitle` 并替换为 `seo_title`。
2. group 组件的索引规则有变，使用 group 组件的文章内，`group: group_name` 对应的组件名必须是 `group_name`。
2. group 组件的列表名优先显示文章的 `short_title` 其次是 `title`。

{% endtimenode %}

{% endtimeline %}
```

{%  timeline 升级小助手  %}

{%  timenode 2020-07-24 [2.6.6 -> 3.0](https://github.com/volantis-x/hexo-theme-volantis/releases)  %}

1. 如果有 `hexo-lazyload-image` 插件，需要删除并重新安装最新版本，设置 `lazyload.isSPA: true`。
2. 2.x 版本的 css 和 js 不适用于 3.x 版本，如果使用了 `use_cdn: true` 则需要删除。
3. 2.x 版本的 fancybox 标签在 3.x 版本中被重命名为 gallery 。
4. 2.x 版本的置顶 `top: true` 改为了 `pin: true`，并且同样适用于 `layout: page` 的页面。
5. 如果使用了 `hexo-offline` 插件，建议卸载，3.0 版本默认开启了 pjax 服务。

{%  endtimenode  %}

{%  timenode 2020-05-15 [2.6.3 -> 2.6.6](https://github.com/volantis-x/hexo-theme-volantis/releases/tag/2.6.6)  %}

不需要额外处理。

{%  endtimenode  %}

{%  timenode 2020-04-20 [2.6.2 -> 2.6.3](https://github.com/volantis-x/hexo-theme-volantis/releases/tag/2.6.3)  %}

1. 全局搜索 `seotitle` 并替换为 `seo_title`。
2. group 组件的索引规则有变，使用 group 组件的文章内，`group: group_name` 对应的组件名必须是 `group_name`。
2. group 组件的列表名优先显示文章的 `short_title` 其次是 `title`。

{%  endtimenode  %}

{%  endtimeline  %}

####  7.  链接卡片 link

```
{% link 糖果屋教程贴, https://akilar.top/posts/615e2dec/, https://cdn.jsdelivr.net/gh/Akilarlxh/akilarlxh.github.io/img/siteicon/favicon.ico %}
```

{% link 糖果屋教程贴, https://akilar.top/posts/615e2dec/, https://cdn.jsdelivr.net/gh/Akilarlxh/akilarlxh.github.io/img/siteicon/favicon.ico %}