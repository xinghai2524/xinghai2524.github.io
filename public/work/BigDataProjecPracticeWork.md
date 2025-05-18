<div class="container">

# **大数据开发项目实战**</div>

# 第三章




<h3>3-13   查询用户收视行为信息表中的无效数据</h3>

**统计消费金额的最大值、最小值、平均值和差**

```scala
val billeventData = spark.sql("select * from user_project.mmconsume_billevents")
val tvBilleventsData= billeventData.filter("sm_name like '%电视%' and sm_name != '模拟有线电视'")
val avgTVBillData = tvBilleventsData.groupBy("phone_no").agg((sum(col("should_pay")-col("favour_fee"))/7).alias("avg_fee"))
avgTVBillData.select(max("avg_fee"),min("avg_fee"),avg("avg_fee"),stddev("avg_fee")).show()
```

![image-20250409225803710](https://db.xinghai.ink/Typora/17442106875060856.png)

**按`range_fee`分组统计记录数**

```scala
val rangeTVBillData = avgTVBillData.withColumn("range_fee",floor(col("avg_fee")/10)*10)
val rangeTVCount = rangeTVBillData.groupBy("range_fee").count().orderBy(col("range_fee").asc)
rangeTVCount.show(30)
```

![image-20250409225817556](https://db.xinghai.ink/Typora/17442106998380368.png)

**保存至数据库**

```scala
import java.util.Properties
val connectionProperties = new Properties
connectionProperties.setProperty("user","root")
connectionProperties.setProperty("password","123456")
rangeTVCount.write.mode("append").jdbc("jdbc:mysql://hadoop01:3306/user_label","rangeTVCount",connectionProperties)
```

![image-20250409225956856](https://db.xinghai.ink/Typora/17442107987598674.png)

数据可视化

```python
import pandas as pd
import sqlalchemy
from pyecharts.charts import Line
from pyecharts import options as opts
import matplotlib.pyplot as plt

engine = sqlalchemy.create_engine('mysql+pymysql://root:123456@hadoop01/user_label')
query = "select * from rangeTVCount"

df = pd.read_sql_query(query,engine)
df = df.sort_values("range_fee")
x = df["range_fee"].astype(str).tolist()  # 转换为列表
y = df["count"].tolist()


line = (
    Line()
    .add_xaxis(x)
    .add_yaxis("abc", y)
)
line.render_notebook()

```

![image-20250409230042038](https://db.xinghai.ink/Typora/1744210844917534.png)

<h3>3-14  统计电视用户月均消费金额</h3>

**统计消费金额的最大值、最小值、平均值**

```scala
val billeventData = spark.sql("select * from user_project.mmconsume_billevents")
val netBilleventsData= billeventData.filter("sm_name like '%珠江宽频%'")
val avgNetBillData = netBilleventsData.groupBy("phone_no").agg((sum(col("should_pay")-col("favour_fee"))/7).alias("avg_fee"))
avgNetBillData.select(max("avg_fee"),min("avg_fee"),avg("avg_fee"),stddev("avg_fee")).show()
```

![image-20250409231007789](https://db.xinghai.ink/Typora/17442114099191988.png)

**按`range_fee`分组统计记录数**

```scala
val rangeNetBillData = avgNetBillData.withColumn("range_fee",floor(col("avg_fee")/10)*10)
val rangeNetCount = rangeNetBillData.groupBy("range_fee").count().orderBy(col("range_fee").asc)
rangeNetCount.show(30)
```

![image-20250409231015012](https://db.xinghai.ink/Typora/1744211416817597.png)

**保存至数据库**

```scala
import java.util.Properties
val connectionProperties = new Properties
connectionProperties.setProperty("user","root")
connectionProperties.setProperty("password","123456")
rangeNetCount.write.mode("append").jdbc("jdbc:mysql://hadoop01:3306/user_label","rangeNetCount",connectionProperties)
```

![image-20250409231023448](https://db.xinghai.ink/Typora/17442114253725789.png)

![image-20250409231123568](https://db.xinghai.ink/Typora/17442114853268373.png)

**数据可视化**

```python
import pandas as pd
import sqlalchemy
from pyecharts.charts import Line

engine = sqlalchemy.create_engine('mysql+pymysql://root:123456@hadoop01/user_label')
query = "select * from rangeNetCount"

df = pd.read_sql_query(query,engine)
x = df["range_fee"].astype(str).tolist()  # 转换为列表
y = df["count"].tolist()

# 创建折线图
line = Line()
line.add_xaxis(x)
line.add_yaxis(
    y_axis=y,
    series_name="abc"
)
line.render_notebook()
```

![image-20250409231138848](https://db.xinghai.ink/Typora/1744211500847509.png)

<h3>3-15  筛选后的电视用户越军消费金额的平均值和标准差</h3>

```scala
val billeventData = spark.sql("select * from user_project.mmconsume_billevents")
val tvBilleventsData= billeventData.filter("sm_name like '%电视%' and sm_name != '模拟有线电视'")
val avgTVBillData = tvBilleventsData.groupBy("phone_no").agg((sum(col("should_pay")-col("favour_fee"))/7).alias("avg_fee"))
avgTVBillData.filter("avg_fee>10 and avg_fee<=90").select(avg("avg_fee"),stddev("avg_fee")).show()
```

![image-20250416131456579](https://db.xinghai.ink/Typora/1744780500591843.png)

<h3>3-16  统计宽带用户月均消费金额</h3>

 

```scala
val billeventsData = spark.sql("select * from user_project.mmconsume_billevents")
val netBilleventsData = billeventsData.filter("sm_name like '%珠江宽频%'")

val avgNetBillData = netBilleventsData.groupBy("phone_no").agg((sum(col("should_pay")-col("favour_fee"))/7).alias("avg_fee"))


import org.apache.commons.math3.stat.descriptive.rank.Percentile

val _50_P = new Percentile(50.0)
val _50_duf = udf {(arr: scala.collection.mutable.WrappedArray[Double]) => _50_P.evaluate(arr.sorted.toArray)}

avgNetBillData.select(max("avg_fee"),min("avg_fee"),avg("avg_fee"),stddev("avg_fee"),_50_duf(collect_list("avg_fee")).alias("median")).show()

val rangeNetBillData = avgNetBillData.withColumn("range_fee",floor(col("avg_fee")/10)*10)

val rangeNetCount = rangeNetBillData.groupBy("range_fee").count().orderBy(col("range_fee").asc)

rangeNetCount.show(30)
```

![image-20250416140040832](https://db.xinghai.ink/Typora/17447832425368843.png)

![image-20250416140048840](https://db.xinghai.ink/Typora/17447832507302322.png)

保存至数据库

```scala
import java.util.Properties
val connectionProperties = new Properties
connectionProperties.setProperty("user","root")
connectionProperties.setProperty("password","123456")
rangeNetCount.write.mode("append").jdbc("jdbc:mysql://hadoop01:3306/user_label","rangeNetCount",connectionProperties)
```

![image-20250416135625201](https://db.xinghai.ink/Typora/1744782986997331.png)

数据可视化

```python
import pandas as pd
import sqlalchemy
from pyecharts.charts import Line

engine = sqlalchemy.create_engine('mysql+pymysql://root:123456@hadoop01/user_label')
query = "select * from rangeNetCount"

df = pd.read_sql_query(query,engine)
x = df["range_fee"].astype(str).tolist()  # 转换为列表
y = df["count"].tolist()

# 创建折线图
line = Line()
line.add_xaxis(x)
line.add_yaxis(
    y_axis=y,
    series_name="abc"
)
line.render_notebook()
```

![image-20250416135802086](https://db.xinghai.ink/Typora/17447830841820245.png)

<h3>3-17  过滤后宽带用户月均消费金额的统计</h3>

```scala
// 定义过后可以不用写
val billeventsData = spark.sql("select * from user_project.mmconsume_billevents")
val netBilleventsData = billeventsData.filter("sm_name like '%珠江宽频%'")
val avgNetBillData = netBilleventsData.groupBy("phone_no").agg((sum(col("should_pay")-col("favour_fee"))/7).alias("avg_fee"))
import org.apache.commons.math3.stat.descriptive.rank.Percentile
val _50_P = new Percentile(50.0)
val _50_duf = udf {(arr: scala.collection.mutable.WrappedArray[Double]) => _50_P.evaluate(arr.sorted.toArray)}


// 书本案例，只用敲这里就行
avgNetBillData.filter("avg_fee>=0 and avg_fee<90").select(avg("avg_fee"),stddev("avg_fee"),_50_duf(collect_list("avg_fee")).alias("median")).show()
```

![image-20250416150802799](https://db.xinghai.ink/Typora/17447872846873515.png)

<h3>3-18 统计分析电视用户入网时长相关值</h3>

```scala
val usermsgData = spark.sql("select * from user_project.mediamatch_usermsg")
val tvUsermsgData = usermsgData.filter("sm_name like '%电视%' and sm_name != '模拟有线电视' ")

val tvFilteredUsermsgData = tvUsermsgData.filter("open_time != 'NULL'")
val yearTVUserData = tvFilteredUsermsgData.groupBy("phone_no").agg(max(floor(datediff(current_date(),col("open_time"))/365)).alias("years"))

import org.apache.commons.math3.stat.descriptive.rank.Percentile

val _30_P = new Percentile(30.0)
val _30_udf = udf{(arr: scala.collection.mutable.WrappedArray[Double]) => _30_P.evaluate(arr.sorted.toArray)}

val _50_P = new Percentile(50.0)
val _50_udf = udf{(arr: scala.collection.mutable.WrappedArray[Double]) => _50_P.evaluate(arr.sorted.toArray)}

// 统计入网市场的最值、均值、30分位数和50分位数(中位数)

yearTVUserData.select(max("years"),min("years"),avg("years"),stddev("years"),_30_udf(collect_list(col("years").cast("double"))).alias("30%"),_50_udf(collect_list(col("years").cast("double"))).alias("media")).show()
```

![image-20250416155707147](https://db.xinghai.ink/Typora/17447902290519419.png)

```scala
val yearTVUserCount = yearTVUserData.groupBy("years").count
yearTVUserCount.show(30)
```

![image-20250416161651041](https://db.xinghai.ink/Typora/174479141454996.png)

保存到数据库

```scala
yearTVUserCount.write.mode("append").format("jdbc").option("url","jdbc:mysql://hadoop01:3306/user_label").option("dbtable","yearTVUserCount").option("user","root").option("password","123456").save()
```

![image-20250416163326651](https://db.xinghai.ink/Typora/1744792408499839.png)

数据可视化

```python
import pandas as pd
import sqlalchemy
from pyecharts.charts import Line

engine = sqlalchemy.create_engine('mysql+pymysql://root:123456@hadoop01/user_label')
query = "select * from yearTVUserCount"

df = pd.read_sql_query(query,engine)
x = df["years"].astype(str).tolist()  # 转换为列表
y = df["count"].tolist()

# 创建折线图
line = Line()
line.add_xaxis(x)
line.add_yaxis(
    y_axis=y,
    series_name="电视用户入网时长的分布"
)
line.render_notebook()
```

![image-20250416164902473](https://db.xinghai.ink/Typora/17447933445586026.png)

<h3>3-19 统计分析宽带用户入网时长的相关之</h3>

```scala
// 筛选宽带用户
val usermsgData = spark.sql("select * from user_project.mediamatch_usermsg")
val netUsermsgData = usermsgData.filter("sm_name = '珠江宽频' ")
val netFilteredUsermsgData = netUsermsgData.filter("open_time != 'NULL'")
val yearNetUserData = netFilteredUsermsgData.groupBy("phone_no").agg(max(floor(datediff(current_date(),col("open_time"))/365)).alias("years"))

import org.apache.commons.math3.stat.descriptive.rank.Percentile

val _50_P = new Percentile(50.0)
val _50_udf = udf{(arr: scala.collection.mutable.WrappedArray[Double]) => _50_P.evaluate(arr.sorted.toArray)}

yearNetUserData.select(max("years"),min("years"),avg("years"),stddev("years"),_50_udf(collect_list(col("years").cast("double"))).alias("media")).show()

// 分组统计每个入网时长值的用户数量
val yearNetUserCount = yearNetUserData.groupBy("years").count.orderBy(col("years").asc)
yearNetUserCount.show(20)
```

![image-20250416164235838](https://db.xinghai.ink/Typora/17447929577223752.png)

![image-20250416164701828](https://db.xinghai.ink/Typora/1744793224058242.png)

保存至数据库

```scala
yearNetUserCount.write.mode("append").format("jdbc").option("url","jdbc:mysql://hadoop01:3306/user_label").option("dbtable","yearNetUserCount").option("user","root").option("password","123456").save()
```

![image-20250416165217776](https://db.xinghai.ink/Typora/17447935396538417.png)

数据可视化

```python
import pandas as pd
import sqlalchemy
from pyecharts.charts import Line

engine = sqlalchemy.create_engine('mysql+pymysql://root:123456@hadoop01/user_label')
query = "select * from yearNetUserCount"

df = pd.read_sql_query(query,engine)
x = df["years"].astype(str).tolist()  # 转换为列表
y = df["count"].tolist()

# 创建折线图
line = Line()
line.add_xaxis(x)
line.add_yaxis(
    y_axis=y,
    series_name="宽带用户入网时长的分布"
)
line.render_notebook()
```

![image-20250416165146435](https://db.xinghai.ink/Typora/17447935083951945.png)

# 第四章

## 第一次作业

```scala
val data = spark.sql("select t1.phone_no,case when T>8 then '老用户' when T>4 and T<=8 then '中等用户' when T<=4 then '新用户' end as label, ' 电视入网程度' as parent_label from (select phone_no, max(floor(datediff(current_date(),open_time)/365)) as T from user_project.mediamatch_usermsg where sm_name like '%电视%' and open_time is not NULL and sm_name = '模拟有线电视' group by phone_no) t1")
```

![image-20250417215327349](https://db.xinghai.ink/Typora/1744898033681141.png)

```scala
data.write.mode("append").format("jdbc").option("url","jdbc:mysql://hadoop01:3306/user_label").option("dbtable","user_project").option("user","root").option("password","123456").save()
```

![image-20250417215337312](https://db.xinghai.ink/Typora/17448980320467277.png)

![image-20250417215346698](https://db.xinghai.ink/Typora/17448980300242844.png)

```scala
val netdata = spark.sql("select t1.phone_no,case when T>8 then '老用户' when T>4 and T<=8 then '中等用户' when T<=4 then '新用户' end as label, ' 电视入网程度' as parent_label from (select phone_no, max(floor(datediff(current_date(),open_time)/365)) as T from user_project.mediamatch_usermsg where sm_name ='珠江宽频' and open_time is not NULL group by phone_no) t1")
```

![image-20250417215425746](https://db.xinghai.ink/Typora/17448980676130235.png)



```scala
netdata.write.mode("append").format("jdbc").option("url","jdbc:mysql://hadoop01:3306/user_label").option("dbtable","user_netproject").option("user","root").option("password","123456").save()
```

![image-20250417215441295](https://db.xinghai.ink/Typora/17448980839543324.png)

![image-20250417215456004](https://db.xinghai.ink/Typora/17448980985154414.png)

## 第二次作业

![2025-04-23_19-13-11](https://db.xinghai.ink/Typora/17454073798227851.png)

![2025-04-23_19-13-16](https://db.xinghai.ink/Typora/17454074182249238.png)

![2025-04-23_19-13-22](https://db.xinghai.ink/Typora/17454074250249012.png)

![2025-04-23_19-13-27](https://db.xinghai.ink/Typora/17454074387886724.png)

# 第六章

## 6.1    构建特征列

```scala
// 统计每个用户的月均消费金额
val billevents = spark.sql("select phone_no, sum(should_pay) / 3 consume from user_project.mmconsume_billevents where sm_name not like '%珠江宽频%' group by phone_no ")

// 统计每个用户的入网时长
val userevents = spark.sql(" select phone_no,max(months_between(current_date(),run_time)/12) join_time from user_project.mediamatch_userevent group by phone_no ")

// 统计每个用户平均看多少小时电视
val media_index = spark.sql("select phone_no,(sum(duration)/(1000*60*60))/count(1) as count_duration from user_project.media_index group by phone_no")
// 统计上列所有数据
val billevents_userevents_media = billevents.join(userevents, Seq("phone_no")).join(media_index,Seq("phone_no"))
```

![image-20250505224154665](https://db.xinghai.ink/Typora/17464561173493414.png)

## 6.2    计算用户前一个月观看电视时长

```scala
val mediaIndex= spark.sql("select phone_no,round(sum(duration)/(1000*60*60),2) as total_one_hours from user_project.media_index where origin_time >= add_months('2018-01-01 00:00:00',-1) group by phone_no ")

mediaIndex.show(3)

// 定义函数
import org.apache.commons.math3.stat.descriptive.rank.Percentile
val _30_P = new Percentile(30.0)
val _50_P = new Percentile(50.0)
val _30_udf = udf{(arr: scala.collection.mutable.WrappedArray[Double]) => _30_P.evaluate(arr.sorted.toArray) }
val _50_udf = udf{(arr: scala.collection.mutable.WrappedArray[Double]) => _50_P.evaluate(arr.sorted.toArray) }

mediaIndex.select(max("total_one_hours").alias("max"),min("total_one_hours").alias("min"),avg("total_one_hours").alias("avg"),stddev("total_one_hours").alias("stddev"),_30_udf(collect_list("total_one_hours")).alias("30%"),_50_udf(collect_list("total_one_hours")).alias("median")).show()
```

![image-20250506173112228](https://db.xinghai.ink/Typora/17465238752855997.png)

## 6.3    统计电视观看时长为0~15h的信息

```scala
val mediaIndex_15 = mediaIndex.filter("total_one_hours<=15")
mediaIndex_15.select(max("total_one_hours").alias("max"),min("total_one_hours").alias("min"),avg("total_one_hours").alias("avg"),stddev("total_one_hours").alias("stddev"),_30_udf(collect_list("total_one_hours")).alias("30%"),_50_udf(collect_list("total_one_hours")).alias("median")).show()
```

![image-20250506174546231](https://db.xinghai.ink/Typora/17465247483368943.png)

```scala
//统计活跃用户和非活跃用户
val msg = spark.sql("select distinct phone_no,0 as col1 from user_project.mediamatch_usermsg")

val mediaIndex = spark.sql("select phone_no,sum(duration) as total_one_month_seconds from user_project.media_index where origin_time>=add_months('2018-08-01 00:00:00',-1) group by phone_no having total_one_month_seconds>18936000").select("phone_no", "total_one_month_seconds")

val orderIndexTV = spark.sql("select * from user_project.order_index where run_name='正常' and offername!='废' and offername!='赠送' and offername!='免费体验' and offername!='提速' and offername!='提价' and offername!='转网优惠' and offername!='虚拟' and offername!='空包' and offername not like '%宽带%'").select("phone_no").distinct()

val media_order =  mediaIndex.join(orderIndexTV, Seq("phone_no"), "inner").selectExpr("phone_no", "1 as col2").distinct()

val msg_media_order = msg.join(media_order, Seq("phone_no"), "left_outer").na.fill(0).selectExpr("phone_no", "col2 as col1")

val billevents = spark.sql("select phone_no, sum(should_pay)/3 consume from user_project.mmconsume_billevents where sm_name not like '%珠江宽频%' group by phone_no")

val userevents = spark.sql("select phone_no,max(months_between(current_date(),run_time)/12) join_time from user_project.mediamatch_userevent group by phone_no")

val media_index = spark.sql("selkect phone_no ")

```

