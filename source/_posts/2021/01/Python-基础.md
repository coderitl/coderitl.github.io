---
title: Python-基础
tags:
  - Python
  - Python-基础
categories: Python
abbrlink: 62556
date: 2021-01-03 16:27:23
top_img:
cover:
---

###   Python-基础

```bash

# 生成文件 pip freeze > requirements.txt

# 依赖项安装: pip install -r requirements.txt

```



####  1. 格式化输出 `format`

```python
person_name = '张三'

person_age = 18

person_sex = '男'

print('''
    姓名: {}
    
    年龄: {}
    
    性别: 
    
'''.format(person_name, person_age, person_sex))
```

#### 2. `%s`

```python

person_name = '张三'

person_age = '18'

person_sex = '男'


print('姓名:%s 年龄:%s 性别:%s'%(person_name,person_age,person_sex))

```

####  3. `input`输入

```python
# input

name = input('请输入 python: ')

print('学习语言: '+name)

```

#### 4. 进制转换

```python

```

#### 5. 三目运算符

```python
# 三目运算符
a = 4
b = 6
result = a + b if a < b else b - a
# 10 
print(result) 
```

####  6. `if` 语句

```python
# if
a = 10
b = 30

if a>b:
    print(a)
else:
    print(b)
   
```

####  7.  `for` 循环

```python
# 使用系统 range 指定范围
arr = ['a',1,{'value':'bin'}]
for i in range(len(arr)):
    print(arr[i])

-------------------------

# 输出 3 遍 hello world
for ia in range(3):
    print('Hello world')

-------------------------------

# 九九乘法口诀表
for i in range(1, 10):
    for j in range(1, i+1):
        print('{}x{}={}\t'.format(j, i, i*j), end='')
    print()
    
```

####  8. `for else`结构

```python
# pass 空语句
```

####  9. `while`循环

```python
n = 1
while n<=30:
    if n%3==0 and n%5==0:
        print('---------------->',n)
    n+=1
    
# python 独有方法
ceng = 1
while ceng<=5:
    print('*'*ceng)
    
    ceng+=1
    
# 逻辑
ceng = 1
while ceng <= 5:
    count = 1
    while count <= ceng:
        print('*',end='')
        count += 1
    print()
    ceng += 1
```

####  10. 字符串

+ 常量

  ```python
  s1 = 'abc'
  s2 = "abc"
  s3 = '''abc'''
  print(id(s1),id(s2),id(s3))
  
  s1: 2128137317424
  s2: 2128137317424 
  s3: 2128137317424
      
  # 三引号占用的内存空间与单双引号不同
  
  print(s1==s2) # 比较的是内容 True
  print(s1 is s2) # 比较的是地址 True
  ```

+ 变量

  ```python
  s1 = input('请输入:')
  s2 = input('请输入:')
  print(s1==s2) # True
  print(s1 is s2) # False ,常量是True， input()底层做了处理，所以最后地址是不一样的
  ```

+ 切片使用

  ```python
  filename = 'picture.png'
  
  filename[5] # 从0 开始 取第 5 位
  
  filename[0:5] # 取出 5 位
  
  filename[::-1] # 倒叙输出
  
  ```

+ 字符串的内置方法

  ```python
  # 大小写相关
  
  str = 'abc bb'
  print(str.capitalize()) # 首字母大写 Abc bb
  print(str.title()) #  单词的每个首字母大写 Abc Bb
  print(str.upper()) # 所有字母大写 ABC BB
  print(str.lower()) # 所有字母小写  abc bb
  
  ```

+ 随机数应用(验证码)

  ```python
  
  # 验证码案例
  code = ''
  import random
  s = 'QWERTYUIOPASDFGHJKLZXCBN'
  
  for i in range(4):
      ran = random.randint(1, len(s) - 1)
      code += s[ran]
  print(code)
  user_input = input('请输入验证码: ')
  if user_input.lower() == code.lower():
      print('验证码输入正确')
  else:
      print('验证码输入错误')
  ```

+ 查找相关的

  ```python
  # find()  rfind() lfind() index rindex() replace()
  
  str = 'abcd'
  print(str.find('e')) # 找不见返回 -1 ,找见输出起始位置
  print(str.rfind('e')) # 找不见返回 -1 ,找见输出起始位置
  
  # index() 找不见报异常
  # ValueError: substring not found
        
  ```

  ```python
  # rfind()
  x = path.rfind('/')
  filename = path[x+1::]
  print(filename)
  
  ```

  ```python
  # replace()
  
  replace(old,new[,max])
  
  # 将空格替换为 # 号
  s1 = 'indec lucy luks gooes'
  s2 = s1.replace(' ','#')
  print(s2)
  
  # 指定替换的做大次数
  s2 = s1.replace(' ','#',2)
  ```

+ 编码相关

  ```python
  # encode 编码
  
  # decode 解码
  
  # 解码编码
  msg = '人生苦短,我学 Python'
  # encode('指定编码') decode('')
  result = msg.encode('utf-8')
  print(result)
  
  decode =result.decode('utf-8')
  print(decode)
  
  ```

+ `endswith() startwith()`

  ```python
  
  应用: 文件上传 只能上传(jpg，png,bmp,gif)
      
  # 返回值都是布尔类型 True False  
  
  # endswith() 
  filename = 'python.png'
  result = filename.endswith('png') #  filename 是否以 png 结尾
  print(result) # True
  
  --------------------------------------------------------------------------------
  # startwith() 
  s = 'hello'
  result = s.startswith('he') # 判断是否以 he 开头
  print(result) # True 
  
  
  ```

+ `join`使用

  ```python
  # join
  new_str = '_'.join('abc') # 用符号连接字符串
  print(new_str) # a_b_c
  ```

  

+ 去除左右空格

  + 去除左边空格

    ```python
    # 去除左空格
    s = '   hello '
    s = s.lstrip()
    print(s+'1') # hello  1
    ```

  + 去除右边空格

    ```pytohn
    # 去除右空格
    s = '   hello '
    s = s.rstrip()
    print('a'+s+'1') # a   hello1
    ```

  + 去除左右两边的空格

    ```python
    # 同时去除空格
    s = '   hello  '
    s = s.strip()
    print('a'+s+'1') # ahello1
    
    ```

+ 分割字符串

  ```python
  # split('指定字符切割','分割次数 int ')
  s = 'hello world hello kitty'
  result = s.split(' ')
  print(result)
  
  # 结果是 列表
  # ['hello', 'world', 'hello', 'kitty']
  ```

+ 求取定个数(统计)

  ```python
  s = 'aaaaaaaaa'
  s.count('s')
  ```

  

####  11. 列表

+ 遍历列表

  ```python
  for i in range(len(movies)):
      print(movies[i])
  ```

+ 修改列表

  ```python
  branch = ['a','b','c']
  
  branch[0] = 0
  
  print(branch) # [0, 'b', 'c']
  ```

+ 列表元素删除

  ```python
  del branch[0]
  print(branch)
  
  # 删除相关
  remove()
  pop()
  clear()
  ```

+ 列表的切片操作

  ```python
  branch[1::]
  print(branch[1::])
  ```

+ 列表的函数使用

  + `append()`

    ```python
    # append() 末尾追加
    
    
    ```

  + `extend()`

    ```python
    # extend() 
    
    	+、  extends() 列表的合并
    
    ```

  + `insert()`

    ```python
    
    指定位置插入
    
    ```

+ 列表的排序

  ```python
  a = [100,1,5,20,45,11]
  
  # 默认升序
  sorted(列表)
  # print(sorted(a)) [1, 5, 11, 20, 45, 100]
  
  # 翻转
  sorted(a, reverse=True)
  # print(sorted(a, reverse=True)) [100, 45, 20, 11, 5, 1]
  ```

