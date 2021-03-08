---
title: Github-Gitee一台电脑同时使用配置改进
tags: git
categories: Git
cover: 'https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/sshkey.png'
abbrlink: 11357
date: 2020-12-22 20:35:03
top_img:
---

###  Github-Gitee配置改进

>  安装 `git(前面已经重复造轮子了,请自主查看主要过程)`

###  1. 清除 `git`的全局设置

```jsx
git config --global --unset user.name "Your-userName"

git config --global --unset user.email "Your-userEmail"
```

###  2. `github`生成新的 `SSH keys`

+ `github  ssh key`的创建
+ 指定文件路径(`C:/Users/用户名/.ssh/`)，具体到盘符文件夹（`~ 符号会报错`）
+ 注意 `/  与  \ 必须所有同方向`

> 执行: 
>
> ​	`ssh-keygen -t rsa -f  C:/Users/用户名/.ssh/id_rsa.github -C "email@qq.com"`
>
> ​	（个人`github`与`gitee`同邮箱）
>
> 直接回车 3 下
>
> 

###  3.  `gitee`生成新的 `SSH keys`

```jsx
ssh-keygen -t rsa -f  C:/Users/用户名/.ssh/id_rsa.gitee -C "email@qq.com"
```

###  4. 完成后会在 `C:/Users/用户名/.ssh/目录下`生成以下文件

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/sshkey.png">

###  5. 添加识别 `SSH keys `新的私钥

> 默认只读取` id_rsa`，为了让 `SSH` 识别新的私钥，需要将新的私钥加入到 `SSH agent `中

+ ` ssh-agent bash`
  + 正确形式暂时忘记
  + 错误(执行该命令: ` Set-Service -Name ssh-agent -StartupType automatic 个人在使用该命令时通过 powershell 执行`)

+ 使用自己的路径执行如下检测
  + ` ssh-add  C:/Users/爱豆/.ssh/id_rsa.github`
  + ` ssh-add  C:/Users/爱豆/.ssh/id_rsa.gitee`

###  6. 多账号必须配置 config 文件(重点)

```ruby
touch C:/Users/爱豆/.ssh/config   (config 无类型,无后缀) 
```

+ `config`内容

  ```bash
  #Default gitHub user Self
  Host github.com
      HostName github.com
      User git # 默认就是git，可以不写
      IdentityFile  # C:/Users/爱豆/.ssh/id_rsa.github (修改为你的)
  
  
  
  # gitee
  Host gitee.com
      Port 22
      HostName gitee.com
      User git
      IdentityFile  # C:/Users/爱豆/.ssh/id_rsa.gitee (修改为你的)
  
  ```

###  7.  在 `github` 和`gitee` 网站添加` ssh`

1. `github`的添加

   + 点击`github主页`右侧头像
   + 点击`settings`

   + 点击左侧导航`SSH and GPG keys`

   + 点击`New SSH Key`（绿色按钮）
   + `个人删除了之前的 key`
   + 添加 `同名文件.pub 的 key`

2. `gitee`的添加
   + 点击右侧图像
   + 点击设置
   + 点击左侧导航中的`SSH`公钥
   + `添加同名.pub`的公钥

###  8. 测试是否连接成功

+ 检测命令

  ```bash
  ssh -T git@github.com
  
  ssh -T git@gitee.com
  ```

+ 个人显示信息

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/finishKey.png" width="600" title="添加成功">

###  9. `gitee`使用

+ 不添加 `--global`

```bash
git config  user.name "Your-userName"

git config  user.email "Your-userEmail"
```

### 10. `github`个人电脑未提示任何信息直接进行了 `git`相关操作

###  来源参考: <a href="https://www.jianshu.com/p/68578d52470c">知乎</a>