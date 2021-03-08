---
title: Linux-Mariadb使用
tags:
  - Linux
  - mysql
categories: Linux
abbrlink: 4278
date: 2021-01-16 10:16:48
top_img:
---

###  Linux-Mariadb使用

> 数据库文件获取: `https://github.com/lovobin/Python-Flask/tree/main/Mariadb` `all.sql`

+ 启动服务

  ```bash
  systemctl start mariadb
  ```

+ 检测状态

  ```bash
  systemctl status mariadb
  ```

+ 连接`mariadb`

  ```bash
  mysql -u root -p
  ```

+ 数据库创建

  ```sql
  -- 创建数据库 school 并指定默认字符集 utf8
  create database school default charset utf8;
  
  -- 切换数据库
  use school;
  
  -- 删除数据库(一般不要尝试····)
  drop database school; 
  -- 完善删除命令
  drop database if exits school;
  
  ```

+ 图像化工具

  ```bash
  # 配置 root 用户不被允许
  create user 用户名@'%' identified by "密码";
  # 赋予权限
  grant all privileges on 数据库名.* to 用户名@"%";
  grant all privileges on *.* to 用户名@"%";
  grant select on *.* to 用户名@"%";
  ```

+ `pycharm`相关信息填写

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/connect.png" width="600">

  + 验证成功

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/rightC.png">

  + `console`误关闭

    ```bash
    console 误关闭打开:
    
    	ctrl + shift + F10
    	
    	关闭后文件存在,但是需要手动备份源  >  新建文件.sql
    	
    	方块中显示出 console 需要上下左右键控制选择
    ```

    

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/conssol.png">

    + 备份数据

      <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/backupSQL.png">

  + `pycharm`展示`sql`

  + 快捷键

    ```bash
    ctrl + enter 执行所选片段
    
    格式化:
    ctrl + alt + l(小写 L)
    
    # 只要光标在想要复制的行上面,就不需要选中该行，按下即为整行复制
    ctrl + c
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/beautiful.png">

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/formatSQL.png" title="格式化后">

  + `pycharm`编写相关代码

    ```sql
    -- Linux 下连接执行
    MariaDB [(none)]> ? data types; -- 获取数据类型
    -- 数据大小
    MariaDB [(none)]>  ? int;
    ```

  + 命令执行

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/runConmmand.png">

  + `case when then end`

    ```sql
    
    -- 基础语法
    select key1,case key2 when 条件  then ‘输出结果1’ else ‘输出结果2’ end  [as ‘别名’] from table-name;
    
    
    Eg.  -- if else
    
    	select stu_id,stu_name, case stu_sex  when 1 then  '男' else '女'  end as '性别'  from student;
    
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/caseWhenend.png" width="600">

  + `if`

    ```sql
    select stu_id,stu_name,stu_address, if(stu_sex,'男','女') as 性别 from student;
    
    -- Oracle decode函数
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/newCommand.png" width="600">

+ `and`和`between and`

  ```sql
  -- and 和 between and
  
  select stu_id,stu_name,if(stu_sex,'男','女') as 性别 
  	from student where stu_id>'20201' and stu_id <'20206';
  	
  	
  select stu_id,stu_name,if(stu_sex,'男','女') as 性别 
  	from student where stu_id between 20202 and 20205;
  	
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/andBetween.png">

