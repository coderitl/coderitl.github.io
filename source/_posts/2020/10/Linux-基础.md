---
title: Linux-基础
tags: Linux
categories: Linux
cover: 'https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/Linux.jpg'
abbrlink: 56685
date: 2020-10-17 22:20:21
top_img:
---

###  准本工作

+ `Centos`连接用户信息

  ```bash
  login: root
  
  passwd: aidou123456
  ```

+ 基本权限符

  ```bash
  # 超级用户提示符
  
  $ 普通用户提示符
  
  ~ 当前所在家目录
  ```



### Centos 7 安装后没有网络的解决方案：

####  设置 

1. 设置 - 网络适配器 - `NAT模式(wlan可以选择桥接模式)`

2. 进入 `Linux终端 ` 

   ```bash
    # 进入 网卡配置信息目录
    cd /etc/sysconfig/network-scripts
   # 查看具体信息
   ls 
   # 编辑该文件 ens33 每个电脑应该不相同,但以 ifcfg- 开头
   vi ifcfg-ens33
   
   ```

   + 文件解读（配置两个）

     + 公网访问配置

       {% folding ifcfg-ens33-公网访问配置  %}

       ```bash
       # 个人配置项 默认配置项忘记预留 ifconfig/ip addr
       TYPE=Ethernet
       BOOTPROTO=dhcp
       DEVICE=ens33
       ONBOOT=yes
       NM_CONTROLLED=yes
       
       -------- 保存退出 ------------
       esc: wq
       
       # 重启服务
       service network restart
       # 测试
       ping https://www.baidu.com
       
       
       ```

       {% endfolding %}

     + 内网配置

       >  `再开机启动设置处再添加一个网络适配器`

       <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/nat.png">

     +  添加 `ip`

       {% folding 添加内网`IP` %}

       ```bash
       # 查看已开启的网卡信息 
       ip -a
       # windows 下
       控制面板 \ 网络和 Internet \ 网络连接 \ Vmware 网络 [net1 仅主机模式]
       
       # 进入网卡信息配置目录
       cd /etc/sysconfig/network-scripts
       # 复制 ifcfg-ens33 到当前目录下
       cp ifcfg-ens33 new-name
       
       ----------------------------------------------------------------
       # 添加如下信息
       TYPE=Ethernet
       BOOTPROTO=dhcp
       DEVICE=ens37
       ONBOOT=yes
       NM_CONTROLLED=yes
       IPADDR=10.1.1.250 # 不要和主机同一网段
       
       ----------------------------------------------------------------
       
       # 保存退出 重启服务
       service network restart
       ```

       <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/windowsIP.png">

       {% endfolding %}

       

###  主机名永久修改

+ `centos7`主机名修改

  ```bash
  vi /etc/sysconfig/network
  # 修改如下配置信息
  NETWORKING=yes
  HOSTNAME=new-name
  
  # [主机名和 ip 绑定 前面两个请勿改动 在后续添加即可] 可选操作
  vi /etc/hosts
  
  ```

  

###  关闭防火墙(注意权限使用)

1. 临时关闭防火墙

   ```bash
   service iptables stop
   ```

2. 永久关闭防火墙

   ```bash
   chkconfig iptables off
   ```

3. 查看

   ```bash
   chkconfig --list | grep iptables
   ```

   

###  YUM 源配置（请更换`aliyun`）

+ `yum`作用： 类似于 360软件安装管家

####  镜像挂载(ISO 镜像文件设置后)

1. 已挂载在光驱中信息查看

   ```bash
   [roo@localhost ~]$ lsblk
   NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
   sda               8:0    0   20G  0 disk 
   ├─sda1            8:1    0    1G  0 part /boot
   └─sda2            8:2    0   19G  0 part 
     ├─centos-root 253:0    0   17G  0 lvm  /
     └─centos-swap 253:1    0    2G  0 lvm  [SWAP]
   sr0              11:0    1  4.5G  0 rom  /run/media/roo/CentOS 7 x86_64 # 需要查看信息
   [roo@localhost ~]$ 
   ```

