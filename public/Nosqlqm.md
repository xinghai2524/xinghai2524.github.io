

# 第一题

> 记得改数据库名称和学号

// 创建一个名为 “姓名简写+DB” 的数据库，
//并在其中创建三个集合，分别为 “professors+学号后两位”、“subjects” 和 “class_rooms”

```
use yxhDB;
db.createCollection('professors022')
db.createCollection('subjects')
db.createCollection('class_rooms')
```

// 2.、向 “professors+学号后两位” 集合插入文档

```
db.professors022.insertOne({

  "name": "李教授",

  "age": 45,

  "faculty": "化学学院",

  "teachingSubjects": ["有机化学", "分析化学", "物理化学"]

})
```

// 3、向 “subjects” 集合插入多条文档（1分）

```
db.subjects.insertMany([
{

  "subjectName": "有机化学",

  "credit": 3.5,

  "professor": "李教授",

  "description": "研究有机化合物的结构、性质和反应的学科。"

},
{

  "subjectName": "分析化学",

  "credit": 3,

  "professor": "李教授",

  "description": "研究物质化学组成和结构的分析方法的学科。"

},
{

  "subjectName": "物理化学",

  "credit": 4,

  "professor": "李教授",

  "description": "应用物理学原理和方法研究化学现象和规律的学科。"

}])
```


//4、向 “class_rooms” 集合中插入一个表示教室信息的文档

```
db.class_rooms.insertOne({

  "roomNumber": "306",

  "capacity": 45,

  "subjectsScheduled": ["有机化学", "分析化学"],

  "equipment": ["投影仪", "实验台", "通风设备"]

})
```

//5、查找 “subjects” 集合中课程学分大于 3 分、授课教师为 “李教授” 课程文档（3分）

```
db.subjects.find({credit:{$gt:3}})
```

//6、查询 “professors+学号后两位” 集合中年龄在 40 到 45 岁之间（包含 40 岁和 45 岁）的教师信息，只看教授名字（3分）

```
db.professors022.find({age:{$gte:40,$lte:45}})
```

//7、为 “class_rooms” 集合中所有可容纳人数小于 50 人的教室添加 “location” 字段，值为 “西楼”（3分）

```
db.class_rooms.updateMany(
  { capacity: { $lt: 50 } },
  { $set: { location: "西楼" } }
);
```

//8、删除 “class_rooms” 集合中容纳人数小于 40 人且没有 “投影仪” 设备的所有教室文档（4分）

```
db.class_rooms.deleteMany(
  { capacity: { $lt: 40 }, equipment: { $nin: ["投影仪"] } }
);
```

// 9、为 “subjects” 集合创建一个复合索引，索引字段为 “professor”、“credit” 和 “subjectName”，索引名称为 “subject_index”

```
db.subjects.createIndex(
  { professor: 1, credit: 1, subjectName: 1 },
  { name: "subject_index" }
);
```

// 10、在 “class_rooms” 集合中，查找所有安排了 “有机化学” 并且按照可容纳人数从高到低排序

```
db.class_rooms.find(
  { subjectsScheduled: "有机化学" }
).sort({ capacity: -1 });
```

// 11、统计 “subjects” 集合中不同学分的课程数量，并且按照学分数量从多到少排序输出

```
db.subjects.aggregate([
  { $group: { _id: "$credit", count: { $sum: 1 } } },
  { $sort: { count: -1 } }
]);
```

// 12、计算 “professors+学号后两位” 集合中来自 “化学学院” 且教授课程包含 “物理化学” 的教师的平均年龄

```
db.professors022.aggregate([
  { $match: { faculty: "化学学院", teachingSubjects: { $in: ["物理化学"] } } },
  { $group: { _id: null, avgAge: { $avg: "$age" } } }
]);
```

// 13、按照授课教师分组，统计每个教师教授的课程中，学分大于 3 分且课程名称以 “分析” 开头的课程数量

```
db.subjects.aggregate([
  { $match: { credit: { $gt: 3 }, subjectName: { $regex: "^分析" } } },
  { $group: { _id: "$professor", count: { $sum: 1 } } }
]);
```

# 第二题

> 改学号和名字，注意看题

-- 使用 Redis 客户端连接到本地 Redis 服务器，设置一个名为 “customer” 的字符串键，值为 “自己的姓名简写+学号后两位”，并查看设置结果。

```
set customer yxh022
get customer
```

-- 向名为 “friends” 的列表中依次添加元素 “姓名的拼音1”、“姓名的拼音2”、“姓名的拼音3”，然后获取列表的长度以及所有元素。

```
lpush friends y x h
lrange friends 0 -1
llen friends
```

-- 将值 “verified” 添加到名为 “account_status” 的集合中，再判断值 “verified” 是否存在于该所在集合中。

```
sadd account_status verified
sismember account_status verified
```

-- 为名为 “customer” 的键设置过期时间为 90 秒，然后查看剩余过期时间。

```
expire customer 90
ttl customer
```
