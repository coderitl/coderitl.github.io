---
title: Bootstrap-框架
tags:
  - HTML
  - bootstrap
categories: Bootstrap
abbrlink: 4045
date: 2021-02-18 11:35:16
---



###  Bootstrap-框架



####  响应式开发原理



> 就是使用媒体查询针对不同宽度的设备进行布局和样式的设置,从而适配不同设备的目的

|         设备划分         |      尺寸区间       |  划分   |   类前缀   |
| :----------------------: | :-----------------: | :-----: | :--------: |
|     超小屏幕(`手机`)     |      `<768px`       | `100%`  | `.col-xs-` |
|     小屏设备(`平板`)     | `>=768px ~ <992px`  | `750px` | `.col-sm-` |
|  中等屏幕(`桌面显示器`)  | `>=992px ~ >1200px` | `970px` | `.col-md-` |
| 宽屏设备(`大桌面显示器`) |     `>=1200px`      | `1170`  | `.col-lg-` |



####  响应式布局容器

> 
>
> 响应式需要一个父级作为布局容器,来配合子级元素来实现变化效果
>
> 原理: 就是在不同屏幕下,通过媒体查询来改变这个布局容器的大小，在改变里面子元素的排列方式和大小,从而实现不同屏幕下,看到不同的页面布局和样式变化。
>
> 



####  布局容器

> Bootstrap 需要为页面内容和栅格系统包裹一个 `.container`容器,Bootstrap 预先定义好了这个类,叫`.container`，它提供了两个做此用处的类。



####  栅格选项参数

+ 参数

  > 栅格系统用于通过一系列的行于列的组合来创建页面布局,你的内容就可以放入这些创建好的布局中

+ 按照不同屏幕划分为`1~12`等份

+ 行可以去除父容器作用 `15px`的边距

+ `xs-extra small`：超小,`sm-small`：小，`ms-medium`:中等，`lg-large`:大

+ 列大于 `12`，多余的列所在的元素将最为一个整体另起一行排列

+ 每一列默认有左右 `15px`的`padding`

+ 可以同时为一列指定多个设备的类名，以便于不同份数

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/bootstrap.png">

####  列嵌套

> 
>
> 栅格系统内置的栅格系统将内容再次嵌套
>
> 就是一个列内再分成若干份小列，可以通过添加一个新的 `.row`元素和一系列 `.col-sm-`元素到已经存在的`.col-sm-`元素内
>
> 

```javascript
嵌套列最好加一个行 `row`，这样可以取消父元素的 padding 值,而且高度自动和父级一样高
```



####   列偏移

> 使用`.col-md-offset-`类可以将列向右偏移。这些类实际是通过` * `选择器为当前元素增加了左侧的边距`margin`

<img src='https://gitee.com/wang_hong_bin/repo-bin/raw/master/offset.png'>

<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/writeOffset.png">

+ 中间偏移--居中显示

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/centerOffset.png">



####  列排序

> 通过使用 `.col-md-push-*`和`.col-md-pull-*`类就可以容易的改变列的顺序



####  响应式工具

> 为了加快对移动设备友好的页面开发工作,利用媒体查询功能,并使用这些工具可以方便的针对不同设备展示或隐藏页面内容

|    隐藏类    | 超小屏 | 小屏 | 中屏 | 大屏 |    可见类     |
| :----------: | :----: | :--: | :--: | :--: | :-----------: |
| `.hidden-xs` |  隐藏  | 可见 | 可见 | 可见 | `.visible-xs` |
| `.hidden-sm` |  可见  | 隐藏 | 可见 | 可见 | `.visible-sm` |
| `.hidden-md` |  可见  | 可见 | 隐藏 | 可见 | `.visible-md` |
| `.hidden-lg` |  可见  | 可见 | 可见 | 隐藏 | `.visible-lg` |

<img src="https://img-blog.csdnimg.cn/20210218181445529.gif">



###  案例实战

+ `bootstrap`中的内边距

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/alibaixiu.png">

+ 清除浮动

  ```css
  类: clearfix
  ```

+ 响应式

  ```css
  主要通过媒体查询进行屏幕尺寸控制 
  ```

+ 总结

  ```css
  移动端布局:
  	流式布局(百分比)
  	flex
  	rem
  	媒体查询
  
  主要需要选择一套主方案,其余为辅, 配合完成响应式布局
  
  ```

  

###  效果案例

![BootStrap响应式布局](https://img-blog.csdnimg.cn/20210221103806743.gif#pic_center)



###  发布

1. 文件进行`git`上传
2.  开启`git pages`
3.  文件进行`cdn`加速处理
4.  项目预览: <a href="https://lovobin.github.io/AliBaixiu/index.html">Bootstrap-响应式</a>

###  整体回顾

1. 先进行`PC`整体端布局
   + 划分区块
   + 将整个页面划分为 `左(2) 中(7) 右(3)`
2.  左侧导航布局
   + `logo`和`nav`
   + `logo`中使用`hidden-xs`在小屏对图片隐藏处理
   + `nav`由原来的 `100%`改为`width: 20%`并进行浮动处理
3.  中间部分
   + 图片不需要设置宽度,将会根据`7等比占据大小`
   + 当我们处于超小屏幕 `news` 第一个` li `宽度为 `100% `剩下的各占 `50% `
   + 当处于超小屏下对文字大小和图片进行隐藏处理
4.  右侧区域
   + 仅对样式添加,未进行其他操作