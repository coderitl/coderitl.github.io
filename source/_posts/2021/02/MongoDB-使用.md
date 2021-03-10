---
title: MongoDB-使用
tags:
  - Node
  - MongoDB
categories: MongoDB
abbrlink: 50332
date: 2021-02-15 10:02:12
---



###   Mongodb-数据库

```bash
说明描述:

	collection-name 自定义集合名

    [ ]  可选参数

    db.collection-name.find().pretty(); # 命令行中格式化显示某集合

    bin:  安装 mongodb 的 bin 目录下

```



####  命令行

```bash
windows+r: mongo [进入交互式命令行模式]

退出: exit / ctrl + D

```



####  基础操作

+ 查询数据库

  ```javascript
  show databases;
      admin   0.000GB
      config  0.000GB
      local   0.000GB
  
  ```

+ 使用数据库

  ```javascript
  use database-name;
  
  > use admin;
  switched to db admin
  
  注意: 在 mongodb 中使用不存在的数据库时不会报错,会自动隐式创建不存在的数据库
  ```

+ 查看集合

  ```javascript
  show collections;
  ```

+ 创建集合

  ```javascript
  语法:
  	db.createCollection('collection-name');
  
  > db.createCollection('student');
  { "ok" : 1 }
  
  注意: createCollection 没有 s
  ```

+ 删除集合

  ```javascript
  语法:
  	db.collection-name.drop();
  
  -- 创建集合 c2
  > db.createCollection('c2');
  { "ok" : 1 }
  -- 查看集合 
  > show collections;
  c2
  student
  -- 删除集合 c2
  > db.c2.drop();
  true -- 返回结果为布尔值
  ```

+ 查看当前使用数据库

  ```javascript
  -- 隐式创建的数据库没有内容查看不会被显示
  db
  ```

+ 删除数据库

  ```javascript
  use drop-database-name;
  db.dropDatabase();
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/monfo.png">



####  集合的增删改查

+ 集合增加数据

  + 插入一条数据

    ```javascript
    语法: db.collection-name.insert(json-data);
    注意: 集合存在则直接插入数据,集合不存在则隐式创建
    
    -- 显示可用集合
    show collections;
    
    
    -- 插入数据
    db.test.insert({"name":"zahngsan"});
    
    
    
    
    result: WriteResult({ "nInserted" : 1 })
    
    注意: 数据库和集合不存都会隐式创建，对象的键统一不加引号方便看，但是查看集合数据时系统会自动添加双引号
    ```

  + 插入多条数据

    ```javascript
    // 集合插入多条数据 db.collection-name.insert({})
    db.emp.insert([
        {
            name: "张三",
            age: 20,
            gender: "男"
        },
        {
            name: "李四",
            age: 18,
            gender: "女"
        },
        {
            name: "王五",
            age: 10,
            gender: "男"
        },
        {
            name: "王麻子",
            age: 38,
            gender: "男"
        }
    ]);
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/insertMore.png" width="600">

  + 快速输出` n `条数据

    ```javascript
    // 快速插入 10 条数据 支持 js 语法
    for (var i = 0; i < 10; i++) {
        print(i); // 测试输出
    }
    
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/mongojs.png" width="400">

  + 快速在指定集合插入`n `条数据

    ```javascript
    // 在指定集合中快速插入 n 条数据
    for (var i = 0; i < 10; i++) {
        db.dept.insert({
            deptno: "deptno" + i, // 字符拼接的形式
            age: i + 1
        });
    }
    
    // 查询结果集
    db.dept.find();
    
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/jsMon.png">

  + 查看集合内容

    ```javascript
    db.collection-name.find();
    
    > db.test.find();
    { "_id" : ObjectId("602380e157486fb18cef5489"), "name" : "zhangsan" }
    { "_id" : ObjectId("6023839257486fb18cef548a"), "name" : "lisi", "age" : 18, "gender" : "男" }
    
    _id: 可以被覆盖,进行自定义 _id: value (不推荐修改) 
    _id: 
    	组成原理: 时间戳 机器 PID 计数器
    ```

  + 条件查询

    ```javascript
    语法: db.collection-name.find(条件,[查询的列])
    ```

    ```javascript
    查询所有数据:  {} 可省略
    查询特定条件的值:  {条件: value}
    多条件查询: {条件1:value,条件2:value,····}
    
    查询列:
    [
        不写列 查询全部
        {某列名称: 1} 只显示 该列
        {某列名称: 0} 除了该列,显示其他列
    ]
    ```

  1. 查询所有数据

     ```javascript
     db.dept.find({});
     ```

  2.   只显示 `age` 列数据

       ```javascript
       db.dept.find({}, {
           age: 1
       });
       ```

  3. 显示所有非 `age`列数据

     ```javascript
     db.dept.find({}, {
         age: 0
     });
     ```

  4.  条件列

      | 运算符 |   作用   |
      | :----: | :------: |
      | `$gt`  |   大于   |
      | `$gte` | 大于等于 |
      | `$lt`  |   小于   |
      | `$lte` | 小于等于 |
      | `$ne`  |  不等于  |
      | `$in`  |   `in`   |
      | `$nin` | `not in` |

      ```javascript
      db.collection-name.find(
      	键: {运算符: 值}
      );
      ```

      + 查询年龄大于`8`的列数据`$gt`运算符

        ```javascript
        db.dept.find({
            age: {
                $gt: 8
            }
        });
        ```

        <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/$gt.png">

  5. 特定范围`&in` 运算符

     ```javascript
     // 特定范围内 Eg. 7, 8, 9
     db.dept.find({
         age: {
             $in: [7, 8, 9]
         }
     })
     
     
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/$in.png">

+ 修改集合

  > 
  >
  > 基础语法: `db.collection-name.update(条件,新数据[，是否新增,是否修改多条])`
  >
  > 是否新增: 指条件匹配不到数据则插入(`true`是插入,`false`不插入 默认)
  >
  > 是否修改多条：指将匹配成功的数据都修改(`true`是,`false`否 默认)
  >
  > 

  + 准备测试数据

    ```javascript
    // 创建新集合
    db.createCollection('testInfo');
    
    // 通过 for 循环插入 n 条测试数据
    for (var i = 0; i < 10; i++) {
        db.testInfo.insert({
            name: "name" + i,
            age: i + 1
        });
    }
    
    ```

  + 数据更新`update`

    ```javascript
    // 将 name: "name0" 改为 name: "name11"
    // 替换操作 并不能实现数据修改
    db.testInfo.update({
        name: "name0"
    }, {
        name: "name11"
    });
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/changeMon.png" width="600">

    + 数据修改

      ```javascript
      db.collection-name.update({条件}，{
                                
                                新数据【修改器】:{键: 值}}
      )
      ```

      ```javascript
      // 将 name: "name9" 改为 name: "name01"
      
      db.testInfo.update({name:"name9"},{$set:{name:"name01"}});
      
      ```

      <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/updateMon.png">

    + 多列数据更新

      ```javascript
      // 修改 name:name4 age:5 修改为 name:"name04",age:40
      db.testInfo.update({
          name: "name4",
          age: 5
      }, {
          $set: {
              name: "name04",
              age: 40
          }
      });
      
      --------------------------------------- S: 输出 -------------------------------------------------------
      
      > db.testInfo.find({name:"name04"});
      { "_id" : ObjectId("6023a1de167e00002a003d48"), "name" : "name04", "age" : 40 }
      >
      --------------------------------------- E: 输出 ------------------------------------------------------
      ```

    + 根据条件,对数据进行 `+5/-5`  `$inc`操作符

      ```javascript
      db.testInfo.find({
          name: "name01"
      }, {
          $inc: {
              age: 5/ [  -5 原基础减 5 ]
          }
      });
      
      ```

      <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/update$inc.png" width="600">

    |  修改器   |   作用   |
    | :-------: | :------: |
    |  `$inc`   |   递增   |
    | `$rename` | 重命名列 |
    |  `$set`   | 修改列值 |
    | `$unset`  | 删除字段 |

    + 所有操作符进行练习

      ```javascript
      
      ```

      <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/optionA.png">

    + `true`

      ```javascript
      db.testInfo.update({
          name: "name20",
          age: 5
      }, {
          $set: {
              name: "name04",
              age: 40
          }
      }, true);
      // 第三个条件 true: 没有找到则进行添加
      ```

      <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/updateTrue.png" width="600">

    + 第四个参数`true/false`

      ```javascript
      db.testInfo.update({name:"name2"},{$set:{age:22}},false,true);
      
      false: 没有不添加
      true: 允许修改多条
      
      ```

      <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/trueOrFalse.png" width="600">