2. 挂载

   ```bash
   # 以只读方式挂载
   mount -o ro /dev/sr0 /mnt/
   # 查看
   /dev/sr0                 4.5G  4.5G     0  100% /run/media/roo/CentOS 7 x86_64
   
   # 查看光盘下的目录 [mnt]
   ls /mnt/
   ```

3. 修改配置文件告诉`yum` 工具去那个仓库找

   {% folding yum配置 %}

   ```bash
   # 进入仓库目录
   cd /etc/yum.repos.d
   # 查看已有网络源
   ls
   
   # 备份已有
   # 新建文件见存放已有 repo
   mkdir backupRepo
   # 移动所有 repo 至 backupRepo目录中
    CentOS-* backupRepo/
   
   
   # 新建文件  光盘镜像源 发现在后续使用有缺陷
   vi local.repo
   # 添加如下配置
   [local] # [名称随意]
   name=xxx # 描述信息
   baseurl=file:///mnt # 必须指定
   enabled=1 # 启用仓库
   gpgcheck=0 # 不检验 【校验码】
   
   # 保存 退出
   
   # 清除 yum 缓存
   yum clear  all
   # 创建 yum 缓存
   yum makecache
   # 验证
   yum repolist
   ```

   {% endfolding %} 

4. 阿里源更换

   ```bash
   1. 备份原有镜像源
   2. 下载 wget
   	yum -y install wget
   	
   3. 下载新的CentOS-Base.repo 到/etc/yum.repos.d/
   	wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
   	
   4. 下载aliyun
   	wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
   	
   5. 清理缓存
   	yum clean all
   	
   6. 生成缓存
   	yum makecache  
   ```

   

###  SSH 远程`NAT 模式ip不可以连接,需要通过 仅主机模式即为内网ip连接 `

+ 检测端口号占用问题

  ```bash
  netstart -a|grep 端口号
  ss -a|grep 端口号
  lsof -i 端口号
  grep 端口号 /etc/services
  ```