+ 冒泡排序

  ```python
  
  ```

+ 选择排序

  ```python
  
  ```

####  12 . 元组

```python
特点: 
    1. 定义的符号: ()
    2. 元组中的内容不可修改
    3. 关键字: tuple
    
    只能执行 查 的操作
    
```

```python
import  random
list1 = []
for i in range(10):
    ran = random.randint(1,20)
    list1.append(ran)
print(list1)
t = tuple(list1)
print(t)

[3, 9, 18, 17, 7, 19, 8, 14, 7, 15]
(3, 9, 18, 17, 7, 19, 8, 14, 7, 15)

# 使用列表进行增删改查

```

####  13. 字典

```python
# 空字典 dict1 = dict()
# 空列表 list1 = list()
# 空元组 tuple1 = tuple()
dict = {}
```

+ 增加

  ```python
  dict[key] = value;
  
  # 同名则为修改
  
  ```

+ 删除

  ```python
  del 字典名[key]
  
  对应的函数:
      字典名.remove('key') # 没有报错
      字典名.pop('key')
      字典名.clear()
      字典名.popitem()
  
      
  注意:
      pop([key,default])
      根据 key 删除字典中的键值对,返回值是 只要删除成功，怎返回键值对的值 value
      pop 的默认值,往往是在删除的时候没有找到对应的 key ，则返回 default 默认值
      
      popitem(): 随机删除字典中键值对(一般都是从末尾删除元素)
          
  ```

+ 修改

  ```python
  # 同名则为修改
  ```

+ 查询

  ```python
  dict[key]
  ```

+ 字典的拼接

  ```python
  update() 
  ```

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210104101610.png">



+ 形式转换

  ```python
  fromkeys(seq)
  
  将 seq 转成字典的形式,如果没有指定默认的 value 则用 None
  
  list1 = ['a','b','c']
  
  new_dict = dict.fromkeys(list1);
  
  ```

####  14. 集合

+ 关键字

  ```python
  集合: set 关键字 无序不重复的元素
      
  作用: 不重复的特点
      
  ```

+ 声明集合

  ```python
  set() # 创建空集合,只能使用 set()
  ```

+ 应用

  ```python
  list1 = [1, 2, 3, 4, 1, 2, 3]
  newList = set(list1)
  print(newList) # {1, 2, 3, 4}
  
  ```

+ 增

  ```python
  s1 = set()
  # 增
  # 增加一个
      s1.add('add-01')
      s1.add('add-02')
      s1.add('add-03')
      print(s1) # {'add-03', 'add-01', 'add-02'}
  # 增加多个
  	update()
      t1 = ('a','b')
      s1.update(t1)
      print(s1) # 输出无序
  
  ```

+ 删

  ```python
  remove() # 存在删除,没有报错 keyValue
  pop() # 随机删除,在集合中删除第一个
  clear() # 清空
  
  dicard() # 类似remove() 在移除没有元素不报错
  
  
  ```

+ 改

+ 查

+ 可变和不可变

  ```python
  
  
  不可变: 对象指向的内存中的值是不可以改变
      
  不可变的类型: int str float 元组tuple
      
  ----------------------------------------------    
      
  可变的； 对象所指向的内存中的值是可以改变的
  
  可变类型: 字典dict  列表list
      
     
  ```

+ 类型转换

  ```python
  str()  int()  list()  dict()  set()  tuple()
  ```

  + `str`可转类型

    ```python
    int list set tuple
    
    ----------------------------  str--> int  --------------------
    
    s = '1234' # 字符串类型
    i = int(s) # 字符串转换为数字
    print(type(i)) # <class 'int'>
    
    -----------------------------  str--> list --------------------
    list1 = list(s)
    print(list1) # ['1', '2', '3', '4']
    
    -----------------------------  str--> set --------------------
    
    set1 = set(s)
    print(set1) # {'3', '4', '1', '2'}
    
    -----------------------------  str--> tuple --------------------
    tupl1 = tuple(s)
    print(tupl1) # ('1', '2', '3', '4')
    
    ```

  + `list`可转类型

    ```python
    set()  tuple() 可以转换成字典 [(key,value),()···]
    ```

  + `dict可转类型`

    ```python
    list
    ```

  + `tuple可转类型`

    ```python
    list
    ```

  + `set可转类型`

    ```python
    list
    ```

####  15. 函数

+ 函数简介

  ```python
  作用: 将重复的代码,封装到函数,只要使用直接找函数 函数可以增强代码的模块化和提高代码的重复利用率
      
  格式:
      def 函数名:
          pass
  ```

+ 拆包装包

  ```python
  装包: 把传递的参数,包装成一个集合,称之为“装包”
      
  拆包: 把集合参数,再次分解成单独的个体,称之为"拆包"
      
  # 封装一个求和函数
  def add(*args):
      sum = 0
      if len(args) > 0:
          for i in args:
              sum += i
          print(sum)
      else:
          print('没有元素可以计算')
  add()
  add(1,2,4,6,100)
  
  注意: 可变参数必须放在后面
  ```

+ 关键字参数

  ```python
  # 关键字参数
  def add(a,b=1):
      print(a+b)
  add(1,2) # 3  b=1 相当于默认值，后来的值会将其覆盖
  
  # 可变 值必须是 key=value
  def add(**args):
      pass
  
  调用函数时有 ** 叫拆包
  
  定义时有 ** 叫装包
  
  应用:
      def bb(a, b, *c, **d):
          print(a, b, c, d)
  
      bb(1, 2)  # 1 2 () {}
      bb(1, 2, 3, 4)  # 1 2 (3, 4) {}
      bb(1, 2, x=100, y=20)  # 1 2 () {'x': 100, 'y': 20}
  
  ```

+ 函数的返回值

  ```python
  return
  
  有 return 需要用变量接受
  ```

+ `global`问题

  ```python
  函数内部声明的变量,局部变量
  
  声明在函数外侧的变量是全局变量
  
  
  
  def fun():
      global name # 不修改全局变量,只是获取打印,但是如果要发生修改全局变量,则要在函数内部声明, global 变量名
      
  全局变量如果是不可变在函数中进行修改需要添加 global 关键字
  如果全局变量是可变的,在函数中修改的时候就不需要添加 global 
  ```

+ 嵌套函数

  ```python
  def func():
      # 声明变量
      n = 100  # 局部变量
      list1 = [2, 3, 45, 5]
  
      # 声明内部函数
      def inner_func():
          nonlocal n # 内部函数修改局部变量需要使用 nonlocal
          # 对 list1 的元素进行 +5 操作
          for index, i in enumerate(list1):
              list1[index] = i + n
          list1.sort()
          print(list1)  #  [102, 103, 105, 145]
      inner_func()
  func()
  
  内部函数的特点:
      1. 可以访问外部函数的变量
      2. 内部函数可以修改外部函数的可变类型的变量 比如: list1
      3. 内部函数修改全局的不可变变量时,需要在内部函数声明 global 变量名
      内部函数修改外部函数的不可变的变量时,需要在内部函数中声明； nonlocal 变量名
    	4. locals() 查看本地变量有哪些,以字典的形式输出
      globals() 可以查看全局变量有那些,以字典的形式输出(会出系统的一些键值对)
  ```

####  16. 闭包

+ 闭包的概念

  ```python
  在函数中提出的概念
  ```

+ 条件

  ```python
  1. 外部函数中定义了内部函数
  2. 外部函数是有返回值
  3. 返回值是: 内部函数域名
  4. 内部函数引用了外部函数的变量
  
  语法格式:
      def 外部函数():
          pass
      	def 内部函数():
              pass
          return 内部函数名
  ```