+ 删除数据

  ```javascript
  语法: db.collection-name.remove();
  
      db.testInfo.remove({name:"name2"},true); // 只删除一条数据
      db.testInfo.remove({name:"name2"}); // 删除多条数据
  
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/removeMon.png" width="600">

+ 删除集合

  ```javascript
  // 删除集合语法 
  db.collection-name.drop();
  // 删除成功显示 true
  db.testInfo.drop(); 
  ```

  

####  排序分页

+ 基础语法

  ```javascript
  语法: db.collectipon-name.find().sort(JSON数据)
  
  JSON数据: 键就是要排序的列/字段 值: 1-升序 -1-降序
  
  ```

+ 排序练习

  ```javascript
  // 准备测试数据
  use test3;
  db.c1.insert({_id:1,name:"a",sex:1,age:1});
  db.c1.insert({_id:2,name:"a",sex:1,age:2});
  db.c1.insert({_id:3,name:"b",sex:2,age:3});
  db.c1.insert({_id:4,name:"c",sex:2,age:4});
  db.c1.insert({_id:5,name:"d",sex:2,age:5});
  
  // 查询
  db.c1.find();
  
  // 排序  -1降 1升
  
  // 对 age 列进行降序输出
  db.c1.find().sort({age: -1});
  db.c1.find().sort({age: 1});
  
  ```

+ `limit & skip`

  ```javascript
  limit(n): 查看 n 条
  skip(n): 跳过 n 条
  ```

  ```javascript
  // 跳过skip(2) 条查 limit(2) 
  db.c1.find().skip(2).limit(2);
  
  注意: skip() 
  
  db.c1.find().limit(2); == db.c1.find().skip(0).limit(2);
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/limitSkip.png" width="400">

  > `skip 计算公式: (当前页-1) * 每页显示条数`
  >
  > ​	
  >
  > `当前页: 第一页  1 ,  第二页  2 ····`
  >
  > 
  >
  > 练习: 某集合中有 10 条数据, 每页只显示两条数据
  >
  > `db.collection-name.skip(当前页 - 1).limit(2);`
  >
  > | 第一页 |                    `skip()`                    |
  > | :----: | :--------------------------------------------: |
  > |  `1`   | `db.collection-name.find().skip(1-1).limit(2)` |
  > |  `2`   | `db.collection-name.find().skip(2-1).limit(2)` |
  > |  `3`   | `db.collection-name.find().skip(3-1).limit(2)` |
  >
  > 

  

####  聚合查询

+ 基本语法

  ```javascript
  db.collection-name.aggregate(
  [
      {
          管道: {表达式}
      }
  ]
  )
  ```

+ 常用管道

  ```bash
  $group 将及合中的文档分组,用于统计结果
  $match 过滤数据,只要输出符合条件的文档
  $sort  聚合数据进一步排序
  $skip 跳过指定文档数
  $limit 限制集合数据返回文档数
  
  ```