+ 修改配置文件

  ```bash
  vim /etc/ssh/ssh_config 
  # 过滤
  esc: /Port 修改端口号【2209】
  # 重启服务
  service sshd restart
  # 验证连接
  	1. 连接方式一: ssh -l用户名 ip -p端口号
  	2. ssh 用户名@ip:port 【ip: 使用内网自定义ip可用于连接】
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/ipaddr.png" width="800">

  + 个人出现了一写问题

    ```bash
    主要原因就是由于使用的光盘镜像中 openssh 包问题,导致 sshd 服务无法启动
    ```

    

### Linux 常用命令:

####  文件处理命令

1. 创建目录

   ```bash
   mkdir -p [目录名] (-p递归创建)
   ```

2. 删除目录

   ```bash
   rm -rf 【目录名】  【-r 删除目录   -f 强制】
   ```

3. 复制

   ```bash
   cp [选项] [原文件或目录] [目标目录]
   	[-r 复制目录 -p 连带文件属性复制 -d 若源文件是链接文件，则复制链接属性 -a == -pdr]
   ```

4. 重命名

   ```bash
   mv [在移动的基础上进行重命名 cp 命令同样可以进行重命名操作]
   ```

####  目录：

+ `linux`常用目录

  ```bash
   + /根目录
   + /bin 命令保存目录(普通用户就可以读取)
   + /boot 启动目录，启动相关文件
   + /dev 设备文件保存目录
   + /etc 配置文件保存目录
   + /home 普通用户家目录
   + /lib 系统库保存目录
   + /mnt 系统挂载目录
   + /media 挂载目录
  ```

+ 文件搜索命令

  1. `find`名令基础使用

     {% folding Find命令基本使用方法 %}

     ```bash
     文件搜索命令: locate 文件名[只能是文件名]
     
     命令搜索命令 whereis 与 which
     
     文件搜索命令 find
     
     字符串搜索命令 grep
     
     find 命令与 grep 命令的区别
     
     
     搜命令的搜索：
     
     	whereis 命令名
     	
     	which is
     	
     find 命令:
     	
     	find 【搜索范围】 【搜索条件】
     	
     	find / -name 具体文件名
     	
     通配符:
     	
         * ? []
         
         find /路径 -name "*"  任意多个
         
         find /root -iname 具体文件名（忽略大小写）
         
         find /root -nouser 没有所有者文件
         
         find /var/log/ -mtime +10 （10天前修改的文件）
         
         -10: 10 内修改的文件
          10 10天当天修改的文件
         +10 10天前修改的文件
         
     	按照文件大小搜索:
     	
     	find . -size 25k(k,M 单位)
     	+25(大于)
     	-25(小于)
     	
     PATH: 环境变量
     ```

     {% endfolding %}

  2. `grep` 命令

     ```bash
     
     	grep 【选项】 字符串 文件名
     	
     	选项:
     		
     		-i 忽略大小写
     		
     		-v 排除指定字符串
     		
     grep "size" 文件名（xxx）（在xxx 中查找 size 相关的字符串 ）
     
     grep -v "size" 文件名（xxx）（在 xxx 中不查找 size 相关的字符串 ）
     ```

  3.  `find`与`grep` 的区别:

     ```bash
     find 命令: 在系统当中搜索费和条件的文件名，如果需要匹配，使用通配符匹配，通配符是完全匹配
     
     grep 命令:  在文件当中搜索符合条件的字符串，如果需要匹配，使用正则表达式进行匹配，正则表达式包含匹配
     ```

  4. 帮助命令

     ```bash
     man 
     
     help
     ```



#### 压缩与解压缩命令

+ 常见压缩格式

  ```bash
  压缩:
      .zip 
      .rar
      .bz2
  
      .tar.gz
      .tar.bz2
      
     zip 压缩文件名.zip 源文件
     
     zip -r 压缩文件名 源目录 
  ```

+ zip 使用

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20201018113743290.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzM0MDQyMA==,size_16,color_FFFFFF,t_70#pic_center)

+ zip file

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20201018113743458.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzM0MDQyMA==,size_16,color_FFFFFF,t_70#pic_center)
  
  

+ 解压缩命令

  ```bash
  解压缩:
  	unzip 压缩文件
  ```

+ 解压目录压缩文件 `unzip one.zip` 

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020101811374235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzM0MDQyMA==,size_16,color_FFFFFF,t_70#pic_center)

  

+ 解压文件 `unzip newFile.zip`

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20201018113743372.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzM0MDQyMA==,size_16,color_FFFFFF,t_70#pic_center)
  
+ gzip使用方法

  {% folding gzip使用方法 %}

  ```bash
  gzip 源文件
  
  # 压缩为 .gz 格式的压缩文件，源文件会消失
  
  gzip -c 源文件 > 压缩文件
  
  # 压缩为 .gz 格式 源文件保留
  
  gzip -r 目录 # 测试未通过
  
  # 压缩目录下所有的子文件 但不能压缩目录
  
  
  # 解压缩:
  	
  	gzip -d 压缩文件
  	
  	gunzip 压缩文件
  	
  	
  # 压缩
  
  bzip 源文件 # 压缩为 .bz2 格式 不保留源文件
  
  bzip2 -k 源文件 (不能压缩目录) 
  
  # 解压缩
  
  bzip2 -d 压缩文件（-k 保留压缩文件）
  
  bunzip2 压缩文件 （-k 保留压缩文件）
  ```

  {% endfolding %}



####  常用压缩格式

+ 常用压缩格式

  ```bash
  .tar.gz
  
  .tar.bz2
  ```

+ 使用方法

  ```bash
  tar -cvf 打包文件名 源文件
  
  选项: 
  	
  	-c 打包
  	
  	-v 
  	
  	-f 指定打包的文件名
  ```

+ `.tar.gz` 格式

  ```bash
  # .tar.gz 压缩格式
  
  其实 .tar.gz 格式是先打包为 .tar 格式,在压缩为 .gz 格式
  
  tar -zcvf 压缩包名 .tar.gz 源文件
  
  选项: 
  	
  	-z 压缩为 .tar.gz 格式
  	
  	-x 解压缩为 .tar.gz 格式
  	
  ```

+ `tar zcvf `

  ![tar-gz格式压缩](https://img-blog.csdnimg.cn/20201018144436364.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzM0MDQyMA==,size_16,color_FFFFFF,t_70#pic_center)

+ `zxvf tar-gz`

  ![解压缩](https://img-blog.csdnimg.cn/20201018144620489.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzM0MDQyMA==,size_16,color_FFFFFF,t_70#pic_center)

+ `.tar.bz2` 压缩格式

  ```bas
  tar -jcvf 压缩包名.tar.bz2 源文件
  
  选项；
  
  	-z 压缩为 .tar.bz2 格式
  	
  tar -jxvf 压缩包名.tar.bz2
  	
  	-x 解压缩为 .tar.bz2 格式
  	
  ```

+ 解压到指定位置

  ```bash
  tar -jxvf 文件名.tar.bz2 -C xxx/xxx/xxx ( xxx--> 指定的文件路径)
  
  ** 注意: -C 的位置
  
  ```

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020101814505577.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzM0MDQyMA==,size_16,color_FFFFFF,t_70#pic_center)

+ 关机和重启命令

  ```bash
  关机:
  
  	shutdown -r now
  
  重启: 
  
  	reboot
  ```



###  配置`VIM`编辑器

####  基本配置

+ 配置 vim

  ```bash
  # 创建文件
  touch .vimrc
  # 写入一下配置信息
  vim .vimrc
  
      set nu # 显示行号
      syntax on # 高亮显示
      set ts=4 # 制表位
      set expandtab # 自动转换 tab
      set ruler # 显示光标
      set nohls # 关闭搜索高亮
  ```

####  末行模式

1. 显示关闭行号(`按下Esc后执行`)

   ```bash
   set nonu # 关闭行号
   set nu # 显示行号
   
   ```

2. 制表键位数设置

   ```bash
   set ts=4
   ```

3. `vim`下代码高亮显示

   ```bash
   syntax on # 开启
   syntax off # 关闭
   ```

4. 光标所在位置

   ```bash
   set ruler # 显示光标所在位置
   
   set noruler # 关闭光标显示
   ```

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/ruler.png">

5. 命令模式

+ 移动光标

  ```bash
  G # 光标移到文件末尾
  200G # 光标移动到第 200行
  gg # 光标移动到行首
  
  h 左
  j 下
  k 上
  l 右
   
   ctrl + y / ctrl + e 移动一行
   ctrl + f / ctrl + b 翻一页
   
   0 光标移动到行首
   $ 光标移动到行尾
   w 光标移动到下一个单词
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/LinuxD.png" title="慕课网截图">

