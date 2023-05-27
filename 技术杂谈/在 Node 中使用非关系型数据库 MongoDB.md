---
title: 在 Node 中使用非关系型数据库 MongoDB
date: 2020-06-25 20:00
updated: 2020-06-25 20:00
cover: //cdn.wallleap.cn/img/pic/cover/202302dCEkfN.jpg
category: 技术杂谈
tags:
  - web
  - 后端
description: 在 Node 中使用非关系型数据库 MongoDB
---

MongoDB 是非关系型数据库的一种，相比起其他数据库而言，对前端开发者更友好

## 一、数据库简介

- 数据库是按照数据结构来组织、存储和管理数据的仓库
- 我们的程序都是在内存中运行的，一旦程序运行结束或者计算机断电，程序运行的数据都会丢失
- 所以我们就需要将一些程序运行的数据持久化到硬盘之中，以确保数据的安全性
- 说白了，数据库就是存储数据的仓库
- 数据库分类
  - 关系型数据库(RDBMS)
    - MySQL、Oracle、DB2、SQL Server……
    - 关系数据库中都是表
  - 非关系型数据库(No SQL  Not Only SQL)
    - MongoDB、Redis……
    - 键值对数据库
    - 文档数据库 MongoDB

## 二、MongoDB 简介

- MongoDB 是为快速开发互联网 Web 应用而设计的数据库系统

- MongoDB 的设计目标是极简、灵活、作为 Web 应用栈的一部分

- MongoDB 的数据模型是面向文档的，所谓文档是一种类似于 JSON 的结构，简单理解 MongoDB 这个数据库中存的是各种各样的 JSON（BSON）

- 三个概念

  - 数据库（database）：数据库是一个仓库，在仓库中可以存放集合
  - 集合（collection）：集合类似于数组，在集合中可以存放文档
  - 文档（document）：文档数据库中的最小单位，我们存储和操作的内容都是文档

- 下载 MongoDB

  - 下载地址：<https://www.mongodb.org/dl/win32/>
  - MongoDB 的版本偶数版本为稳定版，奇数版本为开发版
  - MongoDB 对于32位系统支持不佳，所以3.2版本以后没有再对32位系统的支持

- 安装 MongoDB

  - 安装

  - 配置环境变量 `D:\Program Files\MongoDB\Server\4.2\bin`

  - 在 C 盘根目录下创建 `data/db` 文件夹

  - 打开 cmd 命令行窗口

    - 输入 `mongod` 启动 MongoDB 服务器
    - 32位的初次启动需要输入 `mongod --storageEngine=mmapv1`

  - 再打开一个 cmd 窗口

    - 输入 `mongo` 连接 mongodb，出现`>`

  - 其他配置命令 `mongod --dbpath "D:\Program Files\MongoDB\Server\4.2\data\db --port 123"`

  - 数据库

    - 服务器用来保存数据，`mongod` 启动

    - 客户端用来操作服务器，对数据进行增删改查的操作，`mongo` 来启动

    - 需要打开两个窗口，我们可以将 MongoDB 设置为系统服务，可以自动在后台启动，不需要每次都手动启动

      - `C://data/` 创建 db、log 目录

      - 在 `D:\Program Files\MongoDB\Server\4.2` 下添加一个配置文件 `mongod.cfg`，配置文件中添加内容

        ```cfg
        systemLog:
         destination: file
         path: c:\data\log\mongod.log
        storage:
         dbPath: c:\data\db
        ```

      - 以管理员身份打开命令行窗口，输入命令 `sc.exe create MongoDB binPath="\"D:\Program Files\MongoDB\Server\4.2\bin\mongod.exe\" --service --config=\"D:\Program Files\MongoDB\Server\4.2\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"`，创建 MongoDB 服务
      - 启动 MongoDB 服务
      - 如果启动失败，则输入 `sc delete MongoDB` 删除服务之后，重新开始配置

## 三、MongoDB 的基本操作

