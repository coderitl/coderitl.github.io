---
title: CSS-3d旋转木马
password: ''
abstract: 'Something is encrypted, please enter the password to view.'
message: 'Hello, password is required here'
wrong_pass_message: 'Sorry, this password doesn''t look right, please try again.'
wrong_hash_message: >-
  Sorry, this article cannot be verified, but you can still see the decrypted
  content
abbrlink: 31582
date: 2020-12-07 13:35:13
tags:
categories:
top_img:
cover:
---

###  CSS-3d旋转木马

+ 效果预览

  <img src="https://img-blog.csdnimg.cn/20201207133244557.gif" alt="CSS-3d旋转木马" title="CSS-3d旋转木马">

+ `css`源码

  ```css
   body {
              perspective: 1000px;
          }
  
          section {
              position: relative;
              width: 300px;
              height: 200px;
              margin: 200px auto;
  
              transform-style: preserve-3d;
              animation: rotateImg 10s linear infinite;
          }
  
          @keyframes rotateImg {
              0% {
                  transform: rotateY(0);
              }
  
              100% {
                  transform: rotateY(360deg);
              }
          }
  
          section:hover {
              /* 鼠标移入暂停动画 */
              animation-play-state: paused;
          }
  
          section div {
              position: absolute;
              top: 0;
              left: 0;
              width: 100%;
              height: 100%;
              box-shadow: 0 0 10px rgba(0, 0, 0, .5);
          }
  
          section div:nth-child(1) {
              background: url('img/01.jpg') no-repeat;
              transform: translateZ(300px);
          }
  
          section div:nth-child(2) {
              background: url('img/02.jpg') no-repeat;
              transform: rotateY(60deg) translateZ(300px);
          }
  
          section div:nth-child(3) {
              background: url('img/03.jpg') no-repeat;
              transform: rotateY(120deg) translateZ(300px);
          }
  
          section div:nth-child(4) {
              background: url('img/04.jpg') no-repeat;
              transform: rotateY(180deg) translateZ(300px);
          }
  
          section div:nth-child(5) {
              background: url('img/05.jpg') no-repeat;
              transform: rotateY(240deg) translateZ(300px);
          }
  
          section div:nth-child(6) {
              background: url('img/06.jpg') no-repeat;
              transform: rotateY(300deg) translateZ(300px);
          }
  ```

+ `html`

  ```html
    <!-- 
          思考原理: 
              1. 涉及定位
              2. 旋转
              3. 3D效果
              4. 鼠标移入移出
              5. css3 动画
       -->
      <section>
          <div></div>
          <div></div>
          <div></div>
          <div></div>
          <div></div>
          <div></div>
      </section>
  ```

  