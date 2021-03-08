---
title: Canvas使用
tags:
  - html
  - canvas
categories: Canvas
abbrlink: 44759
date: 2021-02-02 11:46:33
top_img:
---

###   Canvas

####  Canvas 的简介

```javascript
是HTML5提供的一种新标签, ie9才开始支持的，Canvas是一个矩形区域的画布，可以用 JS 控制每一个像素在上面绘画。
canvas 标签使用 JavaScript 在网页上绘制图像，本身不具备绘图功能。canvas 拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。
```

####  Canvas 的基础使用

```html
    <canvas id="tutorial" width="600" height="600">
        当前的浏览器版本不支持,请升级浏览起器
    </canvas>
        
```

```javascript

		// 获取画布
        var canvas = document.getElementById('tutorial');
        // 获取上下文,上下文有两个 2d 的上下文和 3d 的上下文
        // 所有的图像绘制都是通过 ctx 属性或者 是方法进行设置的，和 canvas 标签没有关系
        var ctx = canvas.getContext('2d');
        // 设置颜色
        ctx.fillStyle = "green";
        // 绘制正方形 x y width height
        ctx.fillRect(100, 100, 100, 100); 
```

####  Canvas 像素化

```javascript
我们使用 canvas 绘制了一个图形,一旦绘制成功了,canvas 就像素化了它们。
```

####  Canvas 的动画思想

+ 效果演示

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/canvas-move.gif" width="600">

+ 实例源码

  ```javascript
   // 获取画布
          var canvas = document.getElementById('tutorial');
          // 获取上下文,上下文有两个 2d 的上下文和 3d 的上下文
          // 所有的图像绘制都是通过 ctx 属性或者 是方法进行设置的，和 canvas 标签没有关系
          var ctx = canvas.getContext('2d');
          // 设置颜色
          ctx.fillStyle = "green";
          // 绘制正方形
          // ctx.fillRect(100, 100, 100, 100);
          // 信号量
          var left = 100;
          // 动画过程
          setInterval(function () {
              // 清除画布 0,0 代表从什么位置开始清除 600 600 代表清除的宽度和高度
              ctx.clearRect(0, 0, 600, 600);
              // 更新信号量
              left++;
              // 重新绘制
              ctx.fillRect(left, 100, 100, 100)
          }, 5)
  ```

####  Canvas 填充和绘制

+ 效果演示

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/canvas.png">

+ 填充

  ```javascript
  
  ctx.fillStyle = 'color-value';
  
  ctx.fillRect(x,y,width,height);
  
  ```

+ 绘制

  ```javascript
  
  ctx.strokeStyle = 'color-value';
  
  ctx.strokeRect(x,y,width,hieght);
  
  ```

+ 清除画布内容

  ```javascript
  ctx.clearRect(x,y,canvas-width,canvas-height);
  ```

+ 具体实现

  ```javascript
  	<div>
          <button id="btn1"> 填充矩形 </button>
          <button id="btn2"> 绘制矩形边框 </button>
  		<button id="btn3"> 清除 canvas 画布内容 </button>
      </div>
      <canvas id="mycanvas" width="600" height="600">
          当前浏览器不支持 canvas,请升级浏览器后再浏览
      </canvas>
  ```

  ```javascript
   		var canvas = document.getElementById('mycanvas');
          // 获取 btn 
          var btn1 = document.getElementById('btn1');
          var btn2 = document.getElementById('btn2');
  		var btn3 = document.getElementById('btn3');
  
          // 获取上下文
          var ctx = canvas.getContext('2d');
          btn1.onclick = function () {
              // 设置填充颜色
              ctx.fillStyle = 'purple';
              // 设置填充
              ctx.fillRect(100, 100, 50, 50);
          }
          btn2.onclick = function () {
              // 绘制边框颜色
              ctx.strokeStyle = 'purple';
              // 绘制正方形
              ctx.strokeRect(300, 100, 50, 50);
          }
  
          btn3.onclick = function () {
                  // 清除画布内容
                  ctx.clearRect(0,0,canvas.width,canvas.height);
              }
  
  
  ```

  

####  Canvas 绘制路径

+ 作用

  ```javascript
  绘制路径作用是为了设置一个不规则的多边形状态
  ```

+ 步骤

  1. 设置路径的起点
  2.  使用绘制命令画出路径
  3.  封闭路径
  4.  填充或者绘制已经封闭路径的状态

  + 实现

    ```javascript
    		var canvas = document.getElementById('mycanvas');
            var ctx = canvas.getContext('2d');
            // 创建一个路径
            ctx.beginPath();
            // 移动绘制点
            ctx.moveTo(100, 100);
            // 描述行进路径
            ctx.lineTo(200, 200);
            ctx.lineTo(400, 180);
            ctx.lineTo(380, 50);
            // 封闭路径
            ctx.closePath();
            // 绘制不规则的图形
            ctx.strokeStyle = 'blue';
            // 没有 Rect 代表绘制 --> 描边
            ctx.stroke();  // 通过线条来绘制图形轮廓
    
    		 // 填充
            ctx.fillStyle = 'pink';
            ctx.fill(); // 通过填充路径的内容区域生成实心的图形
    
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/moveline.png" width="600">

  

####  圆弧绘制

```javascript
 		var canvas = document.getElementById('mycanvas');
        var ctx = canvas.getContext('2d');
        // 创建一个路径
        ctx.beginPath();
        // ctx.arc(x,y,r,start,end,boolean(direction) )
        ctx.arc(100, 100, 50, 0, 2 * Math.PI, true)
        ctx.stroke();
```

+ 参数解释

  ```javascript
  // 圆
  ctx.arc(100, 100, 50, 0, 2 * Math.PI, true)
  // 圆
  ctx.arc(100, 100, 50, 0, 8 [大于 7 都是圆], false)
  // 圆
  ctx.arc(100, 100, 50, 0, 2 * Math.PI, true)
  ```

  1.  100  `canvas内坐标起始点`
  2.  50  圆的半径
  3.  0 绘制起点
  4.  `2*Math.PI`  圆圈弧度
  5. `true` 逆时针

+ 效果图

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/circleCanvas.png">

> 0,1指的是开始和结束的位置,单位如果是数字,则代表一个圆弧的弧度(一个圆的弧度是`Math.PI * 2` ,约等于 7 个弧度) 所以如果为两个参数的差为 7 ，并且是 顺时针方向,则代表绘制一个圆



#### Canvas 小案例