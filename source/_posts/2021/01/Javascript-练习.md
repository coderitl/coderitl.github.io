---
title: Javascript-练习
tags:
  - Javascript
categories: javascript
abbrlink: 22099
date: 2021-01-29 18:46:53
top_img:
cover:
---

###  Javascript-练习

1. 判断一个字符串中出现次数最多的字符m并统计次数

   ```javascript
   // 出现次数最多的字符的变量
           var value = '';
           // 出现的次数的变量
           var index = 0;
           // 原始字符串
           var str = 'aaabbbcccaaabbbaaabbbbbbbbb';
           // 把字符串转换为数组
           var arr = str.split('');
           // 将数组进行排序 把数组在转换为字符串
           str = arr.sort().join('');
           // 正则进行匹配
           var reg = /(\w)\1+/g;
           str.replace(reg, function (val, item) {
               if (index < val.length) {
                   index = val.length;
                   value = item;
               }
           })
           console.log('出现的次数: '+index,'出现的字符是: '+value);
   ```

2.  优先级,作用域

   ```javascript
   1. 作用域链: 从内部(当前作用域)逐级向上查找
   
   2. 顺序、优先级
   	
   	变量 ==> 函数 => 参数 ==> 变量提升
   
   ```

   ```javascript
   顺序、优先级:
   
           var str = 'str';
           function fun1() {
               var str = 'fun1';
               console.log(str); // fun1
           }
           fun1();
   
   ----------------------------------------------------------------------------------
   
   
           var str1 = 'str';
           function fun1(str1) {
               console.log('a: ', str1);
   			str1 = 'a';
               function str1() {
                   return 'b: str1 fun'
               }
               console.log(str1);  // function(){ return 'b: str1 fun'}
           }
           fun1();
   
   
   ```

   + 输出

     ```javascript
       		// 全局作用域
     		var bar = 1;
             function test() {
                 // 变量提升 var bar;
                 console.log(bar); // undefined
                 // 局部变量
                 var bar = 2;
                 console.log(bar); // 2 
             }
             test();
     ```

   + 输出值

     ```javascript
     // 变量 
     var foo = function () {
                 console.log(1);
             }
      // 函数
       function foo() {
           console.log(2);
       }
      
     	foo(); // 1 变量 > 函数 优先级
     ```

   + 输出值

     ```javascript
     		// 1 级 作用域
             function c() {
                 // 2 级 作用域
                 var b = 1;
                 function a() {
                     // 3 级作用域
                     // 变量提升 var b;
                     console.log('undfined: ', b); // undifined
                     var b = 2;
                     console.log('2: ', b); // 2
                 }
                 a();
                 console.log('b2: ',b); // 1, 在 2 级 作用域下寻找变量 b 
             }
             c();
     ```

   + 匿名函数

     ```javascript
     
             var name = 'World';
             (function () {
                 // 变量提升 var name; 内部存在 name 变量
                 if (typeof name === 'undefined') {
                     var name = 'Jack';
                     console.log('Goodbye' + name);
                 } else {
                     console.log('Hello ' + name);
                 }
             })()
     
      //result:  Goodbye  Jack
             
     ```

   + 输出

     ```javasc
            var f = true;
             if (f === true) {
                 var a = 10;
             }
             function fn() {
                 var b = 20;
                 c = 30;
             }
             fn();
             console.log(a); // 10
             console.log(b); // undefined  不能拿到内部
             console.log(c); // undefined window.c30 ==  c = 30
     ```

   + 解析`URL`为对象

     ```javascript
      function parseQueryString(url) {
                 var obj = {};
                 var urls = url.split('?');
                 console.log(urls);
                 var arr = urls[1].split('&');
                 console.log(arr);
                 for (var i = 0, len = arr.length; i < len; i++) {
                     var brr = arr[i].split('=');
                     obj[brr[0]] = brr[1];
                 }
                 return obj;
             }
             console.log(parseQueryString('https://www.google.com/search?q=js&oq=js&aqs=chrome..69i57j69i61l3.564j0j4&sourceid=chrome&ie=UTF-8'));
         </script>
     ```

     