+ 闭包的应用

  ```python
  
  ```

+ 闭包的缺点

  ```python
  闭包的缺点: 
      1. 作用域没有那么直观
      2. 因为变量不会被垃圾回收所以有一定的内存占用问题
  ```

+ 闭包的作用

  ```python
  闭包的作用: 
      1. 可以使用同级的作用域
      2. 读取其他元素的内部变量
      3. 延长作用域
  ```

+ 闭包的总结

  ```python
  总结:
      1. 闭包似优化了变量,原来需要类对象完成工作,闭包也可以完成
      2. 由于闭包引用；额外部函数的局部变量,则外部函数的局部变量没有及时释放,消耗内存
      3. 闭包的好处,使代码变得简洁,便于阅读代码
      4. 闭包是理解装饰器的基础
  ```

####  17. 装饰器(重点)

+ 装饰器

  ```python
  特点: 
      1. 函数 A 是作为参数出现的(函数B就会接受函数A作为参数)
      2. 要有闭包的特点
  ```

  ```python
  
  # 定义一个装饰器 (含有闭包特点)
  def decorate(func):
      a = 100
  
      def wrapper():
          print('----------------------> 内部函数 输出')
          func()
          print('----------------------- 111111111111112222222222222', a)
      return wrapper
  
  # 使用装饰器
  @decorate
  def house():
      print('我是毛坯房······················')
  
  # 调用函数
  house()
  
  ```

+ 带参数的装饰器

  ```python
  *args,**kwargs 作为参数传递
  
  
  如果装饰器是多层的,谁距离函数最近就优先使用那个装饰器
  ```

####  18. 匿名函数

```python
def add(a,b):
    return a+b
f = add

s = lambda a,b:a+b

result = s(1,2)
```

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210104145533.png">

+ 匿名函数作为参数

  ```python
  
  ```

+ `map()`

  ```python
  list1 = [1,4,7,6]
  result = map(lambda x:x if x%2==0 eldr x+1,list1)
  print(list(result))
  ```

+ `reduce()`

  ```python
  对列表中的元素进行加减乘除运算的函数
  ```

+ `filter()`

  ```python
  # 过滤出 大于 10 的数子
  list1 = [10, 20, 2, 3, 4, 6, 19]
  result = filter(lambda x: x > 10, list1)
  print(list(result))
  ```

+ 递归函数

  ```python
  普通函数: def func(): pass
  匿名函数: lambda 参数: 返回结果
  递归函数: 普通函数的一种表现形式
  ```

###  文件操作

+ 文件操作

  + 文件读取

    ```python
    import os
    # 以 txt 文件练习  其他读取 有 gbk 错误
    # 读取路径 print(os.getcwd()) D:\python就业视频\python基础
    stream = open(r'D:\python就业视频\python基础\hello.txt')
    container = stream.read()
    txt = stream.readable()  # 判断文件是否可读  True
    readLine = stream.readline()  # 读取一行
    lines = stream.readlines()  # 读取多行
    print(container, txt, readLine)
    ```

+ 文件写入

  ```python
  # mode = 'a' 
  stream = open(r'D:\python就业视频\python基础\hello.txt', 'w')
  print(stream.write('aaaaaaaaaaaaaaaa'))  # 覆盖源文件
  
  print(stream.writelines(str)) # 保留源文件 追加
  
  ```

+ 文件复制

  ```python
  with open(r'D:\python就业视频\python基础\hello.txt') as stream:
      container = stream.read()  # 读取文件
      with open(r'D:\python就业视频\hello.txt', 'w') as writeFile:
          writeFile.write(container)
          print('文件写入')
  ```

+ `os`模块

  ```python
  # 路径读取
  ```

###  异常机制

+ 异常

  ```python
  try:
      可能出现异常的代码
  except 类型1:
      如果有异常执行的代码
  except 类型1:
      如果有异常执行的代码
  ···
  finally:
      无论是否存在异常都会执行的代码
  ```

+ `try-except-else`结构:

  ```python
  
  ```

+ `try-finally`结构:

  ```python
  
  ```

+ 抛出异常(`126集`)

  ```python
  # 抛出异常
  def refister():
      username = input('请输入用户名: ')
      if len(username) < 6:
          raise Exception('我是抛出的异常···')
      else:
          print('输入的用户名是: ' + username)
  # 接受异常
  try:
      refister()
  except Exception as err:
      print(err)
      print('注册失败')
  else:
      print('注册成功')
  
  ```

###  列表推导式(`128集`)

+ 列表推导式

  + `[表达式 for 变量 in 旧列表] `

    ```python
    
    ```

  + `[表达式 for 变量 in 旧列表 if 条件]`

    ```python
    
    list1 = [10, 2, 4, 6, 90, 30, 60]
    # 取出 大于 10的数
    newList = [i for i in list1 if i >= 10]
    print(newList)
    ```

  + `if else`

    ```python
    dict1 = {'name': 'tom', 'salary': 5000}
    dict2 = {'name': 'lucy', 'salary': 8000}
    dict3 = {'name': 'jack', 'salary': 4500}
    dict4 = {'name': 'lily', 'salary': 3000}
    
    # if 薪资大于 5000 加 200,低于 5000 加 500
    
    newList = [person['salary'] + 200 if person['salary'] > 5000 else person['salary'] + 500 for person in list1]
    print(newList) # [5500, 8200, 5000, 3500] 
    ```

+ 字典推导式

  ```python
  # 集合推导式
  list1 = [1, 2, 1, 2, 3, 4, 5, 6, 4]
  set1 = {x for x in list1}
  print(set1) # {1, 2, 3, 4, 5, 6}
  ```

+ 集合推导式

  ```python
  dict1 = {'a': 'A', 'b': 'B'}
  newdict = {value: key for key, value in dict1.items()}
  print(newdict) # {'A': 'a', 'B': 'b'}
  ```

###  生成器

```python
在 python 中,这种一边循环一边计算的机制,称为生成器: generator

得到生成器的方式:
    1. 列表推导式
    2. 借助函数完成 (yield)
    
    注意: 只要函数中出现；了 yield 关键字,说明函数就不是函数,就是生成器
```



```python

步骤:
    1. 定义一个函数,函数中使用 yield 关键字
    2. 调用函数,接受调用的结果
    3. 得到的结果就是生成器
    4. 借助于 next()
    
---------------------------------------------------------------------------------

def fun():
    n = 0
    while True:
        n += 1
        yield n
g =  fun()
# next()  __next__()
print(next(g))
```

###  面向对象

+ 面向对象

  ```python
  
  ```

+ 类

  ```python
  class 类名[(父类)]:
      属性: 特征
      方法: 动作
  ```

+ 构造器

  ```python
  
  ```

+ 对象方法

  ```python
  
  class Phone:
      def call(self):
          print('call············')
          
          
  phone = Phone()
  # 通过对象调用的方法
  phone.call()
  ```

+ 类方法

  ```python
  特点: 
      1. 定义需要依赖装饰器 @classmethod
      2. 类方法中参数不是一个对象,而是类
      3. 类方法中只可以使用类属性
      4. 类方法中是否使用普通方法? 不能
  类方法的作用:
      因为只能访问类属性和类方法,所以可以在对象创建之前,如果需要完成一些动作(功能)
  
  class Dog:
      def __index__(self,nikename):
          self.nikename = nikename
      def run(self):
          print('{}在院子里跑来跑去'.format(self.nikename))
      def eat(self):
          print('吃饭饭····')
         # self.run() # 类中方法的调用 需要通过 self.方法名()
      @classmethod
      def test(cls):
          print('cls')
  ```

