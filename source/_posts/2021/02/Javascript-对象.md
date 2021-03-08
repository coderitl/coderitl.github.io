---
title: Javascript-对象
tags:
  - javascript
  - 对象
categories: javascript
abbrlink: 27752
date: 2021-02-02 16:30:42
---

###  Javascript-对象

+ 对象

  ```javascript
  对象属于一种复合的数据类型,在对象中可以保存多个不同数据类型的属性
  ```

+ 对象的分类

  ```javascript
  对象的分类：
     - 由 ES 标准中定义的对象, 在任何的 ES 的实现中都可以使用
     - 比如: Math String Number Boolean Function Object····
  宿主对象:
      - 由 JS 的运行环境提供的对象,目前来讲主要指由浏览器提供的对象
      - 比如: DOM BOM
   自定义对象:
  	- 由开发人员自己创建的对象
  ```

+ 创建对象

  ```javascript
  使用 new 关键字调用函数是构造函数 constructor 构造函数是专门用来创建对象的函数
  
  // 创建对象
   var obj = new Object();
  ```

+ 对象的基本操作

  ```javascript
  // 向对象中添加属性
  
  语法:
  
  	对象.属性名 = 属性值;
  
  // 读取对象的值
  	对象.属性名
  
  // 修改属性值
  	对象.属性名 = 新值;
  
  // 删除对象的属性
  
  	delete 对象.属性名
  
  ```

+ 字面量定义

  ```javascript
    var objs = {
              name: 'name-value',
              age: 10,
              add: function () {
                  alert(1)
              }
          }
  ```

  

###  工厂创建对象

```javascript

        function createDog(name, age) {
            var obj = new Object();
            obj.name = name;
            obj.age = age;
            return obj;
        }
        var dog1 = createDog('xiaohuang', 2);
        console.log(dog1);

```



###  构造函数

```javascript
构造函数就是一个普通的函数m创建方式和普通函数没有区别

不同的是构造函数习惯上首字母大写

function Person(){}

var per = new Persopn();

```

+ 构造函数的执行过程
  1.  立刻创建一个新的对象
  2.  将创建的对象设置为函数中 this
  3.  逐行执行函数中的代码
  4.  将新建的对象作为返回值返回

```javascript
  function Person(name, age, gender) {
            this.name = name;
            this.age = age;
            this.gender = gender;
            console.log('this: ', this);
        }
        var per = new Person('name', 20, 'gender');
        console.log(per);
```

<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/this.png">

```javascript

使用 instanceof 可以检查对象是否是一个类的实例

语法:

	对象 instanceof 构造函数
	console.log(per instanceof Person) // true

使用同一个构造函数的创建的对象,我们称为一类对象,也将一个构造函数称为一个类 通过一个构造函数创建的对象m称为该类的实例

```



###   this 的情况

1. 当以函数的形式调用时，`this` 就是`window`
2.  当以方法形式调用时m谁调用方法 `this`就是谁
3.  当以构造函数的形式调用时，`this`就是新创建的那个对象



###  原型对象

```javascript
我们创建的每一个函数，解析器都会向函数中添加一个属性 prototype 

这个属性对应着一个对象，这个对象就是我们所谓的原型对象

如果函数作为普通函数调用 prototype 没有任何作用

当函数以构造函数的形式调用时,我们可以通过 __proto__ 来访问该属性

原型对象就相当于一个公共区域m所有同一个类的实例都可以访问到这个原型对象，我们就可以将对象中共有的内容,统一设置到原型对象中

当我们访问对象的一个属性或方法时,它会现在对象自身中寻找，如果有则直接使用，如果没有则会去原型对象中寻找,如果找到则直接使用。
```

