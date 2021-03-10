---
title: BOM-页面加载事件
password: ''
abstract: 'Something is encrypted, please enter the password to view.'
message: 'Hello, password is required here'
wrong_pass_message: 'Sorry, this password doesn''t look right, please try again.'
wrong_hash_message: >-
  Sorry, this article cannot be verified, but you can still see the decrypted
  content
tags: javascript
categories: javascript
abbrlink: 32966
date: 2020-12-01 11:13:07
top_img:
cover:
---



###  BOM-页面加载事件
<!-- more -->
```javascript
1. load 等页面内容全部加载完毕,包含页面 dom 元素 图片 flash css 等

2. DOMContentLoaded 是 DOM 加载完毕,不包含图片 flash css 等就可以执行 加载速度比 load更快一些
```



###  BOM-窗口大小事件

```javascript
    window.addEventListener('resize', function () {
            console.log('················');
        });
```

