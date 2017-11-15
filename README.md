Demos for [mongoDB 入门篇](http://www.imooc.com/learn/295)
# mongoDB 入门篇
## 一. 数据库基本概念
### 1-1 mongoDB 现状
1. mongoDB 特点
    - 免费
    - 开源
    - 技术支持
    
### 1-2 课程简介

### 1-3 MongoDB 相关网站介绍
    
### 1-4 关于数据库
1. 数据库概念
    - 有组织地存放数据
    - 按照不同的需求进行查询
    
2. 数据库分类
    - 按是否支持 SQL 语言分类
        - SQL 数据库, eg. MySQL, Oracle
        - NoSQL(Not Only SQL) 数据库, eg. Redis, MongoDB
        
    - SQL 与 NoSQL 数据库对比
    
        SQL 数据库 | NoSQL 数据库
        :-------: | :----------:
        实时一致性 | 最终一致性 
        事务      | Redis支持部分事务, MongoDB不支持事务
        多表联合查询 | 不支持多表联合查询
        
### 1-5 Why MongoDB ?
1. 无数据结构的限制
    - 没有表结构的概念, 每条记录可以有完全不同的结构
    - 业务开发方便快捷
    - SQL 数据库需要事先定义表结构再使用, 而 MongoDB 没有这个必要
    
2. 完全的索引支持
    - 单键索引, 多键索引
    - 数组索引
    - 全文索引
    - 地理位置索引
    
3. 方便的冗余与扩展
    - 复制集保证数据安全
    - 分片扩展数据规模
    
4. 良好的支持
    - 完善的文档
    - 齐全的驱动支持
    
## 二. MongoDB 的安装与配置
### 2-1 MongoDB 运行环境简介

### 2-2 编译 MongoDB 文件
1. MongoDB 常用组件
    - mongod
    - mongo
    - mongoimport
    - mongoexport
    - mongodump
    - mongorestore
    - mongooplog
    - mongostat
    
### 2-3 搭建简单的 MongoDB 服务器

### 2-4 连接 MongoDB 服务器

## 三. MongoDB 基本使用
`[Mongo Shell Methods Reference](https://docs.mongodb.com/manual/reference/method/)`

### 3-1 MongoDB 的基本操作之写入数据和查询数据
1. 查看数据库和集合信息
    ```
    show dbs
    show collections
    ```
    
2. 插入
    ```
    use imooc
    db.imooc_collection.insert({x:100})
    ```
    
3. 查询所有
    ```
    use imooc
    db.imooc_collection.find()
    ```
    
4. 条件查询
    ```
    use imooc
    db.imooc_collection.find({x:100})
    ```
    
5. 查询筛选
    ```
    use imooc
    db.imooc_collection.find().skip(3).limit(2).sort({x:1})
    ```
    
### 3-2 MongoDB 的基本操作之更新单条数据
1. 全部更新
    ```
    db.imooc_collection.find({x:1})
    db.imooc_collection.update({x:1}, {x:999})
    ```
    
2. 部分更新, 使用 `$` 操作符
    ```
    db.imooc_collection.insert({x:100,y:100,z:100})
    db.imooc_collection.update({z:100},{$set:{y:99}})
    ```
    
### 3-3 MongoDB 的基本操作之更新不存在的数据
1. update 方法的第三个参数 `upsert` 表示 `未找到匹配时是否插入新记录`, 默认为 false; 将其置为 true, 则更新的数据未匹配时, 就自动插入这条数据
    ```
    db.imooc_collection.find({y:999})   // 不存在
    db.imooc_collection.update({y:100},{y:999},true)
    db.imooc_collection.find({y:999})   // 已经插入
    ```
    
### 3-4 MongoDB 的基本操作之更新多条数据
1. MongoDB 中 Update 方法默认只会更新第一条符合条件的数据, 为了防止误操作
    ```
    // 插入 3 条相同数据
    for(i=0;i<3;++i) db.imooc_collection.insert({c:1})
    db.imooc_collection.find({c:1})
    // update 默认只更新一条数据
    db.imooc_collection.update({c:1},{c:2})
    db.imooc_collection.find({c:2})
    ```
    
2. update 方法的第四个参数 `multi` 表示 `是否更新满足查询条件的多条记录`, 默认为 false; 将其置为 true 即可更新多条数据, 需要注意更新多条数据时, 只能使用 `$` 操作符
    ```
    db.imooc_collection.update({c:1}, {$set:{c:2}}, false, true)
    db.imooc_collection.find({c:2}) // 成功更新多条数据
    ```
    
### 3-5 MongoDB 的基本操作之删除数据
1. 删除档案, 使用 `remove` 方法, 默认删除所有满足条件的档案
    ```
    db.imooc_collection.find({c:2})
    db.imooc_collection.remove({c:2})
    ```
    
2. 删除集合, 使用 `drop` 方法
    ```
    db.imooc_collection.drop()
    show collections
    ```
    
### 3-6 MongoDB 的基本操作之创建索引
1. 查看集合索引, 使用 `getIndexes` 方法
    ```
    db.imooc_collection.getIndexes()
    ```
    
2. 使用 `createIndex` 方法可以创建索引
    ```
    db.imooc_collection.createIndex({x:1})
    ```
    
## 四. MongoDB 常见的查询索引
    
    
    