+ 静态方法

  ```python
  
  ```


+ 魔术方法(参考资料:<a href="https://www.cnblogs.com/zhangboblogs/p/7860929.html">Python常用魔术方法</a>)

  + 魔术方法是什么

    ```python
    魔术方法就是一个类/对象中的方法，和普通方法唯一的不同时，普通方法需要调用！而魔术方法是在特定时刻自动触发。
    ```

  + `__init__`

    ```python
    初始化魔术方法
    
    触发时机：初始化对象时触发（不是实例化触发，但是和实例化在一个操作中）
    ```

  + `__str__`

    ```python
    # 单纯打印对象名称,出来的是一个地址,地址对于开发者来说没有太大意义
    
    # 如果想在打印对象名的时候能够给开发者更多一些信息量
    
    Eg.
    
    class Person:
        def __init__(self, nickname, age):
            self.nickname = nickname
            self.age = age
    
        def __str__(self):
            return '姓名是: ' + self.nickname + ',年龄是: ' + str(self.age)
    
    
    person = Person('Bin', 18)
    print(person) # 姓名是: Bin,年龄是: 18
    
    ```

    ```python
    _str__
    触发时机: 使用 print(对象) 或者 str(对象) 的时候触发
    参数: 一个self接收对象
    返回值: 必须是字符串类型
    作用: print（对象时）进行操作，得到字符串，通常用于快捷操作
    注意: 无
    ```

  + `__new__`(向内存要空间--> 地址)

    ```python
    实例化魔术方法
    触发时机: 在实例化对象时触发
    参数: 至少一个 cls 接收当前类
    返回值: 必须返回一个对象实例
    作用: 实例化对象
    注意: 实例化对象是 Object 类底层实现，其他类继承了 Object 的 __new__ 才能够实现实例化对象。
    
    没事别碰这个魔术方法，先触发 __new__ 才会触发 __init__
    
    ```

  + `__call_`

    ```python
    
    调用对象的魔术方法
    触发时机: 将对象当作函数调用时触发 对象() 
    参数: 至少一个self接收对象，其余根据调用时参数决定
    返回值: 根据情况而定
    作用: 可以将复杂的步骤进行合并操作，减少调用的步骤，方便使用
    注意: 无
        
    ```

+ 知识补充

  ```python
  1. 对象赋值
      p = Person()
      p1 = p
      说明: p 和 p1 共同指向同一个地址
  ```

  ```python
  2. 删除地址的引用
  	
      del p1 删除 p1 对地址的引用
  ```

  ```python
  3. 查看对地址的引用次数
      
      import sys
      sys.getrefcount(对象名)
  ```

  ```python
  4. 当一块空间没有了任何引用,默认执行 __del__
  
  ref = 0
  ```

  

+  总结魔术方法

  ```python
  重点: __init__ , __str__
      
  了解:
      __new__ 作用: 开辟空间
      __del__ 作用: 没有指针引用的时候会调用,99%都不需要重写
      __call__ 作用: 想不想将对象当成函数使用
          
  ```

  

+ 私有化

  ```python
  私有化
  
  封装: 
      1. 私有化属性
      2. 定义公有 set 和 get 方法
      
  _ _属性: 就是将属性私有化
      
  ```

  ```python
  class Person:
      def __init__(self, name, age):
          self.__name = name
          self.__age = age
  
      def setName(self, name):
          if len(name) > 0 and len(name) <= 6:
              self.__name = name
          else:
              print('名字必须是 6 位')
  
      def getName(self, name):
          return self.__name
  
      def __str__(self):
          return '姓名:{},年龄是:{}'.format(self.__name, self.__age)
  
  
  person = Person('Bin', 18)
  # 修改
  person.setName('asasa')
  print(person)
  
  ```

+ `@property`装饰器

  ```python
  ···
  ```

+ 关联关系(以后补充)

  ```python
  ····
  ```

+ 继承

  ```python
  class fu:
      pass
  class zi-1(fu):
      pass
  class zi-2(fu):
      pass
  
  注意: 可以重写 __init__
  ```

  ```python
  super().__init__() # 调用父类的 __init__
  ```

  + 继承案例练习

    ```python
    编写一个简单的工资管理程序,系统可以管理以下四类人,工人(worker)，销售员(salesman),经理(manager)销售经理(salemanager)所有的员工都具有工号,姓名,工资等属性,有设置姓名,获取姓名,获取员工号,计算工资等
    
    1. 工人: 工人具有工作小时数和时薪的属性,工资计算方法为工作小时数 * 时薪
    2. 销售员: 具有销售额和提成比例的属性,工资计算方法为销售额 * 提成比例
    3. 经理: 具有固定月薪的属性,工资计算方法为固定月薪
    4. 销售经理: 工资计算方法为销售额 * 提成比例 + 固定月薪
        
        请根据以上要求设计合理的类,完成一下功能:
            1. 添加所有类型的人员
            2. 计算月薪
            3. 显示所有人工工资情况
        
    ```

    ```python
    
    python 有多继承的特点
    
    ```

+ 多态

  ```python
  
  ```

+ 单例模式

  ```python
  
  ```


+ 实现单例有几种模式

  ```python
  
  ```

###  模块

+ 模块的导入

  ```python
  在 python 中,模块是代码组织中的一种方式,把功能相近的函数或者类放到一个文件中,一个文件(.py)就是一个模块(model)
  
  模块名就是文件名去掉后缀 py，
  
  好处:
      - 提高代码的可复用,可维护性,一个模块编写完毕后,可以很方便的在其他项目中导入
      - 解决了命名冲突,不同模块中相同的命名不会冲突
  ```

+ 导入模块的方式

  ```python
  1. import 模块名(文件名 去除后缀)
  2. from name import fun_name,变量名,类名
  3. from 模块名 import * (该模块中的所有内容)
     但是如果像限制获取的内容,可以在模块中使用 __all__ =[]
      
      注意: 无论是 import 还是 from 的形式,都会将模块内容进行加载
          如果不希望其进行调用,就会用到 __name__
          在自己的模块里面 __name__ 叫:  __main__
          如果在其他模块中通过导入的方式调用的话叫: __name__ : 模块名
          if __name__ == '__main__':
  			pass
  ```

+ 导包

  ```python
  from 包名.模块名 import 类名，变量名,函数名
  ```

+ `sys`

  ```python
  
  ```

+ `time`

  ```python
  import time
  
  -----------------------------------  重点 -----------------------------
  # 时间戳
  print(time.time())
  
  # 延迟
  time.sleep(3)
  
  # 将元组的时间转成字符串
  s = time.strftime('%Y-%m-%d')
  print(s)
  
  ----------------------------------------------------------------------
  
  t = time.time()
  print(t) # 1609993679.9369621
  
  # 将时间戳转换成字符串
  print(time.ctime(t)) # Thu Jan  7 12:27:59 2021
  
  # 将时间戳转换成元组
  t = time.localtime(t)
  print(t)
  print(t.tm_yday)
  print(t.tm_hour)
  
  # 将元组的转换成时间戳
  print(time.mktime(t))
  
  
  ```