+ 删除

  ```bash
  dd # 删除光标所在行
  100dd 从光标所在删除 100 行
  ```

+ 复制

  ```bash
  yy # 复制光标所在行
  
  10yy # 光标所在行开始复制 10 行
  
  p # 粘贴
  10p # 粘贴 10 遍
  
  ```

+ 撤销恢复

  ```bash
  u # 撤销
  ctrl + r # 恢复
  ```

+ 映射快捷键

  ```bash
  map <F2> gg99999dd # 回到行首 删除 9999行
  
  inoremap _main if __name__ == '__main__' 
  ```

+ 多文件操作

  ```bash
  :ls # 查看当前打开的所有文件（类似于windows的 windows + Tab,在linux只显示文件名称）
  :b 数字 # 显示指定文件
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/lsAllfile.png">

+ 窗口显示(分屏)

  + 水平拆分

    ```bash
    sp
    
    # 切换窗口
    ctrl + ww
    ```

  + 垂直拆分

    ```bash
    vs # 垂直拆分窗口
    ```

  + 退出窗口

    ```bash
    qa # 水平拆分垂直窗口
    
    wqa # 保存并退出所有窗口
    ```

+ 中断恢复

  + `shift + r`

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/recover.png">

  + 删除隐藏文件

    ```bash
    # 显示隐藏文件 
    ls -a
    
    rm -y 上一次中断的执行文件.后缀名.swp
    
    ```

+ 命令别名

  ```bash
  # 别名: 简化输入
  alias 别名 = '命令'
  
  # alias nl='ls -laR' # 递归显示,
  ```

+ 查找替换

  ```bash
  # 全文替换
  :1,$s/替换目标/替换为/ci # c确认 i 忽略大小写
  
  # 前 n 替换
  :1,10s/替换目标/替换为/ci # c确认 i 忽略大小写 
  
  # 一行有多个需要替换就需要添加 g 参数
  :1,10s/替换目标/替换为/cg # c确认 g 全局 global
  
  # 直接替换
  :1,$s/替换目标/替换为
  
  ```

####  `VIM`查找

> ` ? 或 /`

1. 快捷键

   ```bash
   shift + v | V # 选中光标所在行
     
   shift + g | G # 向下选择  
   ```

2. `vim`主题

   ```bash
   # 末行模式下
   
   :colorscheme (空格一下，按下 ctrl + d)
   
   # 显示可选主题
       blue       default    desert     evening    koehler    murphy     peachpuff  shine      torte
       darkblue   delek      elflord    industry   morning    pablo      ron        slate      zellner
   
   # 可以从网络下载主题
   
   https://github.com/flazz/vim-colorschemes
   
   # 可写入 .vimrc 文件永久配置 存入 git 进行版本控制, 以后方便使用
   
   # 开源: https://github.com/liuchengxu/space-vim (以后配置)
   ```

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/autoindent.png" title="python 文件未能实现自动换行">

3. `Vim`插件配置

   ```bash
   # https://github.com/sbdchd/neoformat vim 代码格式化插件
   ```

####  宏：

+ 录制宏

  ```bash
  末行模式: q其他字母
  ```

+ `python`注释宏录制

  + `vim`文件

  + 按下`q`，在键入其他字母`Eg. a 寄存器名称`

  + 按下`i`

  + 添加注释 `#`

  + 按下`ESC`，按下`j`进入下一行

  + 按下`q`结束宏

    

  + 播放宏

    + 数字 `@a`

  + 演示

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/hong.gif" width="600">



