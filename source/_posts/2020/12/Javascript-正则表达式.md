---
title: Javascript-正则表达式
tags: javascript
categories: javascript
password: ''
abstract: 'Something is encrypted, please enter the password to view.'
message: 'Hello, password is required here'
wrong_pass_message: 'Sorry, this password doesn''t look right, please try again.'
wrong_hash_message: >-
  Sorry, this article cannot be verified, but you can still see the decrypted
  content
abbrlink: 20069
date: 2020-12-16 12:02:31
top_img:
cover:
---

###  Javascript-正则表达式

正则的概念：正则表达式是描述字符模式的对象

```javasc
var 变量 = / 正则表达式/匹配模式
```

+ 或者

  ```javascript
  | 表示或者
  [ab] == a | b [] 或者
  [a-z] 任意小写字母
  [A-Z] 任意大写字母
  [A-z] 任意字母
  
   // 忽略大小写 i
   var reg = /[A-Z]/i;
   console.log(reg.test('a')); // true
  
  ```

+ 修饰符

  | 修饰符 |                         描述                         |
  | :----: | :--------------------------------------------------: |
  |  `i`   |               执行对大小写不敏感的匹配               |
  |  `g`   | 执行全局匹配(查找所有匹配而非在找到第一个匹配后停止) |
  |  `m`   |                     执行多行匹配                     |

+ 检查一个字符串是否含有 `abc或adc或aec`

  ```javascript
  1. 观察匹配目标
  
  2. 分析
  	a 开头
      c 结尾
   reg = /a[bde]c/
  console.log(reg.test('abc')); // true
  ```

+ 以规定字符开头匹配 `^`

  ```javascript
  
          var arr = ['abc', 'adc', 'ref', 'bbc', 'abe', 'abf',];
          // 匹配数组中以 ab
          var reg = /^a/;
          for (var i = 0; i < arr.length; i++) {
              console.log(arr[i] + ':' + reg.test(arr[i]));
          }
  
  匹配以上字符
  
  ```

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20201231185349.png" title="匹配以 a 开头的字符">

+ 匹配除了`[^ ]`以外的字符

  ```javascript
  
          // 匹配除了 ab 以外的字符
          var reg = /[^ab]/;
          var arr = ['ab', 'abc', 'abr'];
          for (var i = 0; i < arr.length; i++) {
              // 请先预测一下结果
              console.log(arr[i] + ':' + reg.test(arr[i]));
          }
  
  ```

  {% hideBlock 请先预测一下结果 %}

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20201231190006.png">

  {% endhideBlock %}

+ 字符串和正则相关的

  |   方法    |              描述              |
  | :-------: | :----------------------------: |
  | `search`  |   检索与正则表达式相匹配的值   |
  |  `match`  | 找到一个或多个正则表达式的匹配 |
  | `replace` |  替换与正则表达式匹配的字符串  |
  |  `split`  |    把字符串分割为字符串数组    |

  ```javascript
  split()
  	-  可以将一个字符串拆分为一个数组
  	- 方法中可以传递一个正则表达式作为参数,这样方法将会根据正则表达式拆分字符串
  
     // 字符串 split()
          var str = '1a1b2c3d4f5g6h7j8';
  		// 以任意字符拆分字符串
          var reg = /[A-z]/;
          var result = str.split(reg);
          console.log(result);
  ```

  {% hideBlock split的分割结果 %}

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20201231191604.png">

  {% endhideBlock %}