+ 常用表达式

  ```javascript
  $sum 总和 $sum:1 同 count 表示统计
  $avg 平均
  $min 最小值
  $max 最大值
  ```

+ 练习聚合函数

  ```javascript
  集合结构:
  
      { "_id" : 1, "name" : "a", "sex" : 1, "age" : 1 }
      { "_id" : 2, "name" : "a", "sex" : 1, "age" : 2 }
      { "_id" : 3, "name" : "b", "sex" : 2, "age" : 3 }
      { "_id" : 4, "name" : "c", "sex" : 2, "age" : 4 }
      { "_id" : 5, "name" : "d", "sex" : 2, "age" : 5 }
  
  ```

  

  > 
  >
  > ```
  > db.collection-name.aggregate([
  > 
  > {管道1:{}},
  > 
  > {管道2: {}},   
  > 
  > ····
  > ]);
  > 
  > ```
  >
  > 

  1. 统计男生人数

     ```javascript
     // 统计男女生人数
     db.c1.aggregate([{
         $group: {
             _id: "$sex",
             rs: {
                 $sum: 1
             }
         }
     }]);
     ```

  2.  查询女生的总年龄

      ```javascript
      
      ```

  3. 根据 性别分组

     ```javascript
     // 根据 性别分组
     db.c1.aggregate([{
         $group: {
             _id: "$sex"
         }
     }]);
     ```

  4.  根据性别分组 统计 总: age

      ```javascript
      db.c1.aggregate([{
          $group: {
              _id: "$sex", // 分组
              total_age: {
                  $sum: "$age"
              } // 分组后条件
          }
      }]);
      ```

  5. 求学生的总人数和平均年龄

     ```javascript
     // 求学生的总人数和平均年龄
     db.c1.aggregate([{
         $group: {
             _id: null, //  不分组,全部数据
             totalStudent: {
                 $sum: 1 // $sum:1 == 其他数据库中的 count(*)
             }, 
             avg: {
                 $avg: "$age"
             }
         }
     }]);
     ```

  6. 查询男生,女生人数 按人数升序

     ```javascript
     db.c1.aggregate([
         { 
             // 分组管道
             $group: {
                 _id: "$sex",
                 toolS: {
                     $sum: 1
                 }
             }
         },
     		
     		// 分组后排序 
         {
             $sort: {
                 toolS: 1
             }
         }
     ]);
     
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/aggrgate.png" width="600">

     + 验证

       <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/toolS.png" width="600">



####  索引

+ 数据库中的索引

  1. 说明: `索引是一种排序好的便于快速查询的数据结构`
  2. 作用: `帮助数据库高效的查询数据`

+ 索引的优缺点

  + 优点

    > 提高数据查询的效率,降低数据库的 IO 成本
    >
    > 通过索引对数据进行排序，降低数据排序的成本，降低 CPU 的消耗

  + 缺点

    > 占用磁盘空间
    >
    > 大量索引影响 SQL 语句效率，因为每次插入和修改数据都需要更新索引

+ 基本语法

  + 测试数据准备

    ```javascript
    // 选择数据库
    use test4;
    // 向数据库中添加数据
    for (var i = 0; i < 10000; i++) {
        db.c1.insert({
            name: "name" + i,
            age: i
        });
    }
    // 统计插入的数据条数
    db.c1.find().count();
    
    
    ```

    

  1. 创建语法

     ```javascript
     db.collection-name.createIndex(待创建索引的列[,额外选项])
     
     参数:
     	待创建索引的列: 1-升序 -1-降序
     	额外选项: 设置索引的名称或者唯一索引
     ```

     + 创建普通索引

       1. 给` name` 列添加普通索引升序: `db.c1.createIndex({name: 1})`

          ```javascript
          > show collections;
          c1
          > db.c1.createIndex({name:1}); // name 列创建索引
          {
                  "createdCollectionAutomatically" : false,
                  "numIndexesBefore" : 1,
                  "numIndexesAfter" : 2,
                  "ok" : 1
          }
          >
          
          ```

          + 查看创建的索引

            ```javascript
            > db.c1.getIndexes(); // 查询已创建索引
            [
                    {
                            "v" : 2,
                            "key" : {
                                    "_id" : 1 // 索引升序排列
                            },
                            "name" : "_id_", // 默认索引名称
                            "ns" : "test4.c1" // test4数据库下的 C1 集合
                    },
                    {
                            "v" : 2,
                            "key" : { // key: 设置索引列
                                    "name" : 1 // 自定义索引升序排列
                            },
                            "name" : "name_1", // 索引默认名称
                            "ns" : "test4.c1" // test4数据库下的 C1 集合
                    }
            ]
            ```

       2.  给 `name`创建索引并起名`asIndexName`

           ```javascript
           db.c1.createIndex({name:1},{name:"asIndexName"}); // name 列创建索引升序 起名: asIndexName
           ```

           ```javascript
           > db.c1.getIndexes();
           [
                   ···
                   {
                           "v" : 2,
                           "key" : {
                                   "name" : 1
                           },
                           "name" : "asIndexName", // 起名成功
                           "ns" : "test4.c1"
                   }
           ]
           >
           ```

           

  2. 删除语法

     ```javascript
     全部删除: db.collection-name.dropIndexes();
     
     删除指定索引: db.collection-name.dropIndex(index-name)
     ```

     + 删除`name`建立的索引

       ```javascript
       > db.c1.dropIndex('name_1');
       { "nIndexesWas" : 2, "ok" : 1 }
       >
       ```

  3. 查看索引

     ```javascript
     db.collection-name.getIndexex();
     ```

  4. 创建符合索引

     ```javascript
     就是一次性给多个字段建立索引
     
     test4.c1: name,age 添加组合索引
     
     语法:
     
     	db.c1.createIndex({键1: 存储方式,键2: 存储方式});
     
     注意: 存储方式为升序或降序 1、-1
     ```

     + 查看建立的索引

       ```javascript
       }
       > db.c1.getIndexes();
       [
               {
                       "v" : 2,
                       "key" : {
                               "_id" : 1
                       },
                       "name" : "_id_",
                       "ns" : "test4.c1"
               },
               {
                       "v" : 2,
                       "key" : {
                               "name" : 1
                       },
                       "name" : "asIndexName",
                       "ns" : "test4.c1"
               },
               {
                       "v" : 2,
                       "key" : {
                               "name" : 1,
                               "age" : 1
                       },
                       "name" : "name_1_age_1",
                       "ns" : "test4.c1"
               }
       ]
       >
       ```

  5.  创建唯一索引

      ```javascript
      给 name 添加普通索引
      语法: db.collection-name.createIndex(待添加索引的列,{unique:”列名“})
      ```

      ```javascript
      > db.c1.createIndex({name:1},{unique:"name"});
      ```

      ```javascript
      // 删除索引
      db.c1.dropIndexes();
      // 创建唯一索引并起名为 uniqueIndex
      db.c1.createIndex({name:1},{name:"uniqueIndex"},{unique:"name"});
      ```



####  分析索引

+ 基本语法

  ```javascript
  db.collection-name.find().explain('executionStats');
  ```

+ 练习

  ```javascript
  // 删除所有索引
  db.c1.dropIndexes();
  ```

  1. 对未添加索引的数据进行查询

     ```javascript
     db.c1.find({age:1000}).explain('executionStats');
     ```

     ```javascript
     > db.c1.find({age:1000}).explain('executionStats');
     {
             "queryPlanner" : {
                     "plannerVersion" : 1,
                     "namespace" : "test4.c1",
                     "indexFilterSet" : false,
                     "parsedQuery" : {
                             "age" : {
                                     "$eq" : 1000
                             }
                     },
                     "queryHash" : "3838C5F3",
                     "planCacheKey" : "3838C5F3",
                     "winningPlan" : {
                             "stage" : "COLLSCAN",
                             "filter" : {
                                     "age" : {
                                             "$eq" : 1000
                                     }
                             },
                             "direction" : "forward"
                     },
                     "rejectedPlans" : [ ]
             },
             // 执行计划相关统计信息
             "executionStats" : {
                     "executionSuccess" : true, // 执行成功的状态
                     "nReturned" : 1, // 返回结果集数目
                     "executionTimeMillis" : 8, // 执行所需的事件,单位: 毫秒
                     "totalKeysExamined" : 0, // 索引检查的的时间
                     "totalDocsExamined" : 10000, // 检查文档总数 (某集合插入的所有数据)
                     "executionStages" : {
                             "stage" : "COLLSCAN", // 索引扫描方式
                             "filter" : { // 过滤条件
                                     "age" : {
                                             "$eq" : 1000
                                     }
                             },
                             "nReturned" : 1, // 返回结果集数目
                             "executionTimeMillisEstimate" : 0, // 预估的执行时间,毫秒
                             "works" : 10002, // 工作单元数,一个查询会被派生一些小的工作单元
                             "advanced" : 1, // 优先返回的结果数目
                             "needTime" : 10000,
                             "needYield" : 0,
                             "saveState" : 78,
                             "restoreState" : 78,
                             "isEOF" : 1,
                             "direction" : "forward", // 方向
                             "docsExamined" : 10000 // 文档检查数目
                     }
             },
             "serverInfo" : {
                     "host" : "DESKTOP-BSVSU4F",
                     "port" : 27017,
                     "version" : "4.1.6",
                     "gitVersion" : "55e72b015e2aa7297c00db29e4d93451ea61a7ca"
             },
             "ok" : 1
     }
     >
     ```

     ```javascript
     扫描方式:
     	collscan 全表扫描
         ixscan 索引扫描
         fetch 根据索引去检索指定 document
     ```

  2. 添加索引后查询

     ```javascript
     添加普通索引:
     	db.c1.createIndex({age:1});
     ```

     ```javascript
     > db.c1.find({age:1000}).explain('executionStats');
     {
             "queryPlanner" : {
                     "plannerVersion" : 1,
                     "namespace" : "test4.c1",
                     "indexFilterSet" : false,
                     "parsedQuery" : {
                             "age" : {
                                     "$eq" : 1000
                             }
                     },
                     "queryHash" : "3838C5F3",
                     "planCacheKey" : "041C5DE3",
                     "winningPlan" : {
                             "stage" : "FETCH", // 
                             "inputStage" : {
                                     "stage" : "IXSCAN",
                                     "keyPattern" : {
                                             "age" : 1
                                     },
                                     "indexName" : "age_1",
                                     "isMultiKey" : false,
                                     "multiKeyPaths" : {
                                             "age" : [ ]
                                     },
                                     "isUnique" : false,
                                     "isSparse" : false,
                                     "isPartial" : false,
                                     "indexVersion" : 2,
                                     "direction" : "forward",
                                     "indexBounds" : {
                                             "age" : [
                                                     "[1000.0, 1000.0]"
                                             ]
                                     }
                             }
                     },
                     "rejectedPlans" : [ ]
             },
             "executionStats" : {
                     "executionSuccess" : true,
                     "nReturned" : 1,
                     "executionTimeMillis" : 5,
                     "totalKeysExamined" : 1,
                     "totalDocsExamined" : 1,
                     "executionStages" : {
                             "stage" : "FETCH",
                             "nReturned" : 1,
                             "executionTimeMillisEstimate" : 0,
                             "works" : 2,
                             "advanced" : 1,
                             "needTime" : 0,
                             "needYield" : 0,
                             "saveState" : 0,
                             "restoreState" : 0,
                             "isEOF" : 1,
                             "docsExamined" : 1,
                             "alreadyHasObj" : 0,
                             "inputStage" : {
                                     "stage" : "IXSCAN",
                                     "nReturned" : 1,
                                     "executionTimeMillisEstimate" : 0,
                                     "works" : 2,
                                     "advanced" : 1,
                                     "needTime" : 0,
                                     "needYield" : 0,
                                     "saveState" : 0,
                                     "restoreState" : 0,
                                     "isEOF" : 1,
                                     "keyPattern" : {
                                             "age" : 1
                                     },
                                     "indexName" : "age_1",
                                     "isMultiKey" : false,
                                     "multiKeyPaths" : {
                                             "age" : [ ]
                                     },
                                     "isUnique" : false,
                                     "isSparse" : false,
                                     "isPartial" : false,
                                     "indexVersion" : 2,
                                     "direction" : "forward",
                                     "indexBounds" : {
                                             "age" : [
                                                     "[1000.0, 1000.0]"
                                             ]
                                     },
                                     "keysExamined" : 1,
                                     "seeks" : 1,
                                     "dupsTested" : 0,
                                     "dupsDropped" : 0
                             }
                     }
             },
             "serverInfo" : {
                     "host" : "DESKTOP-BSVSU4F",
                     "port" : 27017,
                     "version" : "4.1.6",
                     "gitVersion" : "55e72b015e2aa7297c00db29e4d93451ea61a7ca"
             },
             "ok" : 1
     }
     >
     ```

  3. 索引建立规则

     ```javascript
     为常做条件、排序、分组的字段建立索引
     选择唯一性索引
     选择较小的数据列，为较长的字符串使用前缀索引
     ```

     

####  权限机制

#####  开启验证服务

+ 什么是验证服务

  ```javascript
  名词,指用户需要输入账号密码才能登录使用
  ```

+ 操作步骤

  ```javascript
  1. 添加超级管理员
  2. 退出卸载服务
  3. 重新安装需要的输入账号密码的服务(在原安装命令基础上加上 --auth 即可)
  4. 启动服务 
  5. 登录测试
  ```

  1. 添加超级管理员

     ```javascript
     (windows+r后:)命令行: mongo
     
     // 使用 admin 数据库
     use admin;
     
     // 创建 User 语法
     db.createUser({
         user: "账号",
         pwd: "密码",
         roles: [{
             role: "角色",
             db: "所属数据库"
         }]
     });
     
     ---------------------------------- 失败 ----------------------------------------
      db.createUser(
         {
       user: "admisnbin",
         pwd: "scott",
         roles: [{
             role: "scott", // role 有特定选择, 自定会出错, role 第一次选择 root 切记
           db: "school" 
         }]
      }
     )
     
     erroInfomation:  [js] Error: couldn't add user: No role named scott@school
      
     ---------------------------------- 成功 ----------------------------------------
      db.createUser(
         {
           user: "xttblog",
             pwd: "test",
             roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
         }
      )
     
     
     输出信息:
     
         Successfully added user: {
                 "user" : "xttblog",
                 "roles" : [
                         {
                                 "role" : "userAdminAnyDatabase",
                                 "db" : "admin"
                         }
                 ]
         }
     
     
     ```

     + 角色

       ```javascript
       数据库用户角色：read、readWrite;
       数据库管理角色：dbAdmin、dbOwner、userAdmin；
       集群管理角色：clusterAdmin、clusterManager、clusterMonitor、hostManager；
       备份恢复角色：backup、restore；
       所有数据库角色：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase
       超级用户角色：root；这里还有几个角色间接或直接提供了系统超级用户的访问（dbOwner 、userAdmin、userAdminAnyDatabase）
       内部角色：__system
       ```

     + 对应作用

       ```javascript
       Read：允许用户读取指定数据库
       readWrite：允许用户读写指定数据库
       dbAdmin：允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问system.profile
       userAdmin：允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户
       clusterAdmin：只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限。
       readAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读权限
       readWriteAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读写权限
       userAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的userAdmin权限
       dbAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限。
       root：只在admin数据库中可用。超级账号，超级权限
       ```

     + 查看已创建用户角色信息

       ```javascript
       use admin;
       show collections; // 可能无显示
       // 上一步无显示信息无所谓直接执行下面的信息  admisnbin: replace your create user 
       db.system.users.find({user: "admisnbin"}).pretty()
       
       输出信息分析:
       
       {
               "_id" : "admin.admisnbin",
               "user" : "admisnbin",
               "db" : "admin",
               "credentials" : {
                       "SCRAM-SHA-1" : {
                               "iterationCount" : 10000,
                               "salt" : "G49EQwU5NnZ1aEZhPWNEJw==",
                               "storedKey" : "pxop//BnuC8/lZ4ipPFwu2B1oQQ=",
                               "serverKey" : "6zFNfZ8piyhjeHo4Q+jpIXvYNyY="
                       },
                       "SCRAM-SHA-256" : {
                               "iterationCount" : 15000,
                               "salt" : "k7C6yyGI70stIDG86Ia61aQIWwm2lEYJydnZ6w==",
                               "storedKey" : "zYqBWVBjgZVIwoR0ysiE1xWhwM08jIGa+VX2n+Bw3yg=",
                               "serverKey" : "IEVA9fZ1xGcBbEThhxRDjE2ECo4dNQ0P5Tca7t4HcTo="
                       }
               },
               "roles" : [
                       {
                               "role" : "dbAdmin",
                               "db" : "school"
                       }
               ]
       }
       >
       ```

       

  2. 退出卸载服务

     ```javascript
     windows+x: 超级管理员权限
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/powershell.png">

     ```javascript
     bin: mongod --remove
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/windowsPowershell.png">

  3.  安装需要身份验证的 `MongDB 服务`

      ```javascript
      bin目录下:  
      mongod --install --dbpath  
      "D:\Program Files\MongoDB\Server\4.1\data“ --logpath 
      "D:\ProgramFiles\MongoDB\Server\4.1\log\newMongodb" --auth
      
      
      解释: 
      	D:\Program Files\MongoDB\Server\4.1\data  # 安装 data 文件路径
      	D:\Program Files\MongoDB\Server\4.1\log\newMongodb # 安装日志文件路径
      	
      启动服务:
      	net start mongodb
      ```

  4.   验证安装

       ```bash
       > show dbs;
       2021-02-13T14:52:17.110+0800 E QUERY    [js] Error: listDatabases failed:{
               "ok" : 0,
               "errmsg" : "command listDatabases requires authentication",
               "code" : 13,
               "codeName" : "Unauthorized"
       } :
       _getErrorWithCode@src/mongo/shell/utils.js:25:13
       Mongo.prototype.getDBs@src/mongo/shell/mongo.js:124:1
       shellHelper.show@src/mongo/shell/utils.js:914:19
       shellHelper@src/mongo/shell/utils.js:804:15
       @(shellhelp2):1:1
       >
       
       # 【重新安装后:添加权限机制】不能直接显示 mongodb 下的数据库信息
       
       ```

5. 访问

   + 方法一

     ```bash
     mongo 服务器ip地址:端口/数据库 -u 用户名 -p 密码
     ```

     ```javascript
     # 之前创建的用户
     mongo 127.0.0.1:27017/admin -u xttblog -p test
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/createRole.png">

   + 方法二

     ```bash
     1. 先登录
     2. 选择数据库
     3. 输入 db.auth(用户名,密码)
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/useadmin.png">

   

#####  权限使用练习

+ 超级管理员权限用户

  ```javascript
  // userAdminAnyDatabase
  db.createUser({
      user: "root",
      pwd: "root",
      roles: [{
          role: "root", 
          db: "admin"
      }]
  });
          
  ```

  

  ```javascript
  use school;
  
  # 准本测试数据
  for (var i = 0; i < 10; i++) {
      db.stu.insert({
          stuname: "stu" + i,
          stuno: "stuno" + i,
          sex: "1"
      });
  }
  
  ```

  

1. 添加用户 `teacher1` 可以读取 `school `数据库

   ```javascript
   role:  read // 读取指定数据库
   
   db.createUser({
       user: "teacher1",
       pwd: "teacher1",
       roles: [{
           role: "read",
           db: "school"
       }]
   });
   
   ```

   

2.  添加用户 `teacher2` 可以读写 `school` 数据库

    ```javascript
    role: readWrite // 允许用户读写指定数据库
    
    db.createUser({
        user: "teacher2",
        pwd: "teacher2",
        roles: [{
            role: "readWrite",
            db: "school"
        }]
    });
    ```

    

####  备份还原

#####  备份

+ 语法

  ```bash
  mongodump -h -proot -u -p -d -o
  
  参数解释:
  	-h 		host 服务器 IP 地址(一般不写,默认本机)
  	-port 	端口 (一般不写,默认 27017)
  	-u user 账号
  	-p pwd 	密码
  	-d database 数据库(数据库不写则全局)
  	-o open 备份到指定目录下
  ```

  1. 备份`root`用户下所有数据

     ```bash
     mongodump -u root -p root -o  "D:\Program Files\MongoDB\Server\4.1\backupData"
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/backupAll.png">

  2. 备份指定数据库`school`

     ```bash
     # 删除备份 一 数据 D:\Program Files\MongoDB\Server\4.1\backupData --> D:\Program Files\MongoDB\Server\4.1\stuBackup
     mongodump -u teacher1 -p teacher1 -d school -o  "D:\Program Files\MongoDB\Server\4.1\backupData"
     ```

     <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/backupSchool.png">

