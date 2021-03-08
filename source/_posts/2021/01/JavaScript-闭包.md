---
title: JavaScript-闭包
tags:
  - 闭包
  - Javascript
categories: javascript
abbrlink: 48434
date: 2021-01-29 17:19:08
top_img:
cover:
---

###   JavaScript-闭包

```javascript
当内部函数被保存到外部时,将会生成闭包。闭包会导致原有作用域链不释放，造成内存泄露。

Javascript高级程序设计指出: 闭包是指有权访问另一个函数作用域的变量的函数。

Javascrip权威指南指出: 从技术的角度将,所有的 Javascript 函数都是闭包: 它们都是对象,它们都关联到作用域链。

你不知道的Javascript中指出: 当函数可以记住并访问所在的词法作用域时,就产生了闭包,即使函数在当前词法作用域之外执行

```

+ 打印`0,1···9`

  ```javascript
    function test() {
              var arr = [];
              for (var i = 0; i < 10; i++) {
                  console.log(i); // 0 1 2 3 4 5 ···
                  arr[i] = function () {
                      console.log(i," "); // 10 10 10 ···
                      document.write(i + ' '); // 10 10 ···
                  }
              }
              return arr;
          }
  
          var myArr = test();
          for (var j = 0; j < 10; j++) {
              myArr[j](); //  document.write(i + ' ');
          }
  ```

+ 词法作用域

  ```javascript
    // 词法作用域: 指函数在定义(或声明)它们的作用域里运行，而不是在执行(或调用)它们的作用域里运行
          var value = 1;
          function foo() {
              console.log(value);
          }
          function bar() {
              var value = 2;
              foo();
          }
          bar(); // 1
  ```

  

+ 打印`0,1,2`

  ```javascript
  
          for (var i = 0; i < 3; i++) {
              setTimeout(function () {
                  console.log(i); // 3 ···
              }, 100)
          }
  
  1. var ==> let 
  
  2. 立即执行函数
          for (let i = 0; i < 3; i++) {
              (function (i) {
                  setTimeout(function () {
                      console.log(i, " ");
                  }, 100)
              }(i))
          }
  ```

  

+ 打印 `LI`的索引

  + 方法一

    ```html
     <ul id="ul">
            <li> item 1</li>
            <li> item 2</li>
            <li> item 3</li>
            <li> item 4</li>
     </ul>
    ```

    ```javascript
     // 点击每个 li 显示对应的索引
            var _ul = document.querySelector('#ul');
            // 获取子节点
            var lis = _ul.children;
            for (var i = 0; i < lis.length; i++) {
                lis[i].setAttribute('index', i)
                lis[i].onclick = function () {
                    console.log(this.getAttribute('index'));
                }
            }
    ```

  + 方法二

    ```javascript
    
            for (var i = 0; i < lis.length; i++) {
                (function (i) {
                    lis[i].onclick = function () {
                        alert(i);
                    }
                }(i))
            }
    ```

  + 方法三

    ```javascript
    for (var i = 0; i < lis.length; i++) {
                lis[i].index = i;
                lis[i].onclick = function () {
                    console.log(this.index);
                    alert(this.index);
                }
            }
    ```

    