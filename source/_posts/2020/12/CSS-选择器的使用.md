---
title: CSS-选择器的使用
tags:
  - css
  - HTML
categories: css
abbrlink: 5342
date: 2020-12-30 10:22:40
---

###  CSS-选择器的使用

+ 常用选择器

  ```css
  
  元素选择器:
  	作用: 根据标签名选中指定的元素
      语法: 标签名{}
      Eg. div{}  p{} 
  
  ```

  ```css
  ID 选择器:
  	作用: 根据元素的 id 属性值选中一个元素	
  	语法:	#id-属性值{}
  	Eg. #box{}
  ```

  ```css
  类选择器:
  	作用: 根据元素的 class 属性值选中一组元素
  	语法: .class-属性值
  
  注意: class 是一个标签的属性，它和 id 类似,不同的是 class 可以重复使用,可以通过 class 属性来为元素分组
  ```

  ```css
  通配选择器:
  	作用: 选中页面中的所有元素
  	语法: *
  ```

+ 复合选择器

  + 交集选择器

    {% tip cogs %}

    交集选择器:

    ​	作用: 选中同时符合多个条件的元素

    ​	语法: 选择器1选择器2···

    ​	注意点: 交集选择器中如果有元素选择器,必须使用元素选择器开头

    {% endtip %}

    ```css
    /* 将 class 为 red 的 div 的字体 大小设置为 30px */
    条件解析:
      类名: red
      元素: div
    
      <style>
            .red{
                color: red;
                font-weight: 30px;
            }
            div.red{
                color: red;
                font-size: 40px;
                font-weight: 700;
            }
        </style>
    ```

  + `HTML结构`

    ```html
    <body>
        <div class="red"> 变红色 </div>
        <p class="red"> 变红色 </p>
    </body>
    ```

    {% hideBlock 请问效果将会是什么样? %}

    <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/choice.png" width="400" height="400">

    {% endhideBlock %}

+ 分组选择器(并集选择器)

  ```css
  /* 同时选中 div 和 span 元素 */
  div,span{}
  /* 通过类名同时选中 */
  .nav{},.siderbar{}
  
   /* 使用逗号分割多个选择器  */
          .nav,
          .siderbar {
              color: blue;
              font-size: 40px;
              font-weight: 700;
              background: pink;
          }
  ```

  ```html
  
  <body>
      <div class="nav"> 我是 nav </div>
      <div class="siderbar"> 我是 siderbar </div>
  </body>
  
  ```

  {% hideBlock 效果查看 %}

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/splitNav.png" width="400" height="420" alt="资源加载中">

  {% endhideBlock %}

+ 元素之间的关系

  {% tabs yuansu-1 %}

  <!-- tab 父元素 -->

  父元素:

  + 直接包含子元素的元素叫父元素

  <!-- endtab -->

  <!-- tab 子元素 -->

  子元素: 

  + 直接被父元素包含的元素是子元素

  子元素选择器: 

  +  作用: 选中指定元素的指定子元素
  + 语法: `父元素 > 子元素`

  <!-- endtab -->

  <!-- tab 祖先元素 -->

  祖先元素:

  - 直接或间接包含后代的元素叫做祖先元素
  - 一个元素的父元素也是它的祖先元素

  <!-- endtab -->

  <!-- tab 后代元素 -->

  后代元素:

  -  直接或间接被祖先元素包含的叫做后代元素
  - 子元素也是后代元素

  后代元素选择器:

  + 作用: 选中指定元素内的指定后代元素
  + 语法: `祖先  后代(之间空格隔开)`

  <!-- endtab -->

  <!-- tab 兄弟元素 -->

  兄弟元素：

  + 拥有相同父元素的元素是兄弟元素

  兄弟选择器:

  + 寻找`下一个`(紧挨着的)
  + 语法: `前一个元素 + 下一个`
  + 选择下边`所有`的兄弟
  + 语法:` 兄 ~ 弟`

  <!-- endtab -->

  {% endtabs %}

+ 属性选择器

  

  {% tabs  %}

  <!-- tab 属性选择器使用 -->

  [属性名]  选择含有指定属性的元素:

  [属性名=属性值] 选择含有指定属性和属性值的元素

  [属性名 ^= 属性值] 选择属性值以指定值开头的元素

  [属性名 $=属性值] 选择属性值以指定结尾的元素

  [属性名 *=属性值] 选择属性值中含有某值的元素的元素

  <!-- endtab -->

  <!-- tab 内容图解 -->

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/titleS.png" width="600" height="600">

  <!-- endtab -->

  {% endtabs %}

+ 伪类选择器

  - 伪类

    {% tip cogs %}

    伪类(不存在的类,特殊的类)

    - 伪类用来描述一个元素的`特殊状态`
    - 被点击的元素,鼠标移入的元素

    {% endtip %}

  {% tabs child-1 %}

  <!-- tab 伪类选择器 -->

  - 第一个选择

    `元素:first-child{}`

  - 最后一个的选择

    `元素:last-child{}`

    `元素:last-child(n/even/odd/2n+1){}`

  - 第 n 个元素的选择
    - 特殊值
      - `n `第 `n` 个 的 `n` 的范围`0 `到 正无穷
      - `2n`或`even`表示选中偶数位的元素
      - `2n+1`或`odd`表示选中奇数位的元素

  <!-- endtab -->

  <!-- tab 否定伪类 -->

  `元素名:not()`

  `Eg. 去除第三个 li 的选择`

  `ul li:not(:nth-child(3)){}`

  <!-- endtab -->

  

  <!-- tab 超链接伪类 -->

  - 没有访问过的链接(a有效 a:link)
  - 访问过的链接(a有效 a:visited)
  - :active
  - :hover

  <!-- endtab -->

  <!-- tab 伪元素:首字母下沉 -->

  伪元素: 表示页面中一些特殊的并不真是存在的元素(`特殊的位置`)

  伪元素使用:   `::开头`

  + 首字母下沉效果

    > `元素名::first-leffer{}` 第一个字母
    >
    > `元素名::first-line{}` 第一行
    >
    > 常用(`必须结合 contetn使用`):
    >
    > `::after{}`
    >
    > `::before{}`

  <!-- endtab -->

  {% endtabs %}

###  选择器的权重

```html
内联样式			1000
id 选择器			 100
类和伪类选择器		   10	
元素选择器			1
统配选择器			0
继承				没有优先级
比较优先级时: 需要将所有选择器的优先级进行相加计算,最后优先级越高,则越优先级显示(分组选择器是单独计算的)
```

###  像素和百分比

```css
像素:

百分比: 也可以将属性值设置为相对于其父元素属性的百分比(父元素说法不严谨,有待改进)
```

###  `em`和`rem`

```html
em:
    - em 是相对于元素的字体大小来计算的
    - 1em = 1(font-size)
    - em 会根据字体大小的改变而改变
rem:
	- rem 是相对于根元素的字体大小来计算
```

