---
title: javascript-立即执行函数
tags: javascript
categories: javascript
top_img: 'https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20201231173933.png'
cover: 'https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20201231173933.png'
abbrlink: 3461
date: 2020-12-31 17:17:37
---

###  javascript-立即执行函数

+ 立即执行函数

  ```javascript
   // 立即执行函数
          (function () {
              console.log('匿名的立即执行函数');
          }())
  ```

+ 如何理解立即执行函数

  ```javascript
   // 立即执行函数
          (function () {
              console.log('匿名的立即执行函数');
          }())
        
  ```

  ```javascript
   // 如何理解立即执行函数
          var a = 'a';
          console.log(a);
  ```

  ```javascript
  
          var b = ('b');
          console.log(b);
         
  ```

  ```javascript
   // 如何调用一个函数呢？
          function sum() {
              console.log('我是被执行的函数···');
          }
          // 函数调用
          sum();
  
  ```

  ```javascript
     // 理解立即执行函数
  	/*
  	var a =  function () {
              console.log('匿名的立即执行函数');
          }()
       // 联想 不就是立即执行函数
          (a())
  	*/
          (  
              
           function () {
              console.log('匿名的立即执行函数');
          }() 
          
          )
  
  ```

  

