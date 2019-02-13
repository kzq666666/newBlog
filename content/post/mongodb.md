---
title: "Mongodb"
date: 2018-12-11T16:06:49+08:00
showDate: true
draft: false
tags: ["数据库","非关系型","MongoDb"]
---
在学习node的时候，进行连接数据库相关操作，于是就学习了一下mongodb非关系型数据库。
<br>mongodb操作的都是对象

### 基本命令汇总
```bash
show dbs    显示所有的数据库
show tables 显示当前数据库下的所有表
db          显示当前数据库
use mydb    切换到mydb数据库，如果没有则创建mydb数据库
db.stu.insert({})   向stu表中插入数据，如果没有stu则创建一个stu表
db.stu.find()   显示stu表下的所有数据
db.stu.find({条件1},{条件2})  查找满足条件1且条件2的数据
db.stu.find({$or:[{条件1},{条件2}]})  查找满足条件1或条件2的数据
db.stu.find({age:{$gte:10,$lte:20}})    查询stu表中age大于等于10并且小于等于20的数据
```