+ 数据库知识补充

  ```sql
  -- 数据文件备份
  -- Linux: mysqldump -uBinTest -p123456 --all-databases >/root/all.sql
  
  /*
  
  具体表象: 用二维表来保存数据
      ~ 行: 一条记录
      ~ 列: 一个字段(某个属性)
      ~ 主键列: 能够唯一标识一条记录的列
  
  编程语言: SQL 结构化查询语言
      ~ DDL: 数据定义语言 create / drop / alter
      ~ DML: 数据操作语言 insert / delete / update / select
      ~ DCL: 数据控制语言 grant / revoke
  
  */
  
  -- 创建名为 school 的数据库并指定默认的字符集为 utf8
  create database school default charset utf8;
  
  
  -- 查询当前用户
  select user();
  
  -- 如果存在名为 school 的数据库就删除它
  drop database if exists school;
  
  
  -- 创建表 student
  -- ? / help 终端执行
  -- 普通创建表加注释
  create table student
  (
      stu_id      int primary key not null, -- 学生学号
      stu_name    nvarchar(6)     not null, -- 学生姓名
      stu_email   nvarchar(20)    not null, -- 学生邮箱
      stu_address nvarchar(20)              -- 学生住址
  );
  
  -- 优化创建表
  create table tb_student
  (
      stuid      int(100) not null comment '学号',
      stuname    nvarchar(20) comment '姓名',
      stusex     bit default 1 comment '性别',
      stubirth   date,
      stuemail   nvarchar(20) comment '邮箱',
      stuaddress nvarchar(20) comment '住址',
      primary key (stuid)
  );
  
  -- 显示表结构
  desc student;
  desc tb_student;
  
  -- 查询表 student
  select *
  from student;
  
  -- 插入相关信息
  insert into student value (20201, 'name-01', '202101name01@qq.com', 'name-a', 1);
  insert into student value (20202, 'name-02', '202101name02@qq.com', 'name-b', 1);
  insert into student value (20203, 'name-03', '202101name03@qq.com', 'name-c', 1);
  insert into student value (20204, 'name-04', '202101name04@qq.com', 'name-d', 1);
  insert into student value (20205, 'name-05', '202101name05@qq.com', 'name-e', 1);
  insert into student value (20206, 'name-06', '202101name06@qq.com', 'name-f', 1);
  insert into student value (20207, 'name-07', '202101name07@qq.com', 'name-g', 1);
  insert into student value (20208, 'name-08', '202101name08@qq.com', 'name-h', 1);
  insert into student value (20209, 'name-09', '202101name09@qq.com', 'name-i', 1);
  
  
  -- 修改列的数据长度 (创建表时忘记字段长度)
  alter table student
      modify column stu_id int(10);
  
  alter table student
      modify column stu_name nvarchar(20);
  
  
  
  -- 增加列
  alter table student
      add column stu_sex bit default 1;
  
  -- 如果存在就删除学生表
  drop table if exists student;
  drop table if exists tb_student;
  
  -- 根据条件删除
  delete
  from student
  where stu_id = 20201;
  
  
  
  -- 删除列
  alter table student
      drop column stu_sex;
  
  -- 重命名列: 可以修改数据类型的大小
  alter table student
      change column stu_name stu_name varchar(21);
  
  -- 增删改查
  insert into student
  values ();
  delete
  from student
  where stu_name = '';
  -- 更新多个使用逗号分割
  update student
  set student.stu_name = ''
  where student.stu_name = '';
  select *
  from student;
  
  -- 添加外键约束，使两个表有关联
  alter table
      table- name [表名称] add constraint fk_tablename_foreignKeyName[外键名称]
      foreign key (keyname[关联表的主键]) references
      table - name (keyname[关联表的主键])
  
  -- 唯一性约束
  alter table table- name [表名称] add constraint
      uni_tablename_value1_value2[唯一性约束名称,由那两个属性组成唯一]
      unique (value1,value2);
  
  -- 投影和别名
  -- 投影
  select stu_id, stu_name, stu_id from student;
  -- 别名
  select stu_id as '学号',stu_name as '姓名' from student;
  
  
  -- 添加列 stu_sex
      alter table student add column stu_sex bit default 1 comment '性别';
  
  -- 更新数据  默认数据 bit 0--> 男  1--> 女
      update student set stu_sex=0 where stu_id = 20201;
      update student set stu_sex=1 where stu_id = 20202;
      update student set stu_sex=1 where stu_id = 20203;
      update student set stu_sex=0 where stu_id = 20204;
      update student set stu_sex=0 where stu_id = 20205;
      update student set stu_sex=0 where stu_id = 20206;
      update student set stu_sex=1 where stu_id = 20207;
      update student set stu_sex=0 where stu_id = 20208;
      update student set stu_sex=1 where stu_id = 20209;
  
  -- case when end 使用
  select stu_id,stu_name, case stu_sex  when 1 then  '男' else '女'  end as '性别'  from student;
  -- 其他数据库不通用方法
  select stu_id,stu_name,stu_address, if(stu_sex,'男','女') as 性别 from student;
  
  -- and 和 between and
  select stu_id,stu_name,if(stu_sex,'男','女') as 性别 from student where stu_id>'20201' and stu_id <'20206';
  select stu_id,stu_name,if(stu_sex,'男','女') as 性别 from student where stu_id between 20202 and 20205;
  
  -- 模糊查询
      select stu_id,stu_name from student where stu_name like 'name-%';
      select stu_id,stu_name from student where stu_name like 'name_';
      select stu_id,stu_name from student where stu_name like '%name%';
  
  -- 查询空值
      insert into student(stu_id,stu_email,stu_name) values (20210,'20210@qq.com',null);
  -- 空值
      select stu_id,stu_name,stu_email from student where stu_name is  null;
  -- 不为空查询
      select stu_id,stu_name,stu_email from student where stu_name is  not null;
  
  -- 去重操作
      insert into student(stu_id,stu_email,stu_name) values (20211,'20211@qq.com',null);
      insert into student(stu_id,stu_email,stu_name) values (20212,'20211@qq.com',null);
      insert into student(stu_id,stu_email,stu_name) values (20213,'20211@qq.com',null);
      insert into student(stu_id,stu_email,stu_name) values (20214,'20211@qq.com',null);
      insert into student(stu_id,stu_email,stu_name) values (20215,'20211@qq.com',null);
  
  -- 查询邮箱重复学员信息 表不合理
  select distinct(stu_email),stu_id,stu_name from student where stu_email='20211@qq.com';
  
  -- 排序
      -- 升序
      select stu_id,stu_name,stu_address from student order by stu_id asc;
      -- 降序
      select stu_id,stu_name,stu_address from student  where stu_address is not null order by stu_id desc;
  
  
  -- 聚合函数 忽略空值 = null
       max()      -- 最大值
       min()      -- 最小值
       average()  -- 平均值
       count()    -- 统计
       sum()      -- 求和
  
   -- 分组和聚合
      select count(stu_id) from student;
      -- 分组
          -- 统计男生和女生各有多少人
          select if(stu_sex,'男','女') as 性别,count(*) from student group by stu_sex;
  
  -- 筛选 分组 排序
  -- where group by order by
  
  -- 什么时候写 having ？
  /*
      分组以后的筛选 having
      分组前的筛选 where
  */
  
  -- 子查询
  ```

