---
title: Javascript-面向对象编程
tags:
  - Javascript
categories: javascript
abbrlink: 41834
date: 2021-01-18 18:13:02
top_img:
---

###   Javascript-面向对象编程

####  面向过程和面向对象的对比

+ 面向过程
  - 优点: 性能比面向对象高,适合跟硬件联系很紧密的东西
  - 缺点: 没有面向对象易维护,易复用,易扩展

+ 面向对象
  + 优点: 易维护,易复用,易扩展,由于面向对象有封装，继承,多态性的特性，可以设计出低耦合的系统,使系统更加灵活,更加易于维护
  + 缺点: 性能比面向过程低

+ 对象是由属性和方法组成的
  + 属性: 事物的特征,在对象中用属性来表示(常用名词)
  + 方法: 事物的行为,在对象中用方法来表示(常用动词)

####  类(`class`)

+ `类`抽象了对象的公共部分,它繁殖某一大类(class)
+ `对象特指`某一个,通过实例化一个具体的对象

+ 创建类

  ```javascript
    /*
            1. 通过 class 关键字创建类,类名习惯性定义首字母大写
            2. 类里面有个 constructor 函数,可以接受传递过来的参数,同时返回实例对象
            3. constructor 函数只要 new 生成实例时,就会自动调用这个函数,如果我们不写这个函数,类也会自动生成这个函数
            4. 生成实例 new 不能省略
            5. 创建类m类名后面没有小括号,生成实例,类名后面加小括号,构造函数不需要加 function
          */
  ```

  ```javascript
    // 创建类
          class Star {
              // 构造函数
              /*
              constructor() 方法是类的构造函数(默认方法) 用于传递参数,返回实例对象,通过new 命令生成对象实例时,自动调用
              该方法,如果没有显示定义,类内部会自动给我们创建一个  constructor()
              */
              constructor(uname) {
                  this.uname = uname
              }
          }
          // 利用类创建对象 new
          var bin = new Star('BIN-CODE');
          console.log(bin);
  
        
  ```

  + 类中添加方法

    ```javascript
      // 1. 类里面的所有函数不需要写 function
     // 2. 多个函数方法之间不需要添加逗号分隔  
    // 创建明星类
            class Star {
                // 构造函数
                constructor(uname, age) {
                    this.uname = uname;
                    this.age = age;
                }
                study(song) {
                    console.log('2021.01.16·········>: ' + this.uname, '休息后在唱: ' + song);
                }
                sleep() {
                    console.log('我要睡觉了·········');
                }
            }
            var bin = new Star('Bin-Code', 2)
            console.log(bin);
            // 类方法调用
            bin.study('时间过客');//输出结果: 2021.01.16·········>: Bin-Code 休息后在唱: 时间过客
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/javascriptClass.png">

####  继承

+ 继承

  ```javascript
    // super 关键字用于访问和调用对象父类上的函数,可以调用父类的构造函数,也可以调用父类的普通函数
          /*
              1. 继承中,如果实例化子类输出一个方法,先看子类有没有这个方法,如果有就先执行子类的
              2. 继承中,如果子类里面没有,就去查找父类有没有这个方法m如果有,就执行父类的这个方法(就近原则)
          */
  ```

  ```javascript
  
          // 父类
          class Father {
              say() {
                  // console.log('我是父类···');
                  return 'Father类'
              }
          }
          // 子类
          class Son {
              say() {
                  console.log('我是子类···');
              }
          }
          // 实例化父类
          var father = new Father();
          father.say() // 我是父类···
  
          // 实例化子类
          var son = new Son();
          son.say() // 我是子类···
  
          class Cfat extends Father {
              // 类的继承 extends 关键字
              say() {
                  console.log(super.say() + '被继承了···'); // Father 类被继承了···
              }
          }
          var cc = new Cfat();
          cc.say();
  ```

+ 子类扩展

  ```javascript
  // 利用 super 调用父类的构造函数
  // super 必须在子类 this 之前调用
  class Father {
              constructor(x, y) {
                  this.x = x;
                  this.y = y;
              }
              sum() {
                  console.log('求和结果是: ', this.x + this.y);
              }
          }
  
          // 继承父类
          class Son extends Father {
              constructor(x, y) {
                  // 目的: 调用父类的加法函数
                  // 利用 super 调用父类的构造函数
                  // super 必须在子类 this 之前调用
                  super(x, y);
                  this.x = x;
                  this.y = y;
              }
              // 子类扩展
              mul() {
                  console.log('做差的结果: ', this.x - this.y);
              }
          }
          var son = new Son(6, 3);
          // 子类调用父类
          son.sum();
          // 子类调用扩展方法
          son.mul();
  ```

+ 今日`https://www.bilibili.com/video/BV1u7411573c?p=8`