+ `random`

  + 小数
  
    ```python
    import random
    # 随机小数
      r = random.random()
      print(r)
    ```
  
  + 前 10 位随机数，奇数位
  
    ```python
    前 10 位随机数  # 奇数 1--> 起始值 10--> 终点值 2--> 步进值
      ran = random.randrange(1, 10, 2)
      print(ran)
    ```
  
  + 前 10 位随机数整数
  
    ```python
      # 随机整数
      ran = random.randint(1, 10)
      print(ran)
    ```
  
  + 随机选择
  
    ```python
      # 随机选择
      list1 = ['a', 'b', 'c', 'd']
      ran = random.choice(list1)
      print(ran)
    ```
  
  + 打乱顺序
  
    ```python
      # 打乱顺序
      pai = ['红梅 A','方片K','黑2']
      ran = random.shuffle(pai)
      print(pai) # 输出原列表
    ```
  
  + 小应用: 验证码功能
  
    ```python
    # 验证码案例
      def fun():
          code = ''
          for i in range(4):
              # 随机整数
              ranNum = str(random.randint(0, 9))
              # A-Z
              ranUpperStr = chr(random.randint(65, 90))
              # a-z
              ranLowerStr = chr(random.randint(97, 122))
              # 存放大小写组合
              ranList = [ranNum, ranUpperStr, ranLowerStr]
              # 随机选择
              rChoice = random.choice(ranList)
              # 拼接得到最终组合
              code += rChoice
          return code
      
      # 函数调用
      code = fun()
      # 输出
      print(code)
    ```
+ `hashlib`加密模块

  ```python
  print('--------------------- content: 2021-01-11 ------------------------')
  
  # 加密算法
  print('--------------------- Md5 ------------------------')
  pwd = '123456'
  # md5 不可逆 --> 单向
  md5 = hashlib.md5(pwd.encode('utf-8'))
  # 16 进制加密
  print(md5.hexdigest())  # e10adc3949ba59abbe56e057f20f883e
  
  print('------------------------- sha1 ----------------------------------')
  sha1 = hashlib.sha1(pwd.encode('utf-8'))
  # sha1 加密
  print(sha1.hexdigest())  # 7c4a8d09ca3762af61e59520943dc26494f8941b
  
  print('------------------------- sha256 ----------------------------------')
  sha256 = hashlib.sha256(pwd.encode('utf-8'))
  # sha1 加密
  print(sha256.hexdigest())  # 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
  
  ```

  + 小案例: 登录注册

    ```python
    
    # 登录注册
    str = '123456'
    # encode
    str_en = hashlib.sha256(str.encode('utf-8'))
    # 加密
    str_pwd = str_en.hexdigest()
    
    str_list = []
    str_list.append(str_pwd)
    
    # 用户输入密码加密之后进行对比
    user_input = input('请输入密码: ')
    user_sha256 = hashlib.sha256(user_input.encode('utf-8'))
    sha256_pwd = user_sha256.hexdigest()
    
    for i in str_list:
        if sha256_pwd == i:
            print('登录成功!',i)
        else:
            print('请重新输入···')  
    ```

+ `Unicode`之间的转换

  ```python
  # chr  ord
  print(chr(65))  # Unicode --> str
  print(ord('A')) # str --> Unicode
  ```

+ 第三方`pillow`

  ```python
  pip install pillow
  ```

###  正则表达式

+ 正则表达式的定义

  ```python
  正则表达式是对字符串的一种逻辑公式,就是用事先定义好的一些特殊字符,以及这些特殊字符组成规则的字符串
  正则表达式是对字符串和特殊字符操作的一种逻辑公式
  ```

+ 正则表达式的作用和特点

  ```python
  给定一个正则表达式和另一个字符串,达到一定目的
  
  1. 给定的字符串是否符合正则表达式的过滤逻辑(称作匹配)
  
  2. 可以通过正则表达式,从字符串中获取我们想要的特定部分
  
  正则表达式的特点是:
      1. 灵活性,逻辑性和功能性非常强
      2. 可以迅速的用极简单的方式达到字符串的复杂控制
    
  ```

+ 方法

  ```python
  # 使用正则 re 模块的方法: match 从头开始匹配,如果不成功则就返回 None
  
  # 使用正则 re 模块的方法: search  进行正则字符串匹配方法,匹配的是整个字符串 输出索引位置
  
  # group()
  
  # sub(’正则表达式‘,'新内容','替换')
  
  # split() 切割
  ```

  + `re.match`与`re.search`的区别

    ```python
    
    re.match 只匹配字符串的开始，如果字符串开始不符合正则表达式，则匹配失败，函数返回 None，
    
    re.search 匹配整个字符串，直到找到一个匹配。
    
    ```

  + 检索和替换

    ```python
    re 模块提供了 re.sub 用于替换字符串中的匹配项
    
    # 语法
    	
        re.sub(pattern, repl, string, count=0, flags=0)
    
        pattern : 正则中的模式字符串。
        repl : 替换的字符串，也可为一个函数。
        string : 要被查找替换的原始字符串。
        count : 模式匹配后替换的最大次数，默认 0 表示替换所有的匹配。
        flags : 编译时用的匹配模式，数字形式。
    ```

  + `compile`函数

    ```python
    compile 函数用于编译正则表达式，生成一个正则表达式（ Pattern ）对象，供 match() 和 search() 这两个函数使用。
    ```

  + `findall`:

    ```python
    在字符串中找到正则表达式所匹配的所有子串，并返回一个列表，如果没有找到匹配的，则返回空列表。
    
    注意: match 和 search 是匹配一次 findall 匹配所有。
    ```

  + `split`

    ```python
    split 方法按照能够匹配的子串将字符串分割后返回列表
    ```

+ 正则预定义

  ```python
  \A: 表示从字符串的开始处匹配
  \Z: 表示从字符串的结束处匹配，如果存在换行，只匹配到换行前的结束字符串。
  \b: 匹配-一个单词边界，也就是指单词和空格间的位置。例如，’py\b' 可以匹配’ python” 中的’ py’，但不能匹配”oenpyx1"中的 'py'
  \B: 匹配非单词边界。’ py\b’可以匹配”openpyx1"中的’ py'，但不能匹配”python"中的’ py'
  \d: 匹配任意数字，等价于[0-9] 。
  \D: 匹配任意非数字字符，等价于[ \d]。
  \s: 匹配任意空白字符，等价于[\t\n\r\f] 
  \S: 匹配任意非空白字符，等价于[^\s]。
  \w: 匹配任意字母数字及下划线，等价于[a-zA-Z0-9_ ] 
  \W: 匹配任意非字母数字及下划线，等价于[^ \w]
  \\: 匹配原义的反斜杠\
  ```

+ 总结

  ```python
  . 任意字符除(\n)
  ^ 开头
  $ 结尾
  [] 范围
  
  量词:
      * >= 0
      + >= 1
  	? 0,1
      {m}  =m 位
      {m,} >=m
      {m,n} phone>=m  phone<=n(范围内的大小)
      
  
  ```

+ 起名

  ```python
  起名方式: (?P<name>正则)
      
  分组: ()
      
      分组可以使用 group(n组) 获取
  ```

+ `group`小应用

  ```python
  path = '''<img data-original="http://browser9.qhimg.com/bdm/768_474_0/t010448c46c1ecf7cab.jpg" alt="卡通人物 动漫卡通" title="关键字：卡通人物 动漫卡通" data-realurl="http://browser9.qhimg.com/bdr/__85/t010448c46c1ecf7cab.jpg" src="http://browser9.qhimg.com/bdm/768_474_0/t010448c46c1ecf7cab.jpg" style="display: inline;">
  '''
  result = re.match(r'<img data-original="http://browser9.qhimg.com/bdm/768_474_0/t010448c46c1ecf7cab.jpg" alt="卡通人物 动漫卡通" title="关键字：卡通人物 动漫卡通" data-realurl="http://browser9.qhimg.com/bdr/__85/t010448c46c1ecf7cab.jpg" src="(.*?)"',path)
  print(result.group(1)) # http://browser9.qhimg.com/bdm/768_474_0/t010448c46c1ecf7cab.jpg
  ```

###  进程（实现快速执行某任务,不论顺序）

