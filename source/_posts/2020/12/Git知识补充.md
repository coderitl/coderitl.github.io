---
title: Git知识补充
tags: git
categories: Git
top_img: 'https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/thismerge.png'
cover: 'https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/thismerge.png'
abbrlink: 21322
date: 2020-12-26 10:53:54
---

###   git 内容补充

+ 新手推荐练习`https://learngitbranching.js.org/?locale=zh_CN`

###  git 图解

1. `git commit -m "本次提交提交日志"`

   {% folding  blue,git-commit %}

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/gitCommitS.png" title="git  commit -m'提交日志 ' " width="600">

   {%  endfolding %}

2. `git branch`

   {% tip cogs%}

   Git 的分支也非常轻量。它们只是简单地指向某个提交纪录 —— 仅此而已。所以许多 Git 爱好者传颂：

   **`早建分支！多用分支！`**

   这是因为即使创建再多的分支也不会造成储存或内存上的开销，并且按逻辑分解工作到不同的分支要比维护那些特别臃肿的分支简单多了。

   在将分支和提交记录结合起来后，我们会看到两者如何协作。现在只要记住使用分支其实就相当于在说：“我想基于这个提交以及它所有的父提交进行新的工作。”

   {% endtip %}

   

   {% tabs git-branch %}
   <!-- tab -->

   新建分支:

   ​	`git branch new-branch-name`

   ​	{% folding blue,head指向 %}

   `HEAD指向 `

    <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/thisBranch.png" title="HEAD 指向 master">

   {% endfolding %}

   切换分支:

   ​	`git checkout new-branch-name`

   ​	{% folding blue,新建并实现切换分支 %}

   + head 指向 `bugFix`

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/thisBugFix.png">

   

   ​	{% endfolding %}

   <!-- endtab -->

   <!-- tab -->
   创建并切换到该分支:

   ​	`git checkout -b new-branch-name`

   <!-- endtab -->

   <!-- tab -->

   为什么要切换分支？

   如果某个变更（提交）是非常重要的，那么一定要跟某个分支绑定在一起

   <!-- endtab -->
   {% endtabs %}

   

3. `git merge`

   {% tabs merge %}

   <!-- tab merge图解 -->

   {% folding blue, 什么是merge %}

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/thismerge.png" width="600">

   {% endfolding %}

   <!-- endtab -->

   <!-- tab merge-bugFix -->

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20201226120909.png">

   <!--endtab -->

   {% endtabs %}

###   `git rebase`

{% tip cogs%}

第二种合并分支的方法是  **`git rebase`** 。Rebase 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去。

Rebase 的优势就是可以创造更线性的提交历史，这听上去有些难以理解。如果只允许使用 Rebase 的话，代码库的提交历史将会变得异常清晰。

{% endtip %}

{% tabs git-rebase %}

<!-- tab -->

{% folding  后续有待深入理解 %}

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/thisRebase.png">

{% endfolding %}

<!-- endtab -->

<!-- tab rebase-原理 -->

{% folding rebase-合并原理 %}

这关的主要命令:

```bash
+ 新建并切换分支 bugFix 

	git branch bugFix
	git checkout bugFix
	简写:
		git checkout -b bugFix
 + 在 bugFix 分支进行一次提交
 	git commit -m "create new branch bugFix and commit content"
 + 切换回 master 分支
 	git checkout master
 	+ 在 master 提交信息
 	git commit -m "return master and commit content"
 + 返回 bugFix 进行 rebase 
 	git checkout bugFix
 	git rebase master
```

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/finishRebase.png">

{% endfolding %}

<!-- endtab -->

{% endtabs %}

###   分离 `HEAD`

{% tabs 分离HEAD %}

<!-- tab HEAD解释 -->

`HEAD,然而什么是 HEAD`

{% hideBlock 点击查看:HEAD解释 %}

{% tip cogs %}

我们首先看一下 “HEAD”。 HEAD 是一个对当前检出记录的符号引用 —— 也就是指向你正在其基础上进行工作的提交记录。

HEAD 总是指向当前分支上最近一次提交记录。大多数修改提交树的 Git 命令都是从改变 HEAD 的指向开始的。

HEAD 通常情况下是指向分支名的（如 bugFix）。在你提交时，改变了 bugFix 的状态，这一变化通过 HEAD 变得可见。

{% endtip %}

{% endhideBlock %}

<!-- endtab -->

<!-- tab 分离的HEAD -->

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/fHEAD.png">

`HEAD -> C1`

<!-- endtab -->

<!-- tab 分离HEAD实际操作-->

目标: 从 `bugFix` 分支中分离出 HEAD 并让其指向一个提交记录。

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/checkoutC4.png" title="完成下图的操作命令">

