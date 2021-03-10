---
title: Hexo-JsDeliver
tags: Hexo
categories: Hexo
top_img: 'https://cdn.jsdelivr.net/gh/lovobin/hiddenContent/timeline.jpg'
cover: 'https://cdn.jsdelivr.net/gh/lovobin/hiddenContent/timeline.jpg'
abbrlink: 20985
date: 2020-12-24 20:21:18
---

###   Hexo-JsDeliver使用

+ 新建仓库
+ 提交内容
+ 发布版本(**`Releases 右侧栏`**)

###  发布版本后使用文件?

+ 第一次使用版本号（第一次引用）

  > `https://cdn.jsdelivr.net/gh/用户名/仓库名@版本号/文件路径`

+ 不使用版本号（复用）

  + 何为复用: {% note success %} 这里说的复用是重复使用,(想了几个词,但是没有解释清楚“`复用`”){% endnote %}

  > `https://cdn.jsdelivr.net/gh/用户名/仓库名/文件路径`

  <img src="https://cdn.jsdelivr.net/gh/lovobin/hiddenContent/timeline.jpg" title="请勿访问" width="600">

+ 为什么使用版本号

  {% note success %}  <font color="purple">使用版本号引用的优点在于：这个链接仅停留在发布版本号的时刻，无论仓库如何变化，这个版本号的文件都不会受到影响。同时可以避免 JSD 缓存问题 </font> {% endnote %}

+ 为什么去除版本号（`文件修改次数过多时推荐使用`）

  {% note success %} 在 `jsdeliver`前缀下,后续添加`用户名/仓库名/文件路径`引用的内容就直接会被使用,<font color="red">**但是在添加版本号新修改内容就不能得到访问**</font>,相比之下一些不需要改动的文件就添加版本号，时常改动的文件不建议添加版本号{% endnote %}

###  后续使用发现问题（`jsDeliver缓存引起`）

+ 未添加版本号很长一段时间不能加载出文件资源
+ 遗留问题: 添加内容后怎么快速得到资源访问(难道一直添加版本号疑虑中-- 目前只能这样)

