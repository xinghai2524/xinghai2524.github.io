

# spark安装

# 一、spark介绍

spark是基于java和scala开发的分布式计算引擎，使用上，支持使用java，scala，R，python语言编程 

spark生态主要包括·，spark sql，spark core，spark Streaming，MKlib、GraphX以及独立调度器

![spark入门及一些demo_spark demo-CSDN博客](https://db.xinghai.ink/Typora/17463623081481357.png)

spark仅仅只是一个计算框架，不负责数据的存储和管理，通常都会将spark和hadoop进行统一部署，由hadoop的HDFS，HBase、Hive进行数据存



spark安装方式分为单机模式，常用于开发和测试，集群模式通常分为Standalone模式，Yarn模式，Mesos模式，这里使用yarn运行

# 二、下载spark

官网搜索spark，进入spark，选择release版本，下载

![image-20250504225624068](https://db.xinghai.ink/Typora/17463705863978024.png)

这里选择3.2.1

![image-20250504231919126](https://db.xinghai.ink/Typora/17463719610652452.png)

![image-20250504231939082](https://db.xinghai.ink/Typora/17463719808821666.png)

下载到linux中

# 三、配置spark

spark目录如下

```shell
drwxr-xr-x 13  501 ubuntu  4096 Jan 20  2022 ./
drwxr-xr-x  1 root root    4096 May  4 15:30 ../
-rw-r--r--  1  501 ubuntu 22878 Jan 20  2022 LICENSE
-rw-r--r--  1  501 ubuntu 57677 Jan 20  2022 NOTICE
drwxr-xr-x  3  501 ubuntu  4096 Jan 20  2022 R/
-rw-r--r--  1  501 ubuntu  4512 Jan 20  2022 README.md
-rw-r--r--  1  501 ubuntu   167 Jan 20  2022 RELEASE
drwxr-xr-x  2  501 ubuntu  4096 Jan 20  2022 bin/
drwxr-xr-x  2  501 ubuntu  4096 Jan 20  2022 conf/
drwxr-xr-x  5  501 ubuntu  4096 Jan 20  2022 data/
drwxr-xr-x  4  501 ubuntu  4096 Jan 20  2022 examples/
drwxr-xr-x  2  501 ubuntu 16384 Jan 20  2022 jars/
drwxr-xr-x  4  501 ubuntu  4096 Jan 20  2022 kubernetes/
drwxr-xr-x  2  501 ubuntu  4096 Jan 20  2022 licenses/
drwxr-xr-x  9  501 ubuntu  4096 Jan 20  2022 python/
drwxr-xr-x  2  501 ubuntu  4096 Jan 20  2022 sbin/
drwxr-xr-x  2  501 ubuntu  4096 Jan 20  2022 yarn
```

其中

- bin	可执行文件
- conf	配置文件
- data	包含了一些模块包含的数据，一写模板数据
- examples	包含官方的案例

当下载完成spark，解压之后，那么local模式就算是配置成功了

## 3.1    测试local模式的spark

使用一下代码测试spark

```
spark-submit --class org.apache.spark.examples.SparkPi --master local[*] ./examples/jars/spark-examples_2.12-3.2.1.jar 1000
```

- --class 表示通过什么类去运行
- --master表示连接哪个资管管理器去执行任务，比如spark，yarn，local

![image-20250505154230620](https://db.xinghai.ink/Typora/1746430955009241.png)

运行成功

## 3.2  运行在yarn的spark

由于spark需要提交道yarn中执行，所以需要让spark知道yarn的位置在哪

所以，配置`conf/spark-env.sh`添加下列内容

```sh
YARN_CONF_DIR=/opt/spark-3.2.1# /opt/hadoop-3.1.4/etc/hadoop
```

```
spark-submit --class org.apache.spark.examples.SparkPi --master yarn ./examples/jars/spark-examples_2.12-3.2.1.jar 10
```

但是运行的时候被强制终止了，原因就是资源不足，所以不要限制资源

![image-20250505161845088](https://db.xinghai.ink/Typora/17464331271348252.png)

修改yarn-site.xml，添加下列内容，然后重启yarn客户端

```
<property>
        <name>yarn.nodemanager.pmem-check-enabled</name>
        <value>false</value>
</property>
<property>
        <name>yarn.nodemanager.vmem-check-enabled</name>
        <value>false</value>
</property>
```

再次执行就可以了

![image-20250505163040417](https://db.xinghai.ink/Typora/17464338427757032.png)