+ 进程概念

  ```python
  进程是操作系统分配资源的最小单元···
  
  线程是操作系统调度的最小单元···
  ```

+ 创建进程

  ```python
  from multiprocessing import Process
  import os
  from time import sleep
  
  
  def task1(timer, name):
      while True:
          sleep(timer)
          print(os.getpid(), '--------------------> ', os.getppid())
          print('{}'.format(name))
  
  
  def task2(timer, name):
      while True:
          sleep(timer)
          print(os.getpid(), '--------------------> ', os.getppid())
          print('{}'.format(name))
  
  
  if __name__ == '__main__':
      print('主进程···········')
  
      # 子进程
      p1 = Process(target=task1, args=(1, 'p1'), name='任务一')
      print(p1.name)
      p1.start()
  
      p2 = Process(target=task2, args=(2, 'p2'), name='任务二')
      print(p2.name)
      p2.start()
  
  ```

  ```python
  '''
  总结:
      process.start() 启动进程并执行任务
      process.run() 只是执行了任务但没有启动进程
      terminate() 终止
  '''
  
  主进程:  # (解释器的 run )
   
  子进程: 
  ```

+ 终止进程

  ```python
  # 全局变量
  # 进程练习源码 2021-01-11
  from multiprocessing import Process
  import os
  from time import sleep
  
  
  def task1(timer, name):
      while True:
          sleep(timer)
          print(os.getpid(), '--------------------> ', os.getppid())
          print('{}'.format(name))
  
  
  def task2(timer, name):
      while True:
          sleep(timer)
          print(os.getpid(), '--------------------> ', os.getppid())
          print('{}'.format(name))
  
  
  # 全局变量
  number = 1
  
  if __name__ == '__main__':
      print('主进程···········', os.getpid())
  
      # 子进程
      p1 = Process(target=task1, args=(1, 'p1'), name='任务一')
      print(p1.name)
      p1.start()
  
      p2 = Process(target=task2, args=(2, 'p2'), name='任务二')
      print(p2.name)
      p2.start()
  
      while True:
          number += 1
          sleep(0.2)
          if number == 10:
              # 终止进程
              p1.terminate()
              p2.terminate()
              break
          else:
              print('number: ', number)
  
  ```

  

+ 全局变量

  ```python
  
  多进程对于全局变量访问,在每一个全局变量里面都放一个 m 变量
  
  保证每个进程访问变量互不干扰
  
  ```

+ 非阻塞式进程池

  ```python
  '''
      当需要创建的子进程数量不多时,可以直接利用 multiprocessing 中的 Process 动态生成多个进程
      但如果是上百甚至上千个目标,手动的的去创建进程的工作量巨大,此时就可以用到 multiprocessing 模块提供的 Pool 方法
      初始化 Pool 时,可以指定一个最大进程数,当有新的请求提交到 Pool 时,如果池还没有满,那么就会创建一个新的进程来执行该请求,但
      如果池中的进程数已经达到指定的最大值,那么该请就就会等待,直到池中有进程结束,才会创建新的进程来执行
  
      非阻塞式: 全部添加到队列中,立刻返回,并没有等待其他的进程完毕,但是回调函数是等待任务完成后才调用
      阻塞式: 区别在 apply()  apply_async() 
  '''
  ```

  

  ```python
  # 进程池
  
  from multiprocessing import Pool
  import os
  import time
  import random
  
  
  def task_fun(task_name):
      print('任务开始啦·············', task_name, os.getpid())
      # 获取时间戳
      start = time.time()
      # 使用 sleep
      time.sleep(3)
      end = time.time()
      print('用时: {}'.format(start - end))
      # 需要 return
      return '用时: {}'.format(start - end)
  
  
  def callback_fun(n):
      # 必须添加参数
      container_list.append(n)
  
  
  container_list = []
  
  if __name__ == '__main__':
      # 创建进程池 开启 5 个子进程
      pool = Pool(5)
      '''
      源码,Pool 中的参数: 
      def Pool(processes: Optional[int] = ..., # 最大进程数 整数类型
               initializer: Optional[Callable[..., Any]] = ...,
               initargs: Iterable[Any] = ...,
               maxtasksperchild: Optional[int] = ...) -> pool.Pool: ...
      '''
      list = ['1a', '2a', '3a', '4a', '5a', '6a', '7a', '8a']
      for task in list:
          # 非阻塞式
          pool.apply_async(task_fun, args=(task,), callback=callback_fun)
      pool.close()  # 添加任务结束
      pool.join()  # 堵住主进程 插队，不会执行后续 over,会等待 子进程执行完毕··········
  
      # 主进程任务
      for i in container_list:
          print(i)
  
  ```

+ 阻塞式进程池

  ```python
  特点: 添加一个执行一个任务,如果一个任务不结束另一个任务就进不来
  ```

+ 进程间的通信

  ```python
  # 进程通信
  # 通信是通过同一个 args=(参数1,···)
  from multiprocessing import Process, Queue
  from time import sleep
  
  
  def download(q):
      imglist = ['a.jpg', 'b.jpg', 'c.jpg', 'd.jpg', 'e.jpg']
      for img in imglist:
          print('正在下载: ', img)
          sleep(0.5)
          # 放入
          q.put(img)
  
  
  def getfile(q):
      while True:
          try:
              # 获取
              file = q.get(timeout=5)
              print('{} 保存成功'.format(file))
          except:
              print('全部保存完毕·········')
              break
  
  
  if __name__ == '__main__':
      # 通信桥梁
      q = Queue(5)
  
      down = Process(target=download, args=(q,))
      gets = Process(target=getfile, args=(q,))
      # 创建进程
      down.start()
      # down 阻塞
      down.join()
  
      gets.start()
      gets.join()
  
  ```

###  线程

+ 线程的概念

  ```python
  '''
  
  线程: 有时被称为轻量进程(Lightweight Process LWP)，是程序执行流的最小单位。一个标准的线程由线程ID，当前指令指针(PC) 寄存器集合和堆栈组成,另外,线程是进程中的一个实体,是被系统独立调度和分排的基本单位，线程自己不拥有系统资源,只拥有一点儿在运行中必不可少的资源,但它可与同属一个进程的其他线程共享进程所拥有的全部资源.
  
  一个线程可以创建和撤销另一个线程,同一个进程中的多个线程之间可以并发执行。由于线程之间的相互制约,致使线程在运行中呈现出间断性。线程也有就绪，阻塞和运行三种基本状态。
  
  就绪状态: 是指线程具备运行的所有条件m逻辑上可以运行,在等待处理机；
  
  运行状态: 是指线程占有处理机正在运行
  
  阻塞状态: 阻塞状态是指线程在等待一个事件(如某个信号量),逻辑上不可执行。每一个程序都至少有一个线程，若程序只有一个线程,那就是程序本身。
  
  '''
  ```

+ 多线程

  ```python
  '''
  
  线程是程序中一个单一的顺序控制流程。
  
  程序内有一个相对独立的、可调度的执行单元.是系统独立调度和分派 CPU 的基本单位指令运行时的程序的调度单位。在单个程序中同时运行
  多个线程完成不同的工作称为多线程
  
  
  多线程: 多线程(multithreading) 是指从软件或者硬件上实现多个线程并发执行的技术。具有多线程能力的计算机因有硬件支持而能够
  在同一时间执行多于一个线程,进而提升整体处理性能.具有这种能力的系统包括多对处理机,多核心处理器以及芯片级多处理或同时多线处理器。
  在一个程序中,这些独立运行的程序片段就做 "线程"，利用它的编程的概念就叫做"多线程处理".
  
  '''
  ```