### Shell基础:

{% tabs shell-符号 %}

<!-- tab 管道符 -->

```bash
管道符；
 	
 	;
 	
 	&&
 	
 	||
 	
 	
 检测:
 
 	ls && echo "yes" || echo "no"
	
	# 如果 ls 正确执行 输出 yes 否则 no
```

<!-- endtab -->

<!-- tab 通配符 -->

```bash
通配符:

	?
	*
	[]
```

<!-- endtab -->

{% endtabs %}





### 用户和用户组:

{% tabs 用户和用户组 %}

<!-- tab 认识用户和用户组  -->

```bash
# 用户: 使用操作系统

# 用户组: 具有相同系统权限的一组用户
```

<!-- endtab -->



<!-- tab 创建用户和用户组  -->

```bash
# 创建用户组
	groupadd 组名
# 修改用户组名称
	groupmod -n 新组名 旧组名
# 添加组编号
	groupmod -g 668(组编号) 组名
# 创建用户组 并添加组编号
	groupadd -g 888 组名
# 删除用户组
	groupdel 组名(必须先删除用户)
	
	
# 用户
# 创建用户组
	groupadd 组名
# 添加用户
	useradd -g 组名 用户名1
	useradd -g 组名 用户名2
	
# 添加用户 并指定用户个人文件夹
	useradd -d /hone/xxx (用户组 可省略) 用户名
	
# 查看
	cat /etc/passwd
```

<!-- endtab -->



<!-- tab 删除用户和用户组  -->

```bash
# 对用户添加备注
	usermod -c 备注信息 用户名
# 修改用户的文件夹路径
	usernod -d /home/xxx 用户名
# 修改用户的所属用户组
	usermod -g 新用户组名 旧用户组名
# 删除用户和用户文件夹
	userdel -r 用户名
```

<!-- endtab -->



<!-- tab 户和用户组权限管理  -->

```bash
# 禁止除了root 其他用户登录

touch /etc/nologin
```

<!-- endtab -->



<!-- tab 进阶 -->

```bash
# 锁定用户
	passwd -l 用户名 
# 解锁用户
	password -u 锁定的用户名
# 无密码登录
	passwd -d 用户名
```

<!-- endtab -->

{% endtabs %}

​	



