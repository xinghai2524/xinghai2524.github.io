## 前言

关于NoSql数据库，这是一个非关系型数据库，优点在于它使用键值对存储数据，相比于关系型数据库用表结构存储的数据库，NoSql更加适用于数据的结构不固定的场景，更适用于Web开发

NoSql表示的是非关系型数据库，其代表产品有很多

![image-20240812210229084](https://db.xinghai.ink/Typora/17349911585442345.png)

**其中MongoDB是最像关系型数据库的非关系型数据库**

-   MongoDB是一个流行的开源文档型数据库，它使用类似 JSON 的文档模型存储数据，这使得数据存储变得非常灵活。
-   MongoDB 是一个基于文档的 NoSQL 数据库，由 MongoDB Inc. 开发。
-   MongoDB 旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。
-   MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能

**MongoDB 的一些关键特点：**

-   **文档导向**：MongoDB 存储 BSON（二进制 JSON）文档，这些文档可以包含复杂的数据结构，如数组和嵌套对象。
-   **高性能**：MongoDB 提供了高性能的数据持久化和查询能力，特别是对于写入密集型的应用。
-   **水平扩展**：通过分片（sharding）技术，MongoDB 可以在多个服务器之间分布数据，实现水平扩展。
-   **高可用性**：MongoDB 支持副本集（replica sets），提供数据的自动故障转移和数据冗余。
-   **灵活的聚合框架**：MongoDB 提供了一个强大的聚合框架，允许执行复杂的数据处理和聚合操作。
-   **丰富的查询语言**：MongoDB 的查询语言（MQL）支持丰富的查询操作，包括文本搜索、地理位置查询等。
-   **存储过程**：MongoDB 支持在数据库内部执行 JavaScript 代码，允许定义和执行复杂的数据处理逻辑。
-   **GridFS**：对于存储大于 BSON 文档大小限制（16MB）的文件，MongoDB 提供了 GridFS，一种用于存储和检索大文件的规范。
-   **安全性**：MongoDB 提供了多层次的安全特性，包括认证、授权和加密。
-   **驱动程序和工具**：MongoDB 拥有广泛的驱动程序支持，适用于不同的编程语言，以及各种管理工具和可视化界面。
-   **社区和生态系统**：MongoDB 拥有一个活跃的开发者社区，提供了大量的教程、文档和第三方工具。

## 安装启动MongoDB

关于安装MongoDB可以参照[官方文档](https://www.mongodb.com/zh-cn/docs/manual/)

具体步骤不在演示

安装好之后输入命令

```shell
xinghai@24fb83e097e2:/$ mongo
Command 'mongo' not found, did you mean:
  command 'mono' from deb mono-runtime (6.8.0.105+dfsg-3.5ubuntu1)
Try: sudo apt install <deb name>
xinghai@24fb83e097e2:/$
```

如果返回的是上面的结果，那就说明安装成功了

### 启动MongoDB

启动MongoDB分为前台启动、后台启动、配置文件启动

**启动命令**

```shell
mongod --dbpath <dbpath> --logpath <logpath_name> --port 27017 --bind_ip 0.0.0.0 [--fork]
```

参数解释

-   mongod，这个是mongo的服务端程序
-   --dbpath，这个代表数据库再本地文件系统的存放位置
-   --logpath，这个表示运行日志的存放位置，这个需要指定具体的文件
-   --port，指定默认端口，但端口还是要以具体的为准
-   --bind_ip，指定那些ip可以连接数据库，0.0.0.0表示不限制ip
-   --fork，以守护进程的方式启用，就是后台运行

**停止命令**

```shell
mongod --dbpath <dbpath> --logpath <logpath_name> --port 27017 --bind_ip 0.0.0.0 [--fork] --shutdown
```

结束命令需要在启动命令后面加上shutdown

**示例**

```shell
xinghai@002eb7d27e70:~$ mongod --dbpath /home/xinghai/data/db --logpath /home/xinghai/data/log/db.log --fork
about to fork child process, waiting until server is ready for connections.
forked process: 5683
child process started successfully, parent exiting
xinghai@002eb7d27e70:~$ mongosh
Current Mongosh Log ID: 66bc1c6bc93a690bcd838725
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.2.15
Using MongoDB:          7.0.12
Using Mongosh:          2.2.15

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

------
   The server generated these startup warnings when booting
   2024-08-14T10:54:30.146+08:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
   2024-08-14T10:54:30.146+08:00: This server is bound to localhost. Remote systems will be unable to connect to this server. Start the server with --bind_ip <address> to specify which IP addresses it should serve responses from, or with --bind_ip_all to bind to all interfaces. If this behavior is desired, start the server with --bind_ip 127.0.0.1 to disable this warning
   2024-08-14T10:54:30.147+08:00: /sys/kernel/mm/transparent_hugepage/enabled is 'always'. We suggest setting it to 'never' in this binary version
   2024-08-14T10:54:30.147+08:00: Soft rlimits for open file descriptors too low
------

test> exit
xinghai@002eb7d27e70:~$ mongod --dbpath /home/xinghai/data/db --logpath /home/xinghai/data/log/db.log --shutdown
{"t":{"$date":"2024-08-14T02:55:28.080Z"},"s":"I",  "c":"CONTROL",  "id":20697,   "ctx":"main","msg":"Renamed existing log file","attr":{"oldLogPath":"/home/xinghai/data/log/db.log","newLogPath":"/home/xinghai/data/log/db.log.2024-08-14T02-55-28"}}
Killing process with pid: 5683
xinghai@002eb7d27e70:~$ mongosh
Current Mongosh Log ID: 66bc1ca30f5edcd90a838725
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.2.15
MongoNetworkError: connect ECONNREFUSED 127.0.0.1:27017
xinghai@002eb7d27e70:~$
```

### 以配置文件的形式启动

使用命令行的方式设置配置非常的繁琐，可以将配置文件写在一个文件当中，然后根据这个文件启动和停止mongod程序

写入配置到文件，这里的文件名是db

```shell
dbpath = /home/xinghai/data/db
logpath = /home/xinghai/data/log/db.log
logappend = true
port = 27017
bind_ip = 0.0.0.0
fork = true
```

运行**mongod**

```shell
xinghai@002eb7d27e70:~$ mongod -f ./db --fork
about to fork child process, waiting until server is ready for connections.
forked process: 5760
child process started successfully, parent exiting
xinghai@002eb7d27e70:~$ mongosh
Current Mongosh Log ID: 66bc1da6f00a08a4b9838725
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.2.15
Using MongoDB:          7.0.12
Using Mongosh:          2.2.15

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

------
   The server generated these startup warnings when booting
   2024-08-14T10:59:46.150+08:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
   2024-08-14T10:59:46.150+08:00: /sys/kernel/mm/transparent_hugepage/enabled is 'always'. We suggest setting it to 'never' in this binary version
   2024-08-14T10:59:46.150+08:00: Soft rlimits for open file descriptors too low
------

test> exit
xinghai@002eb7d27e70:~$ mongod -f ./db --shutdown
Killing process with pid: 5760
xinghai@002eb7d27e70:~$ mongosh
Current Mongosh Log ID: 66bc1db793dda24c86838725
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.2.15
MongoNetworkError: connect ECONNREFUSED 127.0.0.1:27017
xinghai@002eb7d27e70:~$
```

## 基本概念

| SQL 术语/概念 | MongoDB 术语/概念 | 解释/说明                           |
| :------------ | :---------------- | :---------------------------------- |
| database      | database          | 数据库                              |
| table         | collection        | 数据库表/集合                       |
| row           | document          | 数据记录行/文档                     |
| column        | field             | 数据字段/域                         |
| index         | index             | 索引                                |
| table joins   |                   | 表连接,MongoDB不支持                |
| primary key   | primary key       | 主键,MongoDB自动将_id字段设置为主键 |

**完整术语列表：**

-   **文档（Document）**：MongoDB 的基本数据单元，通常是一个 JSON-like 的结构，可以包含多种数据类型。（结构相当于python字典，相当于mysql的一行记录）
-   **集合（Collection）**：类似于关系型数据库中的表，集合是一组文档的容器。在 MongoDB 中，一个集合中的文档不需要有一个固定的模式。
-   **数据库（Database）**：包含一个或多个集合的 MongoDB 实例。
-   **BSON**：Binary JSON 的缩写，是 MongoDB 用来存储和传输文档的二进制形式的 JSON。
-   **索引（Index）**：用于优化查询性能的数据结构，可以基于集合中的一个或多个字段创建索引。
-   **分片（Sharding）**：一种分布数据到多个服务器（称为分片）的方法，用于处理大数据集和高吞吐量应用。
-   **副本集（Replica Set）**：一组维护相同数据集的 MongoDB 服务器，提供数据的冗余备份和高可用性。
-   **主节点（Primary）**：副本集中负责处理所有写入操作的服务器。
-   **从节点（Secondary）**：副本集中的服务器，用于读取数据和在主节点故障时接管为主节点。
-   **MongoDB Shell**：MongoDB 提供的命令行界面，用于与 MongoDB 实例交互。
-   **聚合框架（Aggregation Framework）**：用于执行复杂的数据处理和聚合操作的一系列操作。
-   **Map-Reduce**：一种编程模型，用于处理大量数据集的并行计算。
-   **GridFS**：用于存储和检索大于 BSON 文档大小限制的文件的规范。
-   **ObjectId**：MongoDB 为每个文档自动生成的唯一标识符。
-   **CRUD 操作**：创建（Create）、读取（Read）、更新（Update）、删除（Delete）操作。
-   **事务（Transactions）**：从 MongoDB 4.0 开始支持，允许一组操作作为一个原子单元执行。
-   **操作符（Operators）**：用于查询和更新文档的特殊字段。
-   **连接（Join）**：MongoDB 允许在查询中使用 `$lookup` 操作符来实现类似 SQL 的连接操作。
-   **TTL（Time-To-Live）**：可以为集合中的某些字段设置 TTL，以自动删除旧数据。
-   **存储引擎（Storage Engine）**：MongoDB 用于数据存储和管理的底层技术，如 WiredTiger 和 MongoDB 的旧存储引擎 MMAPv1。
-   **MongoDB Compass**：MongoDB 的图形界面工具，用于可视化和管理 MongoDB 数据。
-   **MongoDB Atlas**：MongoDB 提供的云服务，允许在云中托管 MongoDB 数据库。

## 查看数据库

-   使用mongosh进入mongo的终端，mondosh是用户和mongo数据库交互的窗口，终端里面可以使用javascript语句
-   如果在操作数据库时，没有指定数据库，系统会默认的使用一个名为test的数据库，该数据库存储在data目录中

**查看所有数据库**

```
show dbs
```

**示例**

```
test> show dbs
admin   40.00 KiB
config  96.00 KiB
local   72.00 KiB
test>
```

------

**查看操作数据库**

可以使用`db`命令查看正在操作的数据库，当然在>前面也可以直接看到

```shell
db
```

**示例**

```
local> db
local
local> use test
switched to db test
test> db
test
test>
```

## 创建数据库

在mongodb数据库当中创建数据库是自动完成的，当插入数据到数据库当中，或者选择数据库时，如果数据库不存在，就会自动床创建一个

### **指定数据库**

```
use database_name
```

**示例**

```
test> db
test
test> use local
switched to db local
local> use test
switched to db test
test> use aaa
switched to db aaa
aaa> db
aaa
aaa>
```

可以发现就算数据库不存在也可以指定数据库，其实是应为会自动创建

但是我们如果使用show dbs就会发现aaa这个数据库不存在

```
aaa> show dbs
admin   40.00 KiB
config  96.00 KiB
local   72.00 KiB
aaa>
```

不只是aaa，系统默认的数据库test也不存在，这是因为，如果数据库没有数据的话，是不会显示出来的，没有数据的数据库就相当于不存在

可以插入一些数据，这样数据库就可见了

```
aaa> db.aaa.insertOne({"name":"菜鸟"})
{
  acknowledged: true,
  insertedId: ObjectId('66bc3f1f7e6fa0d69b838726')
}
aaa> show dbs
aaa     40.00 KiB
admin   40.00 KiB
config  96.00 KiB
local   72.00 KiB
```

### **创建集合**

创建数据库后通常要创建集合以存储文档

```
db.createCollection("myNewCollection")
```

-   db.createcollection,他会在当前数据库当中创建集合
-   mynewCollection，表示集合名称

示例

```shell
aaa> db.createCollection("myNewCollection")
{ ok: 1 }
aaa>
```

### **删除数据库**

选中数据库，然后就可以通过命令删除当前的数据库

```
db.dropDatabase()
```

**示例**

```
aaa> db.dropDatabase()
{ ok: 1, dropped: 'aaa' }
aaa> show dbs
admin   40.00 KiB
config  96.00 KiB
local   72.00 KiB
aaa>
```

### 注意事项

-   数据库名不能包含空格、点（.）或美元符号（$）。
-   数据库的创建是自动的，不需要显式创建，除非你需要在创建时指定特定的配置选项。
-   在MongoDB中，只有在数据库中至少有一个集合时，数据库才会在 `show dbs` 命令的输出中显示。

## 删除数据库

MongoDB 删除数据库的语法格式如下：

```
db.dropDatabase()
```

删除当前数据库，默认为 test，你可以使用 db 命令查看当前数据库名

**示例**

首先需要创建一个集合

```
abc> show dbs	//查看数据库列表
admin    40.00 KiB
config  108.00 KiB
local    72.00 KiB
test> use ttt	//切换到ttt，相当于创建ttt数据库
switched to db ttt
ttt> db.createCollection("myCollection")	//创建集合
{ ok: 1 }
ttt> show collections	//查看数据库集合
myCollection
ttt> show dbs	//查看数据库列表
admin    40.00 KiB
config  108.00 KiB
local    72.00 KiB
ttt       8.00 KiB
ttt> use test
switched to db test
test>
```

然后删除这个集合

```
test> show dbs	//查看列表
abc      40.00 KiB
admin    40.00 KiB
config  108.00 KiB
local    72.00 KiB
test> use abc	//选择数据库
switched to db abc
abc> db.dropDatabase()	//删除数据库
{ ok: 1, dropped: 'abc' }
abc> show dbs	//查看列表
admin    40.00 KiB
config  108.00 KiB
local    72.00 KiB
abc>
```

## 创建集合

MongoDB 中使用 **createCollection()** 方法来创建集合。

语法格式：

```
db.createCollection(name, options)
```

参数说明：

-   name: 要创建的集合名称。
-   options: 可选参数, 指定有关内存大小及索引的选项，可选参数也是json格式

**options 可以是如下参数：**

| 参数名             | 类型   | 描述                                                         | 示例值                          |
| :----------------- | :----- | :----------------------------------------------------------- | :------------------------------ |
| `capped`           | 布尔值 | 是否创建一个固定大小的集合。                                 | `true`                          |
| `size`             | 数值   | 集合的最大大小（以字节为单位）。仅在 `capped` 为 true 时有效。 | `10485760` (10MB)               |
| `max`              | 数值   | 集合中允许的最大文档数。仅在 `capped` 为 true 时有效。       | `5000`                          |
| `validator`        | 对象   | 用于文档验证的表达式。                                       | `{ $jsonSchema: { ... }}`       |
| `validationLevel`  | 字符串 | 指定文档验证的严格程度。<br>`"off"`：不进行验证。<br>`"strict"`：插入和更新操作都必须通过验证（默认）。<br>`"moderate"`：仅现有文档更新时必须通过验证，插入新文档时不需要。 | `"strict"`                      |
| `validationAction` | 字符串 | 指定文档验证失败时的操作。<br>`"error"`：阻止插入或更新（默认）。<br>`"warn"`：允许插入或更新，但会发出警告。 | `"error"`                       |
| `storageEngine`    | 对象   | 为集合指定存储引擎配置。                                     | `{ wiredTiger: { ... }}`        |
| `collation`        | 对象   | 指定集合的默认排序规则。                                     | `{ locale: "en", strength: 2 }` |

**示例**

创建一个集合，集合的name，email，passwd域必填

```shell
test> db.createCollection('set',{validator:{$jsonSchema:{bsonType:'object',required:['name','email','passwd'],properties:{name:{bsonType:'string',description:"名称"},'email':{bsonType:'string',pattern:"^.+@.+$",description:"必须是合格的邮箱地址"},passwd:{bsonType:"int",minimum:0,description:'必须是字符串'}}}}})
{ ok: 1 }
test> show collections
set
test>
```

这样就创建成功了

**插入数据**

```
test> db.set.insert({'name':'xinghai','email':'xinghai@.com','passwd':123})
{
  acknowledged: true,
  insertedIds: { '0': ObjectId('66bc74f77e6fa0d69b838730') }
}
test> db.set.find()
[
  {
    _id: ObjectId('66bc74f77e6fa0d69b838730'),
    name: 'xinghai',
    email: 'xinghai@.com',
    passwd: 123
  }
]
test>
```

插入错误数据

```json
test> db.set.insert({'name':'xinghai','email':'xinghaicom','passwd':12,'adsf':'asdf'})
Uncaught:
MongoBulkWriteError: Document failed validation
Result: BulkWriteResult {
  insertedCount: 0,
  matchedCount: 0,
  modifiedCount: 0,
  deletedCount: 0,
  upsertedCount: 0,
  upsertedIds: {},
  insertedIds: {}
}
Write Errors: [
  WriteError {
    err: {
      index: 0,
      code: 121,
      errmsg: 'Document failed validation',
      errInfo: {
        failingDocumentId: ObjectId('66bc75467e6fa0d69b838734'),
        details: {
          operatorName: '$jsonSchema',
          schemaRulesNotSatisfied: [
            {
              operatorName: 'properties',
              propertiesNotSatisfied: [
                {
                  propertyName: 'email',
                  description: '必须是合格的邮箱地址',
                  details: [
                    {
                      operatorName: 'pattern',
                      specifiedAs: { pattern: '^.+@.+$' },
                      reason: 'regular expression did not match',
                      consideredValue: 'xinghaicom'
                    }
                  ]
                }
              ]
            }
          ]
        }
      },
      op: {
        name: 'xinghai',
        email: 'xinghaicom',
        passwd: 12,
        adsf: 'asdf',
        _id: ObjectId('66bc75467e6fa0d69b838734')
      }
    }
  }
]
test>
```

## 更新集合名

更新集合命令需要用adminCommand命名

```json
db.adminCommand({
    renameCollection:'oldName',
    to:'NewName'
})
```

-   oldName表示旧的集合名称，NewName表示新的集合名称，这两个名称必须的带上数据库的完整名称，例如test数据库集合aaa改成bbb那么名称就是test.aaa,test.bbb

例如

```json
test> show collections
abc
test> db.adminCommand({
... renameCollection:'test.abc',
... to:'test.ccc'
... })
{ ok: 1 }
test> show collections
ccc
test>
```

## 删除集合

删除集合需要进入改数据库才能删除集合

**命令**

```shell
db.collection.drop()
```

-   collection是集合的名称

示例

```shell
test> show collections
ccc
test> show collections
ccc
test> db.ccc.drop()
true
test> show collections

test>
```

## 插入文档

文档的数据结构和 JSON 基本相同。

所有存储在集合中的数据均为 BSON 格式。

BSON 是一种类似 JSON 的二进制形式的存储格式，是 Binary JSON 的简称。

常用的插入文档方法包括：

-   db.collection.insertOne()：插入单个文档
-   db.collection.insertMany()：插入多个文档
-   db.collection.save()：类似insertOne()。如果文档存在，则该文档会被更新；如果文档不存在，则补充一个新文档。

### insertOne

这个方法用于插入单个文档

**示例**

```json
test> show collections	//查看集合列表
test
test> db.test.insertOne({'name':'xinghai','age':18,'email':'bbb@.com'})		//插入文档
{
  acknowledged: true,
  insertedId: ObjectId('66bc7e727e6fa0d69b838736')
}
test> db.test.find()	//查看集合的文档
[
  {
    _id: ObjectId('66bc7e727e6fa0d69b838736'),
    name: 'xinghai',
    age: 18,
    email: 'bbb@.com'
  }
]
test>
```

### insertMany

这个方法用于插入多个文档

**示例**

```shell
test> db.test.insertMany([{'name':'name1','sex':'男'},{'name':'name2','sex':'女'},{'name':'name3','sex':'男'},{'name':'name4','sex':'未知'}])	//插入多个文档
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('66bc7f607e6fa0d69b838737'),
    '1': ObjectId('66bc7f607e6fa0d69b838738'),
    '2': ObjectId('66bc7f607e6fa0d69b838739'),
    '3': ObjectId('66bc7f607e6fa0d69b83873a')
  }
}
test> db.test.find()	//查看集合
[
  {
    _id: ObjectId('66bc7e727e6fa0d69b838736'),
    name: 'xinghai',
    age: 18,
    email: 'bbb@.com'
  },
  {
    _id: ObjectId('66bc7f607e6fa0d69b838737'),
    name: 'name1',
    sex: '男'
  },
  {
    _id: ObjectId('66bc7f607e6fa0d69b838738'),
    name: 'name2',
    sex: '女'
  },
  {
    _id: ObjectId('66bc7f607e6fa0d69b838739'),
    name: 'name3',
    sex: '男'
  },
  {
    _id: ObjectId('66bc7f607e6fa0d69b83873a'),
    name: 'name4',
    sex: '未知'
  }
]
test>
```

### save

当插入的数据有_id字段时，如果集合内有相同id的文档，那么就更新这个文档，如果没有就创建新的文档

这个方法只存在于mongo之前的终端中，在最新的版本，mongo被废弃，取而代之的是mongosh，save方法也再此被弃用

## 更新文档

在 MongoDB 中，更新文档的操作可以使用多种方法实现，常用的方法包括 **updateOne()、updateMany()、replaceOne() 和 findOneAndUpdate()**

### updateOne()

用于匹配过滤的单个文档，如果有多个匹配的文档，只会更新第一个

**命令**

```
db.myCollection.updateOne(filter,update,options)
```

-   filter,定位文档的参数
-   update，指定文档的操作，比如更新、替换等
-   options，设置

**示例**

```json
test> db.test.find()
[
  {
    _id: ObjectId('66bcaeaf7e6fa0d69b838804'),
    name: 'xinghai',
    age: 100
  }
]

test> db.test.updateOne({"name":'xinghai'},{$set:{age:1,'nnn':'eee'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
test> db.test.find()
[
  {
    _id: ObjectId('66bcaeaf7e6fa0d69b838804'),
    name: 'xinghai',
    age: 1,
    nnn: 'eee'
  }
]
test>
```

$set表示替换操作，如果存在就替换，不存在就添加字段

### updateMany

和updateOne操作类似，但是这个方法会更新匹配到的所有文档

**示例**

```shell
test> db.test.find()
[
  {
    _id: ObjectId('66bcaeaf7e6fa0d69b838804'),
    name: 'xinghai',
    age: 1,
    nnn: 'eee'
  },
  { _id: ObjectId('66bcb31c7e6fa0d69b838805'), name: 'name0', age: 55 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 55 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838807'), name: 'name2', age: 55 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838808'), name: 'name3', age: 55 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838809'), name: 'name4', age: 55 }
]
test> db.test.updateMany({'age':55},
... {$set:{'age':66}})		//更新
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 5,
  modifiedCount: 5,
  upsertedCount: 0
}
test> db.test.find()
[
  {
    _id: ObjectId('66bcaeaf7e6fa0d69b838804'),
    name: 'xinghai',
    age: 1,
    nnn: 'eee'
  },
  { _id: ObjectId('66bcb31c7e6fa0d69b838805'), name: 'name0', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838807'), name: 'name2', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838808'), name: 'name3', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838809'), name: 'name4', age: 66 }
]
test>
```

### replaceOne

该方法用于匹配替换单个文档，将新的文档完全覆盖旧的文档

**语法**

```
db.collection.replaceOne(filter, replacement, options)
```

-   **filter**：用于查找文档的查询条件。
-   **replacement**：新的文档，将替换旧的文档。
-   **options**：可选参数对象，如 `upsert` 等

**示例**

```shell
test> db.test.find()
[
  {
    _id: ObjectId('66bcaeaf7e6fa0d69b838804'),
    name: 'xinghai',
    age: 1,
    nnn: 'eee'
  },
  { _id: ObjectId('66bcb31c7e6fa0d69b838805'), name: 'name0', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838807'), name: 'name2', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838808'), name: 'name3', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838809'), name: 'name4', age: 66 }
]
test> db.test.replaceOne({'name':'name0'},{ 'name': 'xinghai', 'eee':66})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
test> db.test.find()
[
  {
    _id: ObjectId('66bcaeaf7e6fa0d69b838804'),
    name: 'xinghai',
    age: 1,
    nnn: 'eee'
  },
  {
    _id: ObjectId('66bcb31c7e6fa0d69b838805'),
    name: 'xinghai',
    eee: 66
  },
  { _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838807'), name: 'name2', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838808'), name: 'name3', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838809'), name: 'name4', age: 66 }
]
test>
```

可以发现，就算替换了内容，但是_id的值并没有改变

### findOneAndUpdate

跟新并且返回更新前或者跟新后的值

**语法**

```shell
db.collection.findAndUpdate(filter,update,options)
```

**示例**

```shell
test> db.test.findOneAndUpdate({'name':'name1'},{$set:{'age':50}})
{ _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 66 }
```

当更新完成时，默认会返回跟新前的文档

```shell
test> db.test.findOneAndUpdate({'name':'name1'},{$set:{'age':50}},{returnDocument:'after'})
{ _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 50 }
```

当指定returnDocument为after时，返回更新后的文档

## 删除文档

常用的删除文档方法包括 deleteOne()、deleteMany() 以及 findOneAndDelete()

### deleteOne

匹配删除单个文档

**示例**

```shell
test> db.test.find()
[
  {
    _id: ObjectId('66bcaeaf7e6fa0d69b838804'),
    name: 'xinghai',
    age: 1,
    nnn: 'eee'
  },
  {
    _id: ObjectId('66bcb31c7e6fa0d69b838805'),
    name: 'xinghai',
    eee: 66
  },
  { _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 50 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838807'), name: 'name2', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838808'), name: 'name3', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838809'), name: 'name4', age: 66 }
]
test> db.test.deleteOne({'name':'xinghai'})
{ acknowledged: true, deletedCount: 1 }
test> db.test.find()
[
  {
    _id: ObjectId('66bcb31c7e6fa0d69b838805'),
    name: 'xinghai',
    eee: 66
  },
  { _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 50 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838807'), name: 'name2', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838808'), name: 'name3', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838809'), name: 'name4', age: 66 }
]
test>
```

可以看到只删除了匹配的第一个文档

### deleteMany

删除匹配的所有文档

**示例**

```shell
test> db.test.find()
[
  {
    _id: ObjectId('66bcb31c7e6fa0d69b838805'),
    name: 'xinghai',
    eee: 66
  },
  { _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 50 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838807'), name: 'name2', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838808'), name: 'name3', age: 66 },
  { _id: ObjectId('66bcb31c7e6fa0d69b838809'), name: 'name4', age: 66 }
]
test> db.test.deleteMany({'age':66})
{ acknowledged: true, deletedCount: 3 }
test> db.test.find()
[
  {
    _id: ObjectId('66bcb31c7e6fa0d69b838805'),
    name: 'xinghai',
    eee: 66
  },
  { _id: ObjectId('66bcb31c7e6fa0d69b838806'), name: 'name1', age: 50 }
]
test>
```

可见删除了匹配的3个文档

### findOneAndDelete

用于删除匹配的文档，并返回删除的文档内容

**示例**

```shell
test> db.test.find()
[
  {
    _id: ObjectId('66bcb31c7e6fa0d69b838805'),
    name: 'xinghai',
    eee: 66
  }
]
test> db.test.findOneAndDelete({'name':'xinghai'})
{ _id: ObjectId('66bcb31c7e6fa0d69b838805'), name: 'xinghai', eee: 66 }
test>
```

## 查询文档

MongoDB 查询文档使用 **find()**、**findOne()** 方法

**示例**

查询所有文档

```shell
test> db.test.find()
[
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880a'), key: 'key0', value: -2 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880b'), key: 'key1', value: 0 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880c'), key: 'key2', value: 2 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880d'), key: 'key3', value: 4 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880e'), key: 'key4', value: 6 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880f'), key: 'key5', value: 8 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838810'), key: 'key6', value: 10 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838811'), key: 'key7', value: 12 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838812'), key: 'key8', value: 14 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838813'), key: 'key9', value: 16 }
]
test>
```

根据条件查询文档

```shell
test> db.test.find({'key':'key4'})
[
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880e'), key: 'key4', value: 6 }
]
test>
```

根据条件操作符查询文档，查询value大于10的文档

```shell
test> db.test.find({'value':{$gt:10}})
[
  { _id: ObjectId('66bd7e0e7e6fa0d69b838811'), key: 'key7', value: 12 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838812'), key: 'key8', value: 14 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838813'), key: 'key9', value: 16 }
]
test>
```

如果你需要以易读的方式来读取数据，可以使用 pretty() 方法，语法格式如下：

```shell
db.col.find().pretty()
```

**示例**

```shell
test> db.test.find().pretty()
[
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880a'), key: 'key0', value: -2 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880b'), key: 'key1', value: 0 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880c'), key: 'key2', value: 2 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880d'), key: 'key3', value: 4 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880e'), key: 'key4', value: 6 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b83880f'), key: 'key5', value: 8 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838810'), key: 'key6', value: 10 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838811'), key: 'key7', value: 12 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838812'), key: 'key8', value: 14 },
  { _id: ObjectId('66bd7e0e7e6fa0d69b838813'), key: 'key9', value: 16 }
]
test>
```

**findOne**

findOne() 方法用于查找集合中的单个文档。如果找到多个匹配的文档，它只返回第一个。

语法：

```shell
db.collection.findOne(query, projection)
```

**示例**

```shell
test> db.test.findOne({'value':{$gt:10}})
{ _id: ObjectId('66bd7e0e7e6fa0d69b838811'), key: 'key7', value: 12 }
test>
```

只返回第一条记录

## 条件操作符

### 比较操作符

比较操作符有：

| 操作符 | 描述             | 示例                              |
| :----- | :--------------- | :-------------------------------- |
| `$eq`  | 等于             | `{ age: { $eq: 25 } }`            |
| `$ne`  | 不等于           | `{ age: { $ne: 25 } }`            |
| `$gt`  | 大于             | `{ age: { $gt: 25 } }`            |
| `$gte` | 大于等于         | `{ age: { $gte: 25 } }`           |
| `$lt`  | 小于             | `{ age: { $lt: 25 } }`            |
| `$lte` | 小于等于         | `{ age: { $lte: 25 } }`           |
| `$in`  | 在指定的数组中   | `{ age: { $in: [25, 30, 35] } }`  |
| `$nin` | 不在指定的数组中 | `{ age: { $nin: [25, 30, 35] } }` |

### 逻辑操作符

逻辑操作符有：

| 操作符 | 描述                   | 示例                                                       |
| :----- | :--------------------- | :--------------------------------------------------------- |
| `$and` | 逻辑与，符合所有条件   | `{ $and: [ { age: { $gt: 25 } }, { city: "New York" } ] }` |
| `$or`  | 逻辑或，符合任意条件   | `{ $or: [ { age: { $lt: 25 } }, { city: "New York" } ] }`  |
| `$not` | 取反，不符合条件       | `{ age: { $not: { $gt: 25 } } }`                           |
| `$nor` | 逻辑与非，均不符合条件 | `{ $nor: [ { age: { $gt: 25 } }, { city: "New York" } ] }` |

### 元素操作符

元素操作符有：

| 操作符    | 描述             | 示例                         |
| :-------- | :--------------- | :--------------------------- |
| `$exists` | 字段是否存在     | `{ age: { $exists: true } }` |
| `$type`   | 字段的 BSON 类型 | `{ age: { $type: "int" } }`  |

### 数组操作符

数组操作符有：

| 操作符       | 描述                     | 示例                                                         |
| :----------- | :----------------------- | :----------------------------------------------------------- |
| `$all`       | 数组包含所有指定的元素   | `{ tags: { $all: ["red", "blue"] } }`                        |
| `$elemMatch` | 数组中的元素匹配指定条件 | `{ results: { $elemMatch: { score: { $gt: 80, $lt: 85 } } } }` |
| `$size`      | 数组的长度等于指定值     | `{ tags: { $size: 3 } }`                                     |

### 其他操作符

还有一些其他操作符如下：

| 操作符   | 描述                               | 示例                               |
| :------- | :--------------------------------- | :--------------------------------- |
| `$regex` | 匹配正则表达式                     | `{ name: { $regex: /^A/ } }`       |
| `$text`  | 进行文本搜索                       | `{ $text: { $search: "coffee" } }` |
| `$where` | 使用 JavaScript 表达式进行条件过滤 | `{ $where: "this.age > 25" }`      |