{% hideBlock 点击查看具体命令HEAD分离 %}

```bash
git checkout c4
```

{% endhideBlock %}



<!-- endtab -->

{% endtabs %}

###    `git status`

```bash
查看状态
```

###  添加文件

```bash
git add 文件名 # 提交指定文件

git add . # 英文小点 对所有文件添加
```

###  添加提交日志信息

```bash
git commit -m "日志信息"

# 修改提交后的 commit message
  +  修改最新的 commit 
	git commit --amend
	
 + 老旧的 commit 进行修改
 	
 	git rebase -i 目标-commit-ID
 
 	注意为交互式: 选择一种 例如: r
```

+ `git commit --amend` 修改最近一次的 `commit-message`

​	<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210103145414.png">

+ 老旧的`message` 修改

  ```bash
  git rebase -i commit-ID (找父级)
  ```

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210103145929.png" title="为能正确使用该命令 有待补充">

  + 应该显示如下信息

    ```bash
    注意: 涉及基点，选择适合的策略修改
    
    须知: 多个或者间隔的 commit  可以合并
    ```

    <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210103151300.png">

###  远程仓库的拉取

```bash
git pull origin 分支名 # origin是对提交地址添加的别名,后续指出
```

###  提交至远程仓库

```bash
git push origin 分支名
```

###  删除不需要的文件

```bash
1. 手动删除

2. 使用命令对文件删除
```

{% hideBlock  基础命令准备预备文件 %}

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/createFils.png" width="600">

{% endhideBlock %}

{% tabs 文件删除 %}

<!-- tab 手动删除文件 -->

1. 手动删除文件

   {% hideBlock 手动删除文件 %}

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/shou.png" title="右键删除想要删除的文件即可" width="600">

   {% endhideBlock %}

2. 查询当前信息

   {% hideBlock 查看删除后的状态信息 %}

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/deleteFile.png" width="600">

   {% endhideBlock %}

<!-- endtab -->

<!-- tab 命令行删除文件 -->

{% tabs 删除的两种方式  %}

<!-- tab -->



```bash
# 删除指定文件
git rm newFile.txt -f # -f 参数为强制删除
# 查看当前状态
git status

```

{% hideBlock 命令行删除单个文件 %}

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/clsFile.png">

{% endhideBlock %}

<!-- endtab -->

<!-- tab 删除该路径下的所有文件及文件夹 -->

`git rm -rf *`

<!-- endtab -->

{% endtabs %}

<!-- endtab -->

{% endtabs %}

###  文件中重命名

{% tabs id-rename %}

<!-- tab 手动重命名 -->

1.  选择目标文件,右击选择重命名
2.  `git status`
3.  在进行步骤 `2`时可以发现实际进行了两个步骤
   + 删除原文件
   + 添加新文件

<!-- endtab -->

<!-- tab 手动重命名配图 -->



   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/renameFir.png" height="300">

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/secondC.png">



<!-- endtab -->

<!-- tab 执行命令行操作 -->

`git mv  原文件名称.后缀名  新文件名称.后缀名  `

{% hideBlock 请思考命令行操作是执行了几步 %}

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/renameFile.png" title="当前状态是 rename">

{% endhideBlock %}

<!-- endtab -->

{% endtabs %}

###  移动文件并对文件重命名

```bash
git mv 目标文件 路径/新名称
```

###  查看文件的前后变化

```bash
git log --pretty=oneline path/文件名

输出:

	11fa30c159f0468334f11fc58f0e98130fa8478c (HEAD -> main) addFuile

+ 查看当前的 commit

	git show 11fa30c159f0468334f11fc58f0e98130fa8478c # 查看具体 commit 信息
	
+ 查看具体文件

	git log -p path/file
```

###  操作失误如何一键还原

```bash
+ (未加入暂存区,未执行 git add .)可以还原回到上一次提交的状态

git checkout -- path/fileName
```

###  不在追踪时如何实现撤销追踪操作

```bah
执行了 git add . 后进行状态还原

git reset HEAD path/fileName
```

###   回到指定版本

```bash
后续补充命令: git cat-file -t commit-ID 

参数：
    -t 查看类型
    -p 查看内容
    
图形化界面打开:
	 gitk --all
```



```bash
1. 实现方法一
	git reset --hard HEAD^ # 一个尖角号代表一个版本
2. 实现方法二
	git log(补充: git log -n(数值 查看多少范围内的提交))
	# 可以取前几位或者全部id
	# Eg. git reset --hard HEAD 11fa
	
	git reset --hard HEAD commit-ID （疑问）
	
	git reset --hard commit-id (回退到某一版本 暂存区和工作区一致 慎重)
	
	# git reset  HEAD 直接恢复暂存区的所有文件
```

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/commitID.png" title="commit id 每提交一次都会产生一个 commit-id">