在 MongoDB 中，数据库和集合都不需要我们手动创建，当我们创建文档时，如果文档所在的集合或数据库不存在则会自动创建数据库和集合

![](https://cdn.wallleap.cn/img/pic/illustration/1588908280549.png)

### 1、基本命令

- 显示当前的所有数据库
  - `show dbs`
  - `show databases`

- 进入到指定的数据库中
  - `use 数据库名`

- db 表示的是当前所处的数据库
  - `db`

- 显示数据库中所有的集合
  - `show collections`

### 2、数据库的 CRUD 操作

安装图形化工具：`MongodbManagerFree` 或 `Studio-3T`

- 向数据库中插入文档

  - `db.<collection>.insert(doc)` 向集合中插入一个或多个文档。当我们向集合中插入文档时，如果没有给文档指定 `_id` 属性，则数据库会自动为文档添加 `_id`，该属性用来作为文档的唯一标识，也可以自己指定，如果我们指定了，数据库就不会添加了，如果自己指定 `_id` 也必须确保它的唯一性

  ```js
  // 向test数据库中的stus集合中插入一个新的学生对象{name:"swk",age:18,gender:"man"}
  use test
  db.stus.insert({name:"swk",age:18,gender:"man"})
  db.stus.insert([
  {name:"shs",age:38,gender:"man"},
  {name:"bgj",age:18,gender:"female"},
  {name:"zbj",age:28,gender:"man"}
  ])
  ObjectId()  // 根据时间戳、机器码
  db.stus.insert({_id:"ts",name:"ts",age:18,gender:"man"})   // 建议不要自己指定
  ```

  - `db.<collection>.insertOne(doc)`  插入一个文档对象
  - `db.<collection>.insertMany(doc)`  插入多个文档对象
  - 这两个和上面的差不多，就是写开了更容易理解

  注：MongoDB 中的文档的属性值也可以是一个文档，当一个文档的属性值是文档时，我们称这为内嵌文档。

  MongoDB 支持直接通过内嵌文档的属性进行查询，如果要查询内嵌文档，可以通过 `.` 的形式来匹配。属性名必须用引号括起来

- 查询

  - `db.<collection>.find()` 查询当前集合中的所有的文档
    - `find()` 用来查询集合中所有符合条件的文档。在开发时，绝对不会执行不带条件的查询
    - `find()` 可以接受一个对象作为条件参数
      - `{}` 表示查询集合中所有的文档
      - `{字段名:值}` 查询属性是指定值的文档
        - 值还可以添加一个选项，多个条件之间使用 `,` 连接
        - `$eq` 等于
        - `$gt`、`$gte` 大于、大于等于
        - `$in`
        - `$lt`、`$lte`
        - `$ne`
        - `$nin`
        - `$or` 或
    - `find()` 返回的是一个数组
    - `db.stus.find({}).count()`返回对象个数，一般用这个；`db.stus.find({}).length()`
    - `db.stus.find().limit(10)` 设置显示数据的上限，这里表示只显示前十条数据
    - `db.numbers.find().skip(10).limit(10)` skip()用于跳过指定数量的数据，这里会显示第11~20条数据。MongoDB 会自动调整 skip 和 limit 的位置，因此顺序随便
  - `db.<collectin>.findOne()` 查询当前集合中符合条件的第一个文档
    - `findOne()` 返回的是一个文档对象

  ```js
  db.stus.find();
  db.stus.find({});
  db.stus.find({}).count();
  db.stus.find({}).length();
  db.stus.find({_id:"ts"});
  db.stus.find({age: 28,name:"zbj"});
  db.stus.find({age: 28})[1];
  db.stus.find({age:{$gt:20}})
  ```

- 修改

  - `db.<collectin>.update(查询条件,新对象[,配置选项])`
    - update()默认情况下回使用新对象来替换旧的对象
    - 如果需要修改指定的属性，而不是替换，需要使用“修改操作符”来完成修改
      - `$set` 可以用来修改文档中的指定属性
      - `$push`用于向数据中添加一个新的元素
      - `$addT0Set`向数据中添加一个新元素，如果数组中已经存在该元素，则不会添加
      - `$unset` 可以用来删除文档的指定属性
    - update()默认只会修改一个
  - `db.<collectin>.updateMany(查询条件,新对象)`  同时修改多个符合条件的文档
  - `db.<collectin>.updateOne(查询条件,新对象)`  修改一个符合条件的文档
  - `db.<collectin>.replace(查询条件,新对象)`   替换一个文档
  - 这三个也是将第一个分开了

  ```js
  db.stus.upadate({name:'shs'},{age:29}) // 替换
  db.stus.upadate({name:'shs'},{$set{age:29， address:"lsh"}) // 修改，默认值修改一个
  db.stus.upadate({name:'shs'},{$set{address:"lsh"})
  db.stus.upadate({name:'shs'},{$unset{age:29}) // 删除
  db.stus.upadate({name:'shs'},{$set{age:29， address:"lsh"}) // 添加配置项也可以修改多个
  ```

- 删除

  - `db.<collectin>.remove()`
    - remove()可以根据条件来删除文档，传递的条件的方式和find()一样
    - 删除符合条件的所有的文档，默认会删除多个
    - 如果remove()第二个参数传递一个true，则只会删除一个
    - 如果只传递一个空对象，则会删除所有的
  - `db.<collectin>.deleteOne()`
  - `db.<collectin>.deleteMany()`  
  - `db.collection.drop()` 删除集合
  - `db.dropDatabase()`删除数据库
  - 一般数据库中的数据都不会删除，所以删除的方法很少调用，一般在数据中添加一个字段，来表示数据是否被删除

  ```js
  db.stus.remove()
  db.stus.remove({})   // 清空集合（性能略差）
  db.stus.drop()     // 删除集合
  db.database()    // 删除数据库
  // 一般删除一个文档都是用这种方式
  db.stus.inert([
   {
    name: "ts",
    isDel: 0
   },
   {
    name: "zbj",
    isDel: 0
   },
   {
    name:"shs",
    isDel: 0
   }
  ])
  db.stus.updateOne({name:"ts"},{$et:{isDel:1}})
  db.stus.find({isDel:0})
  ```

## 四、文档之间的关系

- 一对一(One to One)

  - 夫妻（一个丈夫对应一个妻子）
  - 在 MongoDB 中，可以通过内嵌文档的形式来体现出一对一的关系

  ```js
  db.wifeAndHusband.insert([
   {
          name:"hr",
          husband:{
           name:"gj"
          }
   },{
          name:"pjl"
          husband:{
              name:"wdl"
          }
   }
  ])
  ```

- 一对多(One to Many)/多对一(Many to One)

  - 父母——孩子、用户——订单、文章——评论
  - 也可以通过内嵌文档来映射一对多的关系，属性变为数组

  ```js
  db.users.insert([
   {
    username:"swk"
   },{
    username:"zbj"
   }
  ])
  db.order.insert({
   list:["pg","xj","dyl"],
   user_id:ObjectId("swk_Id")
  })
  var user_idd = db.users.findOne({username:"swk"})._id
  db.order.find({user_id:user_idd})
  ```

- 多对多(Many to Many)

  - 分类——商品、老师——学生
  - 学生属于多个老师、老师教多个学生，学生中有一个老师的id，id多个用数组
  
  ```js
  db.teachers.insert([
   {
    name: 'hqg',
   },
   {
    name: 'hys',
   },
   {
    name: "gxr"
   }
  ])
  db.stus.insert([
   {
    name:"gj",
    tech_ids:[
     ObjectID('hqgID'),
     ObjectID("hysID")
    ]
   },
   {
    name:"swk",
    tech_ids: [
     ObjectID('hqgID'),
     ObjectID("hysID"),
     ObjectID("gxr")
    ]
   }
  ])
  db.teachers.find()
  db.stus.find()
  ```
  
## 五、sort 和投影

- `db.emp.find()` 查询文档时，默认情况是按照 `_id` 的值进行排列(升序)
- `db.emp.find({}).sort({sal:1})` sort() 可以用来指定文档的排序的规则，sort() 需要传递一个队形来指定排序的规则
  - `1` 表示升序
  - `-1` 表示降序
  - `db.emp.find({}).sort(sal:1, empno:-1)` 先按照 sal 升序排列，如果 sal 相同，按照 empno 降序排列
- 注：limit、skip、sort 书写顺序没有要求
- `db.emp.find({}, {ename:1})`在查询时，可以在第二个参数的位置来设置查询结果的投影 `db.emp.find({}, {ename: 1, _id: 0, sal: 1})`

## 六、Mongoose 简介

### 1、简介

- 之前我们都是通过 shell 来完成对数据库的各种操作的，在开发中大部分的时候我们都需要通过程序来完成对数据库的操作
- Mongoose 就是一个让我们可以通过 Node 来操作 MongoDB 的模块
- Mongoose 是一个对象文档模型(ODM)库，它对 Node 原生的 MongoDB 模块进行了进一步的优化封装，并提供了很多的功能
- 在大多数情况下，它被用来把结构化的模式应用到一个 MongoDB 集合，并提供了验证和类型转换等好处

### 2、Mongoose 好处

- 可以为文档创建一个模式结构（Schema）   ——约束
- 可以对模型中的对象/文档进行验证
- 数据可以通过类型转换转为对象模型
- 可以使用中间件来应用业务逻辑挂钩
- 比 Node 原生的 MongoDB 驱动更容易

### 3、新的对象

- Schema(模式对象)
  - 定义约束了数据库中的文档结构
- Model
  - Model 对象作为集合中所有文档的表示，相当于 MongoDB 数据库中的集合
- Document
  - Document 表示集合中的具体文档，相当于集合中的一个具体的文档

## 七、连接 MongoDB 数据库

1. 下载安装 Mongoose  `npm i mongoose --save`
2. 在项目中引入 Mongoose  `var mongoose = require("mongoose")`
3. 连接数据库  ` mongoose.connect('mongodb://数据库IP地址:端口号/数据库名'); `
   - 端口号如果是默认端口号(27017)，则可以省略不写
4. [可选] 监听 MongoDB 数据库的连接状态
   - 在 Mongoose 对象中，有一个属性叫做 connection，该对象表示的就是数据库连接通过监视该对象的状态，可以来监听数据库的连接与断开
     - `mongoose.connection.once("open",function(){})` 数据库连接成功的事件
     - `mongoose.connection.once("close",function(){})` 数据库断开的事件
5. 断开数据库连接(一般不需要调用) `mongoose.disconnect()`
   - MongoDB 数据库，一般情况下只需要连接一次，连接一次以后，除非项目停止、服务器关闭，否接连接一般不会断开

```js
// 例子
var mongoose = require("mongoose")
mongoose.connect("mongodb://127.0.0.1/mongoose_test")
mongoose.connection.once("open",function(){
 console.log("数据库已连接")
})
mongoose.connection.once("close",function(){
 console.log("数据库已断开")
})
mongoose.disconnect()
```

## 八、Schema、Model 和 Document

有了 Model，就可以对数据库进行增删改查的操作了

- `Model.crate(doc(s), [callback])`
  - 用来创建一个文档并添加到数据库中
  - `doc(s)`  可以是一个文档对象，也可以是一个文档对象的数组
  - `callback`  当操作完成之后调用的回调函数
- 查询
  - `Model.find(conditions, [projection], [options], [callback])` 查询所有符合条件的文档 总会返回一个数组
  - `Model.findById(id, [projection], options), [callback]` 根据文档的id属性查询文档
  - `Model.findOne([conditions], [projection], [options], [callback])` 查询符合条件的第一个文档  总会返回一个具体的对象
    - conditions 查询的条件
    - projection 投影  需要获取到的字段 两种方式
      - `{}`  对象，要的字段为1，不要的为0
      - `""` 字段名、不要的设为 `-`
    - options 查询选项（skip limit）
    - callback 回调函数，查询结果会通过回调函数返回，毁掉函数必须传，如果不传回调函数，压根不会查询
  - 通过 find() 查询的结果，返回的对象，就是 Document，文档对象
- 修改
  - `Model.update(conditions, doc, [options], [callback])`
  - `Model.updateMany(conditions, doc, [options], [callback])`
  - `Model.updateOne(conditions, doc, [options], [callback])`
    - 用来修改一个或多个文档
    - conditions 查询条件
    - doc 修改后的对象
    - options 配置参数
    - callback 回调函数
  - `Model.replaceOne(conditions, doc, [options], [callback])` 替换
- 删除(不用这个)
  - `Model.remove(conditions, [callback])`
  - `Model.deleteOne(conditions, [callback])`
  - `Model.deleteMany(conditions, [callback])`
- `Model.count(conditions, [callback])`
  - 统计文档的数量

Document 和集合中的文档一一对应，Document 是 Model 的实例，通过 Model 查询到结果都是 Document

Document 的方法

- `Model#save([options], [options.safe], [options.validateBeforeSave], [fn])`
- `update(update, [options], [callback])`
  - 修改对象
- `remove([callback])`
  - 删除对象(拒绝用这个)
- `get(name)`
  - 获取文档中的指定属性值
- `set(name, value)`
  - 设置文档的指定的属性值
- `id`
  - 获取文档的 `_id` 属性值
- `toJSON()`
  - 转换为一个 JSON 对象
- `toObject()`
  - 将 Document 对象转换为普通的 js 对象
  - 转换为普通的 js 对象以后，所有的 Document 对象的方法或属性都不能使用了
- 其他 `equals(doc)`  `isNew`  `isInit(path)`

```javascript
var mongoose = require("mongoose")
mongoose.connect("mongodb://127.0.0.1/mongoose_test", {useMongoClient:true})
// Schema对数据进行约束
// 将mongoose.Schema赋值给一个变量
var Schema = mongoose.Schema
// 创建Schema(模式)对象
var stuSchema = new Schema({
 name: String,
 age: Number,
 gender: {
     type: String,
        default: "male"
    },
 address: String
})

// Model 代表的是数据库中的集合，通过 Model 才能对数据库进行操作
// 通过 Schema 来创建 Model
// mongoose.model("要映射的集合名", 刚创建的Schema对象) Mongoose 会自动将集合名变为复数
var StuModel = mongoose.model("student", stuSchema)
// 向数据库中出入一个文档 model.create(文档, 回调函数)
stuModel.create({
    name: 'swk',
    age: 18,
    gender: 'male',
    address: "hgs"
}, function(err){
    if(!err){
        console.log("插入成功")
    }
})
stuModel.create([{
    name: 'shs',
    age: 28,
    gender: 'male',
    address: "lsh"
},{
    name: "bgj",
    age: 17,
    gender: "female",
    address: "bgd"
}], function(err){
    if(!err){
        console.log("插入成功")
    }
})

// 查询
StuModel.find({name:"shs"},function(err, docs){
    if(!err){
        console.log(docs)
        console.log(docs[0].name)
    }
})
/* StuModel.find({name:"shs"},{name:1, _id:0},function(err, docs){
    if(!err){
        console.log(docs)
    }
}) */
StuModel.find({name:"shs"},"name -_id",function(err, docs){
    if(!err){
        console.log(docs)
    }
})
StuModel.find({name:"shs"},"name -_id",{skip:3, limit:1},function(err, docs){
    if(!err){
        console.log(docs)
    }
})
StuModel.findOne({}, function(err, doc){
    if(!err){
        console.log(doc.name)
    }
})
StuModel.findById("...",function(err,doc){
    if(!err){
        console.log(doc)
    }
})

// Document对象是Model的实例
/* StuModel.findById("...",function(err,doc){
    if(!err){
        console.log(doc instantceof StuModel)
    }
})
 */

StuModel.updateOne({name: 'ts'}, {$set:{age:20}},function(err){
    if(!err){
        console.log("修改成功")
    }
})

StuModel.remove({name:"bgj"}, function(err){
    if(!err){
        console.log("删除成功")
    }
})

StuModel.count({}, function(err, count){
    if(!err){
        console.log(count)
    }
})

// 创建一个Document
var stu = new StuModel({
    name: "blm",
    age: 14,
    gender: "male",
    address: "bbt"
})
stu.save(function(err){
    if(!err){
        console.log("保存成功")
    }
})
StuModel.findOne({}, function(err, doc){
    if(!err){
        /* doc.update({$set:{age: 28}}, function(err){
            if(!err){
                console.log("修改成功")
            }
        }) */
        doc.age = 28
        save()
        
        /* doc.remove(function(err){
            if(!err){
                console.log("删除成功")
            }
        }) */
        // console.log(doc.get("age"))
        console.log(doc.age)
        // doc.set("name", "zhu")
        doc.name = "zhu"
        // console.log(doc.id)
        console.log(doc._id)
        console.log(doc.toJSON())
        doc = doc.toObject()
        delete doc.address
        console.log(doc)
    }
})
```

## 九、Mongoose 的模块化

定义一个模块，用来连接 MongoDB 数据库

```javascript
// conn_mongo.js
var mongoose = require("mongoose")
mongoose.connect("mongodb://127.0.0.1/mongoose_test")
```

定义一个 student 的模型，几个模型就可以创建几个 js 文件

```javascript
// student.js
var mongoose = require("mongoose")
var Schema = mongoose.Schema
var stuSchema = new Schema({
 name: String,
 age: Number,
 gender: {
     type: String,
        default: "male"
    },
 address: String
})
var StuModel = mongoose.model("student", stuSchema)
// exports.model = StuModel
module.exports = StuModel
```

其他地方引入

```javascript
require("./conn_mongo")
// var Student = require("./models/student").model
var Student = require("./models/student")
Student.find({}, function(err, docs){
    if(!err){
        console.log(docs)
    }
})
```

## 练习

````js
//1.进入my_test数据库
use my_test

//2.向数据库的 user 集合中插入一个文档  
db.users.insert({
    username:"sunwukong"
});

//3.查询user集合中的文档
db.users.find();

//4.向数据库的user集合中插入一个文档   
db.users.insert({
    username:"zhubajie"
});
   
//5.查询数据库user集合中的文档
db.users.find();

//6.统计数据库user集合中的文档数量
db.users.find().count();

//7.查询数据库user集合中username为sunwukong的文档
db.users.find({username:"sunwukong"});

//8.向数据库user集合中的username为sunwukong的文档，添加一个address属性，属性值为huaguoshan
db.users.update({username:"sunwukong"},{$set:{address:"huaguoshan"}});


//9.使用{username:"tangseng"} 替换 username 为 zhubajie的文档
db.users.replaceOne({username:"zhubajie"},{username:"tangseng"});    
    
//10.删除username为sunwukong的文档的address属性
db.users.update({username:"sunwukong"},{$unset:{address:1}});


//11.向username为sunwukong的文档中，添加一个hobby:{cities:["beijing","shanghai","shenzhen"] , movies:["sanguo","hero"]}
//MongoDB的文档的属性值也可以是一个文档，当一个文档的属性值是一个文档时，我们称这个文档叫做 内嵌文档
db.users.update({username:"sunwukong"},{$set:{hobby:{cities:["beijing","shanghai","shenzhen"] , movies:["sanguo","hero"]}}});
db.users.find();

//12.向username为tangseng的文档中，添加一个hobby:{movies:["A Chinese Odyssey","King of comedy"]}
db.users.update({username:"tangseng"},{$set:{hobby:{movies:["A Chinese Odyssey","King of comedy"]}}})

//13.查询喜欢电影hero的文档
//MongoDB支持直接通过内嵌文档的属性进行查询，如果要查询内嵌文档则可以通过.的形式来匹配
//如果要通过内嵌文档来对文档进行查询，此时属性名必须使用引号 
db.users.find({'hobby.movies':"hero"});

//14.向tangseng中添加一个新的电影Interstellar
//$push 用于向数组中添加一个新的元素
//$addToSet 向数组中添加一个新元素 ， 如果数组中已经存在了该元素，则不会添加
db.users.update({username:"tangseng"},{$push:{"hobby.movies":"Interstellar"}});
db.users.update({username:"tangseng"},{$addToSet:{"hobby.movies":"Interstellar"}});
db.users.find();

//15.删除喜欢beijing的用户
db.users.remove({"hobby.cities":"beijing"});

//16.删除user集合
db.users.remove({});
db.users.drop();

show dbs;

//17.向numbers中插入20000条数据 7.2s
for(var i=1 ; i<=20000 ; i++){
    db.numbers.insert({num:i});
}

db.numbers.find()

db.numbers.remove({});


//0.4s
var arr = [];

for(var i=1 ; i<=20000 ; i++){
    arr.push({num:i});
}

db.numbers.insert(arr);


//18.查询numbers中num为500的文档
db.numbers.find({num:500})

//19.查询numbers中num大于5000的文档
db.numbers.find({num:{$gt:500}});
db.numbers.find({num:{$eq:500}});

//20.查询numbers中num小于30的文档
db.numbers.find({num:{$lt:30}});

//21.查询numbers中num大于40小于50的文档
db.numbers.find({num:{$gt:40 , $lt:50}});

//22.查询numbers中num大于19996的文档
db.numbers.find({num:{$gt:19996}});

//23.查看numbers集合中的前10条数据
db.numbers.find({num:{$lte:10}});

//limit()设置显示数据的上限
db.numbers.find().limit(10);
//在开发时，我们绝对不会执行不带条件的查询
db.numbers.find();

//24.查看numbers集合中的第11条到20条数据
/*
    分页 每页显示10条
        1-10     0
        11-20    10
        21-30    20
        。。。
        
        skip((页码-1) * 每页显示的条数).limit(每页显示的条数);
        
    skip()用于跳过指定数量的数据    
    
    MongoDB会自动调整skip和limit的位置
*/
db.numbers.find().skip(10).limit(10);

//25.查看numbers集合中的第21条到30条数据
db.numbers.find().skip(20).limit(10);

db.numbers.find().limit(10).skip(10);

//26.将dept和emp集合导入到数据库中
db.dept.find()
db.emp.find()

//27.查询工资小于2000的员工
db.emp.find({sal:{$lt:2000}});

//28.查询工资在1000-2000之间的员工
db.emp.find({sal:{$lt:2000 , $gt:1000}});

//29.查询工资小于1000或大于2500的员工
db.emp.find({$or:[{sal:{$lt:1000}} , {sal:{$gt:2500}}]});

//30.查询财务部的所有员工
//(depno)
var depno = db.dept.findOne({dname:"财务部"}).deptno;
db.emp.find({depno:depno});

//31.查询销售部的所有员工
var depno = db.dept.findOne({dname:"销售部"}).deptno;
db.emp.find({depno:depno});

//32.查询所有mgr为7698的所有员工
db.emp.find({mgr:7698})

//33.为所有薪资低于1000的员工增加工资400元
db.emp.updateMany({sal:{$lte:1000}} , {$inc:{sal:400}});
db.emp.find()
````
