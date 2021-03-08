---
title: JSON-序列化
tags:
  - Python
  - Json
  - JSON 序列化
categories: Python
abbrlink: 56134
date: 2021-01-06 19:38:31
top_img:
cover:
---

###  JSON-序列化

+ 在线练习`JSON`

  > <a href="https://www.json.cn//">JSON在线编译练习</a>

+ `json`序列化

  ```python
  我们把程序的各种类型数据对象 变成 表示该数据对象的字符串这个过程称之为 序列化
  
  而把字节字符串转化为 程序中的数据对象 这个过程称之为 反序列化
  ```

  ```python
  import json
  
  historyTransactions = [
  
      {
          'time': '20170101070311',  # 交易时间
          'amount': '3088',  # 交易金额
          'productid': '45454455555',  # 货号
          'productname': 'iphone7'  # 货名
      },
      {
          'time': '20170101050311',  # 交易时间
          'amount': '18',  # 交易金额
          'productid': '453455772955',  # 货号
          'productname': '奥妙洗衣液'  # 货名
      }
  ]
  # ensure_ascii=False 中文编码不会改变, indent = 4 (输出格式化一样)
  jsonStr = json.dumps(historyTransactions, ensure_ascii=False, indent=4)
  print(jsonStr)
  
  
  ```

+ 反序列化操作

  ```python
  # 反序列化操作
  print('------------------------------------')
  obj = json.loads(jsonStr)
  print(type(obj))
  print(obj)
  ```

+ 使用 `JSON`深度拷贝

  ```python
  
  ```

  