###  指定文件进行版本回退

```bash
# 拿取回退版本的 commit-ID
git log
# 单独文件进行回退指定版本 其他文件不会受到影响
git checkout commit-id -- 指定文件 
```

###  实战之`git 本地`推送至`github`远程

1. 第一次提交

   + 登录/注册 `github` 账号

   + 点击头像 旁边的`+`

     <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/nwqresository.png" title="新建仓库">

   + 进入如下界面

     + 在本地需要提交至远程的文件夹初始化
     + 执行`git init`
     + 添加暂存区操作`git add .`
     + 添加日志`git commit -m 日志信息`
     + 切换主分支`git branch -M main`(可以不执行该命令，当前默认 main)
     + 对于`git`访问链接起别名 `origin`,`git remote add  origin xxx` 
     + 推送远程`git push origin main`

     <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/gitRes.png" title="远程仓库">

2. 二次修改并推送远程

   + 执行添加命令

     ```bash
     git add .
     ```

   + 执行添加提交的日志信息

     ```bash
     git commit -m 日志信息
     ```

     ```bash
     拉取与推送中可能有一个会出问题 ref···
     # 我暂时会使用强制推送不过不建议甚至不要用
     (出现红色 refjected 时，需要 merge 后续提到解决方案,暂时强制推送)推送命令:
     	git push origin main -f
     ```

   + 拉取远程至本地

     ```bash
     # pull 拉取 origin 别名 main 拉取的分支名
     git pull origin main 
     ```

   + 推送至远程

     ```bash
     git push origin main
     ```

   3. 链接

      <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/codeaddress.png" tile="clone 时会使用到地址或其他途径使用">

4.  克隆仓库

   ```bash
   # 指定分支克隆
   git clone -b 分支名 地址
   # 直接克隆目标
   git clone 地址(上述提到的链接)
   ```

###  版本进行标签化管理

1. 最新内容添加

   ```bash
   # 添加在最新的 commit
   git tag 版本号(自定义符合规范即可 Eg. v1.0)
   ```

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20201226172555.png" title="对最新的提交添加tag">

2. 对以往内容添加标签

   ```bash
   # 获取 commit id
   git log
   # 添加在以往的 commit
   git tag 版本 commit-id
   ```

3. 删除标签

   ```bash
   # 删除标签
   git tag -d 删除的tag-name
   ```

4. `tag`推送至远程库

   ```bash
   git push origin tag-name
   ```

###  分支及分支的操作(增，删)

1. 创建分支

   ```bash
   # 创建分支
   git branch 分支名
   # 查看分支 * 为当前所在分支
   git branch 
   ```

2.  切换分支

   ```bash
   # 切换分支
   git checkout branch-name
   ```

+ 演示

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/addDev.png" title="分支创建,切换" width="400"> 

3. 删除分支

   ```bash
   # 前提条件: 1.不能处于想要删除的分支上 2. 不能删除有提交的分支为推送远程
   git branch -d  branch-name
   ```

   + 解释注释内容

     + 处于该分支不能删除（<font color="red">观察**`*` **</font>）

       <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/innerDev.png" title="处于 dev 分支">

     + 分支进行了 `commit`

       <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/textADd.png" title="分支操作">

       + 强制删除分支

         ```bash
         git branch -D branch-name
         # 成功删除分支显示
         # $ git branch -D dev
         # Deleted branch dev (was a4f4fb0).
         ```

4. 创建分支并切换到该分支

   ```bash
   git checkout -b new-branch-name
   ```

###  分支合并

```bash
# 切换到 main 分支，将 dev 分支合并到 main
# git merge dev
git merge merge-branch-name
```

+ 注意查看右侧图像变动

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/newbranch.gif" title="注意图像变动" width="600">

+ `merge `产生冲突

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/mergeers.png" title="merge Error" width="600">

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/mergeErro.png" title="实现 merge error" width="600">

+ 解决方案
  + 方法一

    ```bash
    # 保留原分支代码，忽略其他分支代码
    git merge --abort
    ```

    <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/finshMerge.png" width="400">

  + 方法二

    ```bash
    自行操作时只需要再次输入: git merge dev（ 分支名-- dev 为例子）
    ```

    + 手动删除特殊符号后保存(与其他人沟通得到最终方案执行)

    + 执行`git add .`

    + 再执行`git commit`，添加编辑信息

      <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/mergeRes.png" title="按 i 进行内容添加,添加完毕后按下ESC 再输入冒号,输入 wq 退出" width="600">

    + `git commit -m` "对于这次合并要添加的日志信息"

      <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/enMerge.png">

    + 推送远程

      ```bash
      git push
      ```

    ###  23. 不同人想要查看版本路线该如何进行操作

    ```bash
    #  局部信息
    git log --oneline
    ```

    <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/logInfo.png" title="使得他人快速了解该项目做了那些">

    ```bash
    # 更加具体
    git log --oneline --graph
    ```

    <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/graph.png">

