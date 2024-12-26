# MongoDB数据库实操复习题目

//创建一个名为 ‘examDB’的数据库，并在其中创建一个一个名为‘students’的集合

```
use examDB;
db.createCollection('students')
```

// 查看当前MongoDB服务器上的所有数据库名称

```
show dbs;
```

// 向students集合中插入以下文档

```
db.students.insertMany([
    {"name": "张三","age": 20,"major": "计算机科学","grades": [85, 90, 78]},
    {"name": "李四","age": 18,"major": "大数据技术","grades": [85, 80, 78]},
    {"name": "王五","age": 16,"major": "软件工程","grades": [85, 75, 78]},
    {"name": "赵六","age": 30,"major": "计算机科学","grades": [75, 60, 80]},
])
```

// 查询students集合中，所有年龄大于18岁的学生文档

```
db.students.find({age:{$gt:18}})
```

// 查询集合中专业为计算机科学，且某一门成绩大于80的学生文文档

```
db.students.find({major:'计算机科学',grades:{$elemMatch:{$gt:80}}})
```

// 按照学生姓名升序查询‘student’集合中的所有文档

```
db.students.find().sort({'name':1})
```

// 将 ‘students’ 集合中张三的年龄更新为21岁

```
db.students.updateMany({name:'张三'},{$set:{age:21}})
db.students.find({name:'张三'})
```

// 把student集合中，所有学生的某一门成绩，加五分

```
db.students.updateMany({},{$inc:{'grades.1':5}})
db.students.find()
```

// 删除小于18岁的所有学生文档

```
db.students.deleteMany({age:{$lt:18}})
db.students.find()
```

// 删除某个学生的grades字段

```
db.students.updateMany({'name':'李四'},{$unset:{'grades':''}})
db.students.find()
```

// 为student集合的name字段创建一个升序索引

```
db.students.createIndex({'name':1})
```

// 查看student的已创建的索引信息

```
db.students.getIndexes()
```

// 删除‘student’集合上名为name_1的索引

```
db.students.dropIndex({'name':1})
db.students.getIndexes()
```

// 统计student集合中的学生总数

```
db.students.countDocuments({});
```

// 计算学生成绩的品均值

```
db.students.aggregate([{$project:{'学生平均值':{$avg:'$grades'}}}])
```

// 复制集合到 ‘students_backup’

```
db.students.aggregate([{$out:"students_backup"}])
db.students_backup.find()
```

// 删除名为examDB的数据库

```
db.dropDatabase()
```