+ 删除外键约束

  ```sql
  alter table table-name drop foreign key fotrign-key-name;
  
  -- 约束
  restrict 不允许操作
  cascade 级联操作
  set null 设置为 null
  ```

+ 表信息

  + `school`

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/finishSQLTable.png">

  + `emp`

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/emp.png">

  + `dept`

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/dept.png">

  + `salgrade`

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/salgrade.png">



###  子查询

+ 子查询
+ 多表查询

###  分页查询

+ 分页查询

  ```sql
  -- 降序
  -- 所有记录
  select  empno,ename,job,sal from emp order by sal desc;
  -- 前 5 条记录
  select  empno,ename,job,sal from emp order by sal desc limit 5;
  -- 偏移 5 条查看 5 条: 6-10 条的记录
  select  empno,ename,job,sal from emp order by sal desc limit 5 offset 5;
  
  -- offset 缩略写法
  -- 跳过 10 条查 5 条
  select  empno,ename,job,sal from emp order by sal desc limit 10,5;
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/limit.png">

+ 简化写法

  ```sql
  -- 查询全表比较信息
  select  empno,ename,job,sal from emp order by sal desc;
  -- 简化写法
  select  empno,ename,job,sal from emp order by sal desc limit 10,5;
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/newlimit.png">

###  注意事项

```bash
1. 创建数据库库和创建表命名尽量使用小写

2. 作为筛选条件的字符串是区分大小看设置的校对规则

    Eg. create database table-name default charset utf8 collate utf_bin_ci;

    规则: utf_general_ci (忽略大小写)

3. 数据库中的对象通常会用前缀加以区分
	-- table / view / index / function / procedure
```

<img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/diffSQL.png">

###  练习

+ 批量插入

  ```sql
  insert into table-name values
  	(),
  	(),
  	(); -- 最后一条 ;
  ```

+ 外键自参照

  ```sql
  alter table tb_emp
      add constraint fk_emp_mgr foreign key (mgr) references tb_emp (eno);
  ```

+ 添加列到指定位置

  ```sql
  alter table table-name add column new-column-name data-type first; -- 添加到第一列
  
  alter table table-name add column new-column-name data-type after column-name; -- 某列的前面或后面
  ```