+ 优点

  + 使用线程可以把占据很长时间的程序中的任务放到后台去处理
  + 用户界面可以更加吸引人,这样比如用户点击了一个按钮去触发某些事件的处理,可以弹出一个进度条
  来显示用户处理的进度
  + 程序的运行速度可能加快
  + 在一些等待的任务实现上如用户输入，文件读写和网络收发数据等,线程就比较有用了.这种情况下我们可以释放一些
  珍贵的资源如内存占用等等

  

+ 线程的状态

  ```bash
  新建 就绪  运行  阻塞  结束
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/threadg.png">

+ 全局解释器锁

  ```python
  '''
  
  Global Interpreter Lock,缩写 GIL 是计算机程序设计语言解释器用于同步线程的一种机制，它使得任何时刻仅有一个线程在执行。即
  
  便在多核心处理器上，使用 GIL 的解释器也只允许同一时间执行一个线程。常见的使用 GIL 的解释器有CPython与Ruby MRI。
  
  '''
  ```

  ```bash
  线程用于: 耗时操作,爬虫 IO
  
  进程用于: 计算密集型
  ```

+ 多线程同步

  ```python
  数据共享:
      如果多个线程共同对某个数据修改，则可能出现不可预料的结果,为了保证数据的正确性,需要对多个线程进行同步
      
  同步: 一个一个的完成,一个1做完另一个才能进来
      效率会降低
      
      使用 Thread 对象的 Lock 和 RLock 可以实现简单的线程同步,这个对象都有 acquire 方法 和 release方法,对于那些需要每次
      只允许一个线程操作的数据,可以将其操作放在 acquire 和 release 方法之间
      
      多线程的优势在于可以同时运行多个任务。但是当线程需要共享数据时,可能存在数据不同步的问题,为了避免这种情况,引入锁的概念
  ```

  ```python
  
  import threading
  from time import sleep
  import random
  
  # 锁对象
  lock = threading.Lock()
  
  # 可变类型
  list1 = [0] * 10  # [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
  
  # --------------------------------- S: 加锁任务 ----------------------------------------------
  def task1():
      # 获取线程锁,如果已经上锁,则等待锁的释放
      lock.acquire()  # 阻塞
      # 任务
      for i in range(len(list1)):
          list1[i] = 1
          sleep(0.5)
      lock.release()  # 释放锁
  
  
  def task2():
      lock.acquire()  # 阻塞
      for i in range(len(list1)):
          print('--------------> ', i)
          sleep(0.5)
      lock.release()  # 释放锁
  
  
  if __name__ == '__main__':
      # 创建线程
      th1 = threading.Thread(target=task1)
      th2 = threading.Thread(target=task2)
  
      # 开启线程
      th2.start()
      th1.start()
  
      # 阻塞
      th2.join()
      th1.join()
  
      print(list1)
  # --------------------------------- E: 加锁任务 ----------------------------------------------
  
  ```

  

+ 死锁

  ```python
  # 死锁
  
  '''
    开发过程中，在线程间共享多个资源的时候,如果两个线程分别占有一部分资源并且同时等待对方的资源，就会造成死锁.
    尽管死锁很少发生,但一旦发生就会造成应用的停止响应,程序不做任何事情
  
    避免死锁
    解决:
        1. 重构代码
        2. 使用 timeout 参数
    '''
    from threading import Thread, Lock
    from time import sleep
  
  # -------------------------------------------------------- S: 死锁 --------------------------------------
  
    # 准备两把锁
  
    lockA = Lock()
    lockB = Lock()
  
  
    # 自定义线程
  
    class MyThreadA(Thread):
        def run(self):  # start()
            #  源码: def acquire(self, blocking: bool = ..., timeout: float = ...) -> bool: ...
            if lockA.acquire():  # 如果可以获取锁则返回 True (源码可知)
                print(self.name + '拿到了A锁')
                sleep(0.1)
                if lockB.acquire():
                    print(self.name + '又获取了B锁,原来还有A锁')
                    lockB.release()  # 释放 B 锁
                lockA.release()  # 释放 A 锁
  
  
    class MyThreadB(Thread):
        def run(self):  # start()
            #  源码: def acquire(self, blocking: bool = ..., timeout: float = ...) -> bool: ...
            if lockB.acquire():  # 如果可以获取锁则返回 True (源码可知)
                print(self.name + '拿到了B锁')
                sleep(0.1)
                if lockA.acquire():
                    print(self.name + '又获取了A锁,原来还有B锁')
                    lockA.release()  # 释放 B 锁
                lockB.release()  # 释放 A 锁
  
    if __name__ == '__main__':
        th1 = MyThreadA()
        th2 = MyThreadB()
        th1.start()
        th2.start()
      
  # -------------------------------------------------------- E: 死锁 --------------------------------------
  ```
  
    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/dblock.png" width="400" height="120">
  
+ 解决死锁

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/reblock.png" width="600" height="300" alt="python 死锁 全局解释器锁">

+ 生产者与消费者(线程之间的通信)

  ```python
  
    '''
    生产者与消费者: 两个线程之间的通信
    
    python 的 queue 模块中提供了同步的,包括 FIFO(先进先出)队列 Queue
    
    LIFO(后入先出) 队列 LifoQueue 和优先级队列 PriorityQueue。这些队列都实现了锁原语(可以理解为原子操作，即要么不做,要么就全做),能够在多线程中直接使用
    
    可以使用队列来实现线程间的同步
    
    '''
  ```

  ```python
  import queue
    import threading
    import random
    from time import sleep
    
    
    def produce(q):
        i = 0
        while i < 10:
            num = random.randint(1, 100)
            q.put('生产者产生的数据: %d' % num)
            print('生产者产生的数据: %d' % num)
            sleep(1)
            i += 1
        q.put(None)
        # 完成任务
        q.task_done()  # task_done() 源码附有
    
    
    def consume(q):
        while True:
            item = q.get()
            if item is None:
                break
            print('消费者获取到: %s' % item)
            sleep(4)
        # 完成任务
        q.task_done()
    
    
    if __name__ == '__main__':
        q = queue.Queue(10)
        arr = []
    
        # 创建生产者
        th1 = threading.Thread(target=produce, args=(q,))
        th1.start()
    
        # 创建消费者
        th2 = threading.Thread(target=consume, args=(q,))
        th2.start()
    
        th1.join()
        th2.join()
    
        print('END···············')
  ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/Threadqueue.png" width="600" height="500" alt="线程 生产者与消费者 python">

+ 数据共享总结

  ```python
  进程共享数据与线程共享数据的区别:
      进程是每个进程中都有一份
      线程是共同一个数据 --> 数据安全问题
      
      GIL --> 伪线程
      
  ```

+ 协程

  + 使用生成器创建协程

    ```python
    # Coroutine 协程
    
    '''
    协程: 耗时操作
    
    耗时操作: 网络请求 网络下载(爬虫), IO：文件的读写 阻塞
    
    '''
    from time import sleep
    
    def task1():
        for i in range(3):
            print('A'+str(i))
            yield
            sleep(1)
    
    def task2():
        for i in range(3):
            print('B' + str(i))
            yield
            sleep(2)
    
    if __name__ == '__main__':
        # 生成器
        t1 = task1()
        t2 = task2()
    
        while True:
            try:
                next(t1)
                next(t2)
            except:
                break
    
    ```

  + 第三方`greenlet`创建协程

    ```python
    # greenlet
    
    ```
    
    ```python
    # 进入  anaconda 安装的 Scripts下
    
      conda: conda install greenlet 
    
      windows: pip/pip3 install greenlet
    ```
    
    ```python
     from greenlet import greenlet
      import time
    
    
      def a():
          for i in range(5):
              print('A' + str(i))
              gb.switch()
              time.sleep(0.1)
    
    
      def b():
          for i in range(5):
              print('B' + str(i))
              gc.switch()
              time.sleep(0.2)
    
    
      def c():
          for i in range(5):
              print('C' + str(i))
              ga.switch()
              time.sleep(0.3)
    
    
      if __name__ == '__main__':
          ga = greenlet(a)
          gb = greenlet(b)
          gc = greenlet(c)
          # 需要调一下
          ga.switch()
    
      '''
    
      结果输出: A0 B0 C0 A1 B1 C1 A2 B2 C2 A3 B3 C3 A4 B4 C4
    
      交替输出
    
      '''
  ```
  
