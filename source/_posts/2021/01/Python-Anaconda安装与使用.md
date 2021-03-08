---
title: Python-Anaconda安装与使用
tags:
  - Python
  - Anaconda
categories: Python
abbrlink: 44616
date: 2021-01-11 10:50:26
top_img:
---

###  Python-Anaconda安装与使用

####  1. Anaconda 安装(推荐)

+ 安装 `Anaconda`

  > 维基百科: Anaconda是一个免费开源的Python和R语言的发行版本，用于计算科学，Anaconda致力于简化软件包管理系统和部署。Anaconda的包使用软件包管理系统Conda进行管理。

1.  进入官网进行软件包下载: <a href="https://www.anaconda.com/products/individual"> 点击前往Anaconda 官网</a>

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/anaconda.png" width="400">

2.  下载后进行正常安装即可

3. 很重要的一步

   <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/anacondai.png" width="400">

4. 忘记步骤3时: 配置`Anaconda`环境变量 `Eg. D:\ProgramData\Anaconda3`

5. 测试安装`conda --version`,输出版本号即为安装成功

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210111110046.png">

6.   全局升级

    ```python
    # Anaconda 的 Scripts 路径下执行
     
        conda update --all
        
    ```

####  2. 使用

+ 发现

  ```python
   Pycharm 后台会自行下载一些东西,电脑风扇可能会加快转速
  ```

1. 作为`Pycharm`的解释器,环境包很多,后续几乎不用再进行安装

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/pycharmA.png" title="">

2. `Jupyter NoteBook`不用再单独进行安装,已经集成再`Anaconda`环境中

   <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/jupyterN.png">

3. `Jupyter Notebook`主题(Dos 窗口下执行)

   1. 安装主题库

      ```bash
      pip install jupyterthemes
      ```

   2.  列出可选主题

      ```bash
      jt -l (小写 L )
      ```

   3. 主题选择

      ```bash
      jt -t choice-themes-name
      ```

      <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/jtl.png" width="400">

4. 恢复默认主题（建议使用默认主题）

   ```bash
   jt -r
   
   注意: 运行后需要删除浏览器缓存 
   ```

   Google Chrome:浏览器： <kbd>ctrl</kbd>+<kbd>shift</kbd>+<kbd>Del</kbd>

5. 设置字体大小

   ```bash
   # 设置 markdown 和 notebook（界面）字体、字体大小
   jt -t oceans16 -tf merriserif -tfs 10 -nf ptsans -nfs 13
   ```

6. 调正单元格屏幕宽度％

   ```bash
   # 不建议执行 
   jt -t chesterish -cellw 90% -lineh 170
   ```

7. 参数

   ```bash
   jt -t chesterish：选择皮肤（chesterish）
   -f consolamono：代码的字体（consolamono）
   -fs 140：代码字体大小（140）
   -altp：Alt键提示布局（默认）
   -tfs 13：Text/MD 单元格字体大小（13）
   -nfs 115：Notebook 字体大小（115）
   -ofs 14：输出面积字形大小（14）
   -cellw 80%：单元格的宽度（80%）
   -T：工具栏可见
   ```

####  3. 第三方包安装

```python
# 选择自己的解释器对应使用 

conda解释器: conda install package-name
    
windows全局解释器: pip/pip3 install package-name
    
也可以添加镜像加速下载:
    
    推荐清华镜像: https://mirrors.tuna.tsinghua.edu.cn/help/pypi/ 
    
    其他可自行查阅
```



###  更新提示:

```bash
update: 2021.01.12  9:07:23

prompt: 前面提及到的包

注意: 
	新手练习建议保留,由于 pip 下载一些所需环境超时难以下载
     
```

<img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/notC.png" width="400" height="130" title="点击查看大图">

+ 更新后

  <img src="https://gitee.com/wang_hong_bin/pic-go-photos/raw/master/20210112091551.png" width="400" height="130" title="点击查看大图">