+ 数据资源获取
+ 习题

###  执行计划

+ 生成执行计划

  ```sql
  
  -- 同一结果
  
  explain select ename,eno from tb_emp where eno=7800;
  
  explain select ename,eno from tb_emp where ename ='张三丰';
  
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/explain.png">

###  索引

+ `index`索引(一本书的目录)

+ 索引意义

  ```sql
  索引可以加速查询索引应该在经常用于查询筛选条件的列上建立索引
  索引会使用额外的存储空间而且会让增删改变得更慢(因为要更新索引)
  
  所以不能滥用索引
  ```

  

+ 创建索引

  ```sql
  
  -- create index index-name on table-name(key);
  create index idx_emp_ename on tb_emp(ename);
  
  ```

+ 删除索引

  ```sql
  -- drop index idx_name on table-name; 
  drop index idx_emp_ename on tb_emp;
  ```

###  视图

+ 查询结果的快照

+ 创建视图

  ```sql
  -- 创建视图
  
  -- create view view-name as select ····
  create view view_emp_dept as select ename,t1.dno from tb_emp t1 inner join tb_dept td on t1.dno = td.dno;
  
  ```

+ 使用视图

  ```sql
  -- 使用视图  访问控制
  
  -- select * from view-name;
  select * from view_emp_dept;
  ```

+ 删除视图

  ```sql
  -- 删除视图
  -- drop view view-name;
  drop view view_emp_dept;
  ```

###  存储过程

+ 存储过程

  ```sql
  
  -- 存储过程
  delimiter $$
  -- 重新定义定界符为 $$
  -- 创建存储过程
  create procedure  sp_dept_avg_Sal(deptno int,out avgsal float)
  begin
          select  avg(sal) into  avgsal from tb_emp where dno=deptno;
  end $$
  
  
  -- 将定界符还原回;
  delimiter ;
  ```

+ 删除存储过程

  ```sql
  -- 删除存储过程
  drop procedure sp_dept_avg_Sal;
  ```

+ 调用存储过程

  ```sql
  call sp_dept_avg_Sal(参数···);
  ```

###  函数

+ 函数

  ```sql
  
  ```

###   触发器

+ 触发器

  ```sql
  在执行增删改查的操作是可以触发其他联级操作,但是有可能导致“锁表”现象,实际开发中应该尽量避免使用触发器
  ```

###  权限

```sql
-- DCL: 授予权限(grant to) 和召回权限(revoke from)
```

+ 创建用户

  ```sql
  -- 创建用户
      create  user 'UserName'@'localhost' identified by 'yourpassword';
      create  user 'UserName'@'127.0.0.1' identified by 'yourpassword';
      create  user 'UserName'@'%' identified by 'yourpassword';
  
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/newUser.png">

+ 删除用户

  ```sql
  -- 删除用户 一一对应 语法:
  
      drop user 'UserName'@'localhost';
      
  ```

  

+ 授予权限

  ```sql
  -- 权限 Oracle--> dba 权限
  -- 授予数据库所有的权限 给用户 ···
  -- 语法:
  grant all privileges on databases-name.* to 'user-name'@'address';
  
  ```

+ 收回权限

  ```sql
  -- 权限收回
  -- revoke  收回什么权限 on 在那个数据 to 的哪个用户;
  -- 收回增删改的权限 'user-name'@'address';
  revoke select,update,delete on database-name.* to 'user-name'@'address';
  ```

+ 事务

  ```sql
  -- 事务 (transaction) - 把多个增删改查的操作做成不可分割的原子性操作
  -- 要么全部都做,要么全部做
  -- 开启事务两种方法:
      -- 1.begin ;
      -- 2. start transaction;
  
  -- 插入测试数据
  insert into tb_emp(eno, ename,job,sal) values (7900,'张三','吃瓜群众',1200);
  -- 查询测试数据
  select * from tb_emp;
  -- 开启事务
  start transaction;
  -- 删除数据
  delete from tb_emp where eno=7900;
  
  -- 再次查询
  select * from tb_emp;
  -- 提交(事务中的所有操作全都不生效)
  commit;
  -- 回滚(事务中的所有操作全部撤销)
  rollback;
  
  -- 未执行 commit;
  ```

  

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/transaction.gif">