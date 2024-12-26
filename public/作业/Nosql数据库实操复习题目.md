# MongoDB数据库实操复习题目

//创建一个名为 ‘examDB’的数据库，并在其中创建一个一个名为‘students’的集合

```
use examDB;
db.createCollection('students')
```

![image-20241226162947802](https://db.xinghai.ink/Typora/17352021435908315.png)

// 查看当前MongoDB服务器上的所有数据库名称

```
show dbs;
```

![image-20241226163013303](https://db.xinghai.ink/Typora/173520215030359.png)

// 向students集合中插入以下文档

```
db.students.insertMany([
    {"name": "张三","age": 20,"major": "计算机科学","grades": [85, 90, 78]},
    {"name": "李四","age": 18,"major": "大数据技术","grades": [85, 80, 78]},
    {"name": "王五","age": 16,"major": "软件工程","grades": [85, 75, 78]},
    {"name": "赵六","age": 30,"major": "计算机科学","grades": [75, 60, 80]},
])
```

![image-20241226163033493](https://db.xinghai.ink/Typora/1735202151946462.png)

// 查询students集合中，所有年龄大于18岁的学生文档

```
db.students.find({age:{$gt:18}})
```

![image-20241226163054084](https://db.xinghai.ink/Typora/1735202154020899.png)

// 查询集合中专业为计算机科学，且某一门成绩大于80的学生文文档

```
db.students.find({major:'计算机科学',grades:{$elemMatch:{$gt:80}}})
```

![image-20241226163108943](https://db.xinghai.ink/Typora/17352021554981613.png)

// 按照学生姓名升序查询‘student’集合中的所有文档

```
db.students.find().sort({'name':1})
```

![image-20241226163132618](https://db.xinghai.ink/Typora/17352021571140258.png)

// 将 ‘students’ 集合中张三的年龄更新为21岁

```
db.students.updateMany({name:'张三'},{$set:{age:21}})
db.students.find({name:'张三'})
```

![image-20241226163210564](https://db.xinghai.ink/Typora/1735202163607838.png)

// 把student集合中，所有学生的某一门成绩，加五分

```
db.students.updateMany({},{$inc:{'grades.1':5}})
db.students.find()
```

![image-20241226163233770](https://db.xinghai.ink/Typora/17352021596221814.png)

// 删除小于18岁的所有学生文档

```
db.students.deleteMany({age:{$lt:18}})
db.students.find()
```

![image-20241226163304588](https://db.xinghai.ink/Typora/17352021709723408.png)

// 删除某个学生的grades字段

```
db.students.updateMany({'name':'李四'},{$unset:{'grades':''}})
db.students.find()
```

![image-20241226163327423](https://db.xinghai.ink/Typora/1735202176057946.png)

// 为student集合的name字段创建一个升序索引

```
db.students.createIndex({'name':1})
```

![image-20241226163342503](https://db.xinghai.ink/Typora/17352021990904162.png)

// 查看student的已创建的索引信息

```
db.students.getIndexes()
```

![image-20241226163401249](https://db.xinghai.ink/Typora/17352021968207085.png)

// 删除‘student’集合上名为name_1的索引

```
db.students.dropIndex({'name':1})
db.students.getIndexes()
```

![image-20241226163424949](https://db.xinghai.ink/Typora/17352021913937497.png)

// 统计student集合中的学生总数

```
db.students.countDocuments({});
```

![image-20241226163444251](https://db.xinghai.ink/Typora/17352021888030653.png)

// 计算学生成绩的品均值

```
db.students.aggregate([{$project:{'学生平均值':{$avg:'$grades'}}}])
```

![image-20241226163458805](https://db.xinghai.ink/Typora/17352021855149152.png)

// 复制集合到 ‘students_backup’

```
db.students.aggregate([{$out:"students_backup"}])
db.students_backup.find()
```

![image-20241226163519547](https://db.xinghai.ink/Typora/17352021816226377.png)

// 删除名为examDB的数据库

```
db.dropDatabase()
```

![image-20241226163530221](https://db.xinghai.ink/Typora/17352022114406822.png)



# Redis数据库实操复习题目

-- 设置一个名为user:name的字符串链，值为张三,并查看值

```
set user:1 'name'
keys *
```

![image-20241226174751446](https://db.xinghai.ink/Typora/17352066915209064.png)

-- 向名为fruits的类表中依次添加元素 apple bnana cherry,并获取长度以及所有元素

```
rpush fruits apple bnana cherry
llen fruits
lrange fruits 0 -1
```

![image-20241226174814994](https://db.xinghai.ink/Typora/1735206692923543.png)

-- 在名为scores的有序集合中，添加成员 student1，分值为85，student2 分值为90 student3 分值为78，并按照分值从高到低获取前两名成员

```
zadd scores 85 student1 90 student2 78 student3
zrevrange scores 0 1 withscores
```

![image-20241226174835238](https://db.xinghai.ink/Typora/17352066949729555.png)

-- 创建一个book的哈希表 表title为Redis实战，author 为 ’某作者‘ publisher为 ’某出版社‘,然后获取所有值和字段

```
hset book title 'Redis实战' author '某作者' publisher '某出版社'
hgetall book
```

![image-20241226174950496](https://db.xinghai.ink/Typora/17352067042738535.png)

-- 将active添加到status的集合中，再判断active是否在集合中

```
sadd status active
sismember status active
```

![image-20241226175008734](https://db.xinghai.ink/Typora/173520669917816.png)

-- 查看redis，user开头的键

```
keys user:*
```

![image-20241226175017553](https://db.xinghai.ink/Typora/17352067145968876.png)

-- 设置名为 user:name 的键，设置过期时间为60秒，然后查看过期剩余时间

```
expire user:1 60
ttl user:1
```

![image-20241226175032956](https://db.xinghai.ink/Typora/1735206717737701.png)

-- 重命名user:1:name的键重命名为user:1:fullname,并查新的键的值

```
set user:1 fullname
get user:1
```

![image-20241226175048923](https://db.xinghai.ink/Typora/1735206721759027.png)

--  删除名为 fruits的列表

```
del fruits
```


![image-20241226175058195](https://db.xinghai.ink/Typora/17352067246307147.png)