+ 第三方`gevent`
  
    ```python
   
   	'''
    	  conda解释器安装 gevent:
        
        conda install gevent
        
        成功后显示:  All requested packages already installed.
  
        全局解释器安装: pip/pip3 install gevent
    
    '''
     
    greenlet已经实现了协程，但是这个人工切换，是不是觉得太麻烦了，python 还有一个比 greenlet 更强大的并且能够自动切换任务的模块`gevent`,其原理是当一个 greentlet 遇到 IO（指的是input ouput输入输出，比如网络、文件操作等）操作时，比如访问网络，就自动切换到其他的greenlet,等到 IO 完成，再适当的时候切换回来继续执行。
    
    由于IO操作非常耗时，经常使程序处于等待状态，有了gevent我们自动切换协程，就保证总有greenlet在运行，而不是等待IO
  
  ```
  
    
  
    ```python
    
    from greenlet import greenlet
    import gevent
    import time
    
    # 猴子补丁
    from gevent import monkey
    monkey.patch_all()
    
    
    def a():
        for i in range(5):
            print('A' + str(i))
            time.sleep(0.1)
    
    
    def b():
        for i in range(5):
            print('B' + str(i))
            time.sleep(0.2)
    
    
    def c():
        for i in range(5):
            print('C' + str(i))
            time.sleep(0.3)
    
    
    if __name__ == '__main__':
        g1 = gevent.spawn(a)
        g2 = gevent.spawn(b)
        g3 = gevent.spawn(c)
    
        g1.join()
        g2.join()
        g3.join()
    
    '''
    没有猴子补丁的输出: A0 A1 A2 A3 A4 B0 B1 B2 B3 B4 C0 C1 C2 C3 C4
    
    添加猴子补丁后输出: A0 B0 C0 A1 B1 A2 C1 A3 B2 A4 B3 C2 B4 C3 C4 # 实现协程
    
  '''
  ```
  
    + <font color="red">实现协程小应用</font>
  
      ```python
      # 协程案例
      import urllib  # 错误
      import gevent
      
      '''
      erro: 由于暂时不了解爬虫,错误无法排除 
      
      date: 2021.01.13 13:40:31 
      
      python: 完结 python 基础学习
      
      '''
      
      # 猴子补丁
      from gevent import monkey
      
      monkey.patch_all()
      
      
      def downUrl(url):
          response = urllib.request.urlopen(url)
          content = response.read()
          print('下载了{} 的数据,长度是:{}'.format(url, len(content)))
      
      
      if __name__ == '__main__':
          urls = ['http://www.163.com', 'http://www.qq.com', 'http://www.baidu.com']
          g1 = gevent.spawn(downUrl, urls[0])
          g2 = gevent.spawn(downUrl, urls[1])
          g3 = gevent.spawn(downUrl, urls[2])
      
          g1.join()
          g2.join()
          g3.join()
      
      ```
  

###  PYMYSQL模块

+ 查询

  ```python
  # 输入相应参数
  import pymysql
  
  
  def main():
      conn = pymysql.connect(host = 'localhost',
                             port = 3306,
                             user = 'root',
                             passwd = 'root',
                             db = 'student',
                             charset = 'utf8',
                             cursorclass = pymysql.cursors.DictCursor)  # 修改类型 元组类型需要去除该参数
      try:
          # 获取游标对象
          with conn.cursor() as cursor:
              # 执行 sql 注意参数位置
              cursor.execute('select eno,ename,sal from tb_emp')
              # 元组类型结果集
              # for row in cursor.fetchall():
              #     print('''
              #     ----------- 查询所有 -------
              #     eno: {}
              #     ename: {}
              #     sal: {}
              #     -------------------------
              #
              #     '''.format(row[0], row[1], row[2]))
  
              # 字典类型结果集 如果查询时带别名, 那么字典的键要更改为 别名
              for row in cursor.fetchall():
                  # print(row)
                  print('''
                  -------------------------
                  eno: {}
                  ename: {}
                  sal: {}
                  --------------------------
                  '''.format(row['eno'], row['ename'], row['sal']))
      except pymysql.MySQLError as erro:
          print(erro)
      finally:
          # 关闭连接释放资源
          conn.close()
  
  
  if __name__ == '__main__':
      main()
  
  ```

+ 添加

  ```python
  # pymysql 的使用
  import pymysql
  
  
  # 生成文件 pip freeze > requirements.txt
  # 依赖项安装: pip install -r requirements.txt
  
  def main():
      conn = pymysql.connect(host = '127.0.0.1',
                             port = 3306,
                             user = 'root',
                             password = 'root',
                             db = 'student',
                             charset = 'utf8')
      try:
          # 获得游标对象
          with conn.cursor() as cursor:
              # execute 执行
              result = cursor.execute('insert into tb_emp values(1001,"张三",4500)')
              if result == 1:
                  print('添加成功')
                  # commit() 很重要 否则看不到响应结果
                  conn.commit()
              else:
                  print('添加失败，操作已经回滚···')
      except pymysql.MySQLError as error:
          print(e)
          conn.rollback()
      finally:
          conn.close()
  
  
  if __name__ == '__main__':
      a = main()
  
  ```

+ 删除

  ```python
  # 输入相应参数
  import pymysql
  
  
  def main():
      conn = pymysql.connect(host = 'localhost',
                             port = 3306,
                             user = 'root',
                             passwd = 'root',
                             db = 'student',
                             charset = 'utf8')
      eno = int(input('请输入要删除的员工编号: '))
  
      try:
          # 获取游标对象
          with conn.cursor() as cursor:
              # 执行 sql
              result = cursor.execute('delete from tb_emp where eno=%s', (eno,))
              if result == 1:
                  print('删除数据成功···')
                  conn.commit()
              else:
                  print('删除数据失败,操作已经回滚····')
      except pymysql.MySQLError as erro:
          print(erro)
          # 回滚
          conn.rollback()
      finally:
          # 关闭连接释放资源
          conn.close()
  
  
  if __name__ == '__main__':
      main()
  
  ```

+ 更新

  ```python
  # 输入相应参数
  import pymysql
  
  
  def main():
      conn = pymysql.connect(host = 'localhost',
                             port = 3306,
                             user = 'root',
                             passwd = 'root',
                             db = 'student',
                             charset = 'utf8')
      # 输入内容
      oldeno = int(input('请输入原编号: '))
      neweno = int(input('请输入新编号: '))
  
      try:
          # 获取游标对象
          with conn.cursor() as cursor:
              # 执行 sql 注意参数位置
              result = cursor.execute('update tb_emp set eno = %s where eno = %s', (neweno, oldeno))
              if result == 1:
                  print('更新数据成功···')
                  conn.commit()
              else:
                  print('更新数据失败,操作已经回滚····')
      except pymysql.MySQLError as erro:
          print(erro)
          # 回滚
          conn.rollback()
      finally:
          # 关闭连接释放资源
          conn.close()
  
  
  if __name__ == '__main__':
      main()
  
  ```

  