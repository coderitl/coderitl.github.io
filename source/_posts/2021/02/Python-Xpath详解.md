---
title: Python-Xpath详解
tags:
  - Python
  - Xpath
categories: Python
abbrlink: 45057
date: 2021-02-09 10:08:57
top_img:
cover:
---

###  Python-Xpath详解

> 
>
> 网页插件: `XPath Helper`
>
> 视频推荐: 慕课网 `web端功能自动化定位元素`
>
> 

1. 认识浏览器默认`xpath`,`ctrl+f`调出浏览器输入`xpath`

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/chromeXpath.png" width="600">

2.  `xpath`语法

   ```bash
   <div id="nav-bar" class="nav-bar"> 导航 </div>
   
   //tag-name[@attribute='value']
   
   Eg.
   
   	//div[@id='nav-bar'] # id 选择器
   	//div[@class='nav-bar'] # 类选择器
   	
   ```

   

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/xpathbaidu.png" width="600">

    

3.  `/`和`//`的区别

   > 
   >
   > `/` : 元素是上一级节点的子节点中的一个，不能跳级
   >
   > `//`:  下级任何子节点或者任何嵌套子节点中的一个，可以跳级
   >
   > 

4.  如何构建一个有效的`xpath`

   ```bash
   灵活使用 / 和 //
   ```

5.  使用`text`定位

   ```bash
   //tag-name[text()='value']
   ```

6. 平级节点或父级节点定位

   ```bash
   //tag-name[text()='value']//parent::parent-tag-name//preceding-sibling::tag-name/ 
   ```

7.  获取`xpath`时注意源码获取 目标`xpath`，因为渲染问题导致查找出错

8. 获取 `a`的`href`值

   ```bash
   ···a/@href # 获取 a 的 href 值
   ···a/text()  # 获取 a 的文本值
   ```

   