###  删除不想要的分支(远程分支)

```bash
# 拉取所有远程库(拉取所有分支)
git fetch
# 删除远程分支 执行前: 三思而后行
git push origin --delete branch-name
```

###  模拟多人修改同一文件（实战后有待优化···）

#####  实现`github`同一台电脑配置两个邮箱和用户名

```bash
git clone 地址 指定文件夹名称
```

```bash
# 添加多个用户
git config --add --local user.name 'xxx'
git config --add --local user.email 'xxx@qq.com'
# 
git config --local --list
```

```bash

# 
git branch -av 
# 本地分支与远端分支关联
git checkout -b branch-name remots/远端别名/branch-name
```

###  纳入了版本管理中: (`.gitignore`文件不生效)

####  需求: 忽略某些文件

+ 在推送后发现某些内容不需要添加，无法忽视

+ 解决方案:

  ```bash
  # 清理暂存区
  git rm -r --cached .
  git add .
  git commit -m 'update .gitignore'
  ```

###  分离头指针

```bash
不建议的操作
	
	git checkout commit-ID
	git commit -am"commit log" # 不经过暂存区
	git log (查看 HEAD 时发现无指向)
	gitk --all(图形化界面查看)
```

+ 分离头指针（我的理解暂时有点抽象）

  ```bash
  分离头指针内容如果无用会被清理
  ```

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210103143654.png" width="600">

###   暂存区和HEAD  包含文件比较

```bash
# 比较命令

git diff --cached 
```

###  工作区和暂存区进行差异比较

```bash
git diff

# 指定文件比较差异
git diff -- file-name
```

###   分支与分支之间内容差异比较

```bash
# 所有内容比较
git diff branch-name1 branch-name2

# 两条分支中具体文件比较差异
git diff  branch-name1 branch-name2  -- file-name(commit-id 比较等同)

```

###  开发中临时加塞紧急任务处理方案

```bash
+ 将当前任务放在一个隔离环境
	git stash
	
+ 去处理BUG

+ 完成 BUG 回到 stash 的任务
	两种:
		1.  git stash apply
			git stash list 
		2. git stash pop
```





##  总结:

###   github 插件推荐：

```bash
1. Octotree - GitHub code tree(作用: 列出目录结构)
2. Enhanced Github(作用: 直接显示文件大小)
3. GitZip for github(作用: 双击可以下载单独文件)
```

####  无法推送,出现`injected`解决方案

```bash
# 查看远端仓库关联信息
git branch -av

git merge origin/branch-name
# 输入这次修改的信息 merge时: git commit 的操作一样
git push 
```

####  本地分支与远程分支关联的两种方式

1. 方式一

   + 再远程仓库(`github`)新建分支

     <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/branchDevA.png" title="建立远程分支">

   + 命令行执行`git fetch`,如下显示拉取了远程

   ```bahs
   $ git fetch
   From https://github.com/lovobin/hiddenContent
    * [new branch]      dev        -> origin/dev
   
   ```

   #### 测试是否关联远程分支

   ```bash
   # 在 dev 分支写入以下修改内容
   $ echo dev-README.md > README.md
   # 添加
   git add .
   # 日志
   git commit -m "dev: update"
   # 请求远程库
   git pull origin dev
   # 添加 merge 日志信息
   $ git pull origin dev
   
       From https://github.com/lovobin/hiddenContent
        * branch            dev        -> FETCH_HEAD
       Removing reName.txt
       Merge made by the 'recursive' strategy.
        index.html | 4 ++++
        reName.txt | 1 -
        2 files changed, 4 insertions(+), 1 deletion(-)
        delete mode 100644 reName.txt
   
   
   $ git commit -m "dev: update "
   $ git push origin dev
   
   ```

   + 刷新远程库

     <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/devOrigin.png" title="得到结果为: 成功关联远程分支">

2. 方式二： 命令行操作(初学者的我尝试后不建议)

   ```bash
   # 新建本地分支
   简写创建切换:
   	创建: git branch branch-name
   	切换: git checkout branch-name
   创建切换总写: 
   	git checkout -b new-branch-name
   # 提交本地分支到远程仓库
   	git push origin local-branch-name
   	
   	
   	
   # 本地分支与远程分支关联(去除···)
   # git branch –set-upstream local-branch-name(本地新建分支名) origin/远程分支名
   ```
   
   