#####  还原

+ 语法

  ```bash
  mongorestore -h -port -u -p -d --drop 备份数据目录
  
  -d 不写则还原全部数据
  --drop 先删除数据库在导入
  ```

+ 先备份数据库,在删除一些普通数据库, **`admin`一定要保留**

+ 删除数据库

  ```bash
  switched to db school
  > db.dropDatabase();
  { "dropped" : "school", "ok" : 1 }
  > show dbs;
  admin   0.000GB
  config  0.000GB
  local   0.000GB
  >
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/databaseInfo.png">

+ 数据库还原

  ```bash
  mongorestore -u root -p root --drop "D:\Program Files\MongoDB\Server\4.1\backupData"
  
  path: 必须放在最后
  
  ```

  <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/restore.png">

  + 查看是否还原

    ```bash
    mongo
    
    > use admin;
    switched to db admin
    > db.auth("root","root");
    1
    > show dbs;
    admin   0.000GB
    config  0.000GB
    local   0.000GB
    school  0.000GB
    >
    
    ```

  + 指定`school`数据库还原

    ```bash
    mongorestore -u teacher1 -p teacher1 -d school --drop "D:\Program Files\MongoDB\Server\4.1\stuBackup"
    ```

    

####  Mongoose 简介



#####  mongoose基础使用

+ `mongoose`是什么？

  ```bash
  是 node 中提供操作 MongoDB 的模块
  ```

+ 能干什么?

  ```bash
  能够通过 node 语法实现 MongoDB 数据库增删改查,从而实现用 node 写程序来管理 MongoDB 数据库
  ```

+ schema

  > 中文网: <a href="http://mongoosejs.com">schema 官网</a>
  >
  > 作用: 用来约束 MongoDB 文档数据(那些字段必须,那些字段可选)

+ 使用报错

  + `dos`窗口认证成功

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/mongoVs.png">

  + `vscode`使用报错

    ```bash
    // 导入模块
    const mongoose = require("mongoose");
    // 连接数据库
    const db = mongoose.createConnection(
      "mongodb://root:root@127.0.0.1:27017/school",
      // mongodb[协议]://user:password@host:port/database-name
      { useNewUrlParser: true, useUnifiedTopology: true },
      (err) => {
        if (err) {
          console.log("-------------------------------------");
          console.log("数据库连接失败: ", err);
          console.log("-------------------------------------");
        } else {
          console.log("数据库连接成功");
        }
      }
    );
    ```

    <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/authError.png">

    + 解决方案

      ```bash
      # mongodb://user:pwd@host/database-name?authSource=admin
      
      mongodb://root:root@127.0.0.1:27017/school?authSource=admin
      
      ```

    + 最终结果

      ```javascript
      // 导入模块
      const mongoose = require("mongoose");
      // 连接数据库
      mongoose
        .connect(
          // mongodb[协议]://user:password@host:port/database-name
          "mongodb://root:root@127.0.0.1:27017/school?authSource=admin",
          { useUnifiedTopology: true, useNewUrlParser: true }
        )
        .then(() => {
          console.log("---------------------------");
          console.log("数据库连接成功");
          console.log("---------------------------");
        })
        .catch((error) => {
          console.log("---------------------------");
          console.log("数据库连接失败: ", error);
          console.log("---------------------------");
        });
      
      // 创建集合规则
      const teacherSchema = new mongoose.Schema({
        // 教师: 课程 班级 上课周期 是否休假
        course: String,
        classroom: String,
        ontime: String,
        isSleep: Boolean,
      });
      
      // 使用规则创建集合 创建集合 Teacher，使用 teacherSchema 规则
      const Teacher = mongoose.model("Teacher", teacherSchema);
      // 创建集合实例
      const teacher = new Teacher({
        course: "node.js",
        classroom: "1801",
        ontime: "12:00",
        isSleep: true,
      });
      // 保存才能添加成功
      teacher.save();
      ```
      
      + 添加数据前
      
        <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/noCreateT.png">
      
      + 添加数据后
      
         <img src="https://gitee.com/wang_hong_bin/repo-bin/raw/master/TrueInsert.png">
#####  mongoDB数据库导入数据

+ 语法

  ```javascript
  mongoimport -d 数据库名称 -c 集合名称 --file 要导入的数据文件【json】
  ```



#####  增删改查

+ 前提条件

  ```javascript
  /***************************/
  // TODO: 连接mongoose和查询数据
  /***************************/
  
  
  // 导入模块
  const mongoose = require("mongoose");
  // 连接数据库
  mongoose
    .connect(
      // mongodb[协议]://user:password@host:port/database-name
      "mongodb://root:root@127.0.0.1:27017/school?authSource=admin",
      { useUnifiedTopology: true, useNewUrlParser: true }
    )
    .then(() => {
      console.log("---------------------------");
      console.log("数据库连接成功");
      console.log("---------------------------");
    })
    .catch((error) => {
      console.log("---------------------------");
      console.log("数据库连接失败: ", error);
      console.log("---------------------------");
    });
  
  // 创建集合规则
  const teacherSchema = new mongoose.Schema({
    // 教师: 课程 班级 上课周期 是否休假
    course: String,
    classroom: String,
    ontime: String,
    isSleep: Boolean,
  });
  
  ```

+ 查询`find`

  + `find`

    ```javascript
    
    // 使用规则创建集合 创建集合 Teacher，使用 teacherSchema 规则
    const Teacher = mongoose.model("Teacher", teacherSchema);
    // 查询集合的所有数据
    /*
    Teacher.find().then((result) => {
      console.log(result);
    });
    
    */
    // 根据条件查询 某一条数据
    Teacher.find({ _id: "6029d92dc0749738e8df4d62" }).then((result) => {
      console.log(result);
    });
    ```

  + `findOne`

    ```javascript
    // findOne 查找为第一条数据
    Teacher.findOne().then((result) => {
      console.log(result);
    });
    ```

  + 区别

    ```javascript
    // TODO: find 和 finOne 的区别: find 返回一组 [],findOne 返回一个
    
    ********************** find **************************
    [
      {
        _id: 6029d92dc0749738e8df4d62,
        course: 'node.js',
        classroom: '1801',
        ontime: '12:00',
        isSleep: true,
        __v: 0
      }
    ]
    ********************** findOne **************************
    {
      _id: 6029d5297f11ef1e1c60bb6f,
      course: 'node.js',
      classroom: '1801',
      ontime: '12:00',
      isSleep: true,
      __v: 0
    }
    
    ```

    

  + 范围查询

    ```javascript
    // 使用集合规则
    const Book = mongoose.model("Book", Books);
    
    
    // TODO: 范围查询 查询价格大于 8 的书籍信息
    Book.find({ price: { $gt: 8 } }).then((result) => {
      console.log("price大于8: ", result);
    });
    
    // TODO: 范围查询 查询价格大于等于 8 的书籍信息
    Book.find({ price: { $gte: 8 } }).then((result) => {
      console.log("price大于等于8: ", result);
    });
    
    // TODO: 范围查询 查询价格小于等于 8 的书籍信息
    Book.find({ price: { $lte: 8 } }).then((result) => {
      console.log("price小于等于8: ", result);
    });
    
    // TODO: 大于 5 小于 8 的书籍信息
    Book.find({ price: { $gt: 5, $lt: 8 } }).then((result) => {
      console.log("price大于5小于8: ", result);
    });
    
    // TODO: in [1,5,8] 的书籍信息 类似其他数据库的模块查询
    Book.find({ price: { $in: [1, 5, 8] } }).then((result) => {
      console.log("price 1 5 8: ", result);
    });
    
    ```

  + 字段查询

    ```javascript
    // select('字段名称一  字段名称二  -id[不查询 id 字段]') 字段名前面添加 “-”为不查询该字段
    
    Book.find().select('auth price -_id').then((result) => {
      console.log("查询字段: ", result);
    });
    
    结果输出:
    
        查询字段:  [
          { auth: 'tuling0', price: 0 },
          { auth: 'tuling1', price: 1 },
          { auth: 'tuling2', price: 2 },
          { auth: 'tuling3', price: 3 },
          { auth: 'tuling4', price: 4 },
          { auth: 'tuling5', price: 5 },
          { auth: 'tuling6', price: 6 },
          { auth: 'tuling7', price: 7 },
          { auth: 'tuling8', price: 8 },
          { auth: 'tuling9', price: 9 }
        ]
    ```

+ 删除文档

  + 删除一条

    ```javascript
    // TODO:查找到一条文档并且删除
    // 返回删除的文档 如果查询条件匹配了多个文档 那么将会删除第一个匹配的文档
    Book.findOneAndDelete({ price: 1 }).then((result) => {
      console.log("删除数据: ", result);
    });
    ```

  + 删除多条

    ```javascript
    
    // 删除多个文档 删除价格大于 7 书籍信息
    // TODO: 传递空对象会将整个文档删除，执行完毕返回结果为对象， { n: 2, ok: 1, deletedCount: 2 } n: 删除文档树 ok: 删除成功
    Book.deleteMany({ price: { $gt: 7 } }).then((result) => {
      console.log(result);
    });
    ```

+ 更新文档

  + 更新一条文档

    ```javascript
    // 根据条件更新一条文档 将价格为 2 的书籍价格更新为 22
    Book.updateOne({ price: 2 }, { price: 22 }).then((result) => {
      console.log(result); // { n: 1, nModified: 1, ok: 1 }
    });
    ```

  + 更新多条

    ```javascript
    // 更新多条 所有价格更改为 22
    Book.updateMany({}, { price: 22 }).then((result) => {
      console.log(result);
    });
    ```

  + 更新多值

    ```javascript
    // 多值更新
    Book.updateOne({ price: 2,auth:"value" }, { price: 22,auth: "new-value" }).then((result) => {
      console.log(result); 
    });
    
    ```

#####  Mongoose 验证

+ 验证

  ```javascript
  在创建集合规则,可以设置当前字段的验证规则,验证失败则就输出插入失败
  ```

+ 验证规则

  ```javascript
  ------------------------- message: system infomation ------------------------
  
  const CSchema = new mongoose.Schema({
    auth: {
      type: String,
      required: true, // 必填项，错误信息不友好
    },
  });
  
  ------------------------- message: self infomation ------------------------
   const CSchema = new mongoose.Schema({
    auth: {
      type: String, // 字符串应用规则
      required: [true, "请输入作者"], // [true,'message'] 自定义错误信息
  	minlength: 2, // 最小长度[2,'最小长度: 2']
      maxKength: 5, // 最大长度 [5,'最大长度为: 5']
      trim: true // 去除空格
    },
    age: {
      type: Number, // 数值类型应用规则
      min: 18, // 最小 18
      max: 100, // 最大 100
    },
    publishDate: {
      type: Date,
      default: Date.now, // 获取默认值 当前时间 命令行不可见,compass 工具可见
    },
    categories: {
      type: String,
      enum: ["java", "javascript", "javac"], // 自定义规则
    },
    rFn: {
      type: String,
      validate: {
        validator: (value) => {
          // 返回布尔值
          // true 验证成功
          // false 验证失败
          // value 要验证的值
          return value && value.lenght > 2; // 自定义规则
        },
        // 自定义错误信息
        message: "错误信息不符合验证规则"
      },
    }
  });
      
      
  ```

+ 获取验证错误信息

  ```javascript
  // 使用集合规则
  const Cschema = mongoose.model("Schma", CSchema);
  Cschema.create({ auth: "Nodejs", age: 23, categories: "javac", rFn: "bbc" })
    .then((result) => {
      console.log("成功: ", result);
    })
    .catch((error) => {
      // 获取错误对象
      const err = error.errors;
      // 循环错误信息对象
      for (let attr in err) {
        // 将错误信息打印到控制台
        console.log(err[attr]["message"]);
      }
    });
  
  ```

##### 集合关联

+ 集合关联

  ```javascript
  不同集合的数据之间是有关系的，例如文章信息和用户信息存储在不同集合中,但文章是某个用户发表的，要查询文章的所有信息包括发表用户,就需要用到集合关联。
  
  //外键？
  
  ```

+ 关联

  1. 使用 `_id`对集合进行关联
  2.  使用 `populate`方法进行关联集合查询

  ```javascript
  
  // 创建 User 规则
  const userSchema = new mongoose.Schema({
    name: { type: String, required: true },
  });
  // 创建 POST 规则
  const postSchema = new mongoose.Schema({
    title: { type: String },
    author: { type: mongoose.Schema.Types.ObjectId, ref: "User" }, // 将 id 作为 关联字段
  });
  
  // 使用规则 集合名称
  const User = mongoose.model("User", userSchema);
  const Post = mongoose.model("Post", postSchema);
  
  // 添加数据
  User.create({ name: "Node-User" }).then((result) => {
    console.log(result);
  });
  
  Post.create({ title: "Node-Post", author: "602a0b486925a224fcecf235" }).then(
    (result) => {
      console.log(result);
    }
  );
  ```

+ 关联查询

  ```javascript
  
  Post.find()
    .populate("author")
    .then((result) => {
      console.log(result);
    });
  
   /*
      [
    {
      _id: 602a0b624e405f43d860083a,
      title: 'Node-Post',
      author: { _id: 602a0b486925a224fcecf235, name: 'Node-User', __v: 0 },
      __v: 0
    }
  ]
  */
  ```

  

