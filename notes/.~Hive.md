<div class="container">

# **Hive 3.X 笔记**</div>



# 第一章 Hive基本原理

## 1.1   Hive基本架构

![image-20250417224517339](https://db.xinghai.ink/Typora/17449011196599863.png)

- Hive中，元数据（表信息，分隔符，数据类型）存储在关系型数据库中（默认是derby数据库，但是推荐mysql数据库）,实际文件存储在HDFS中
- metastore用于处理元数据信息，
- 

# 第二章 Hive的部署

Hive官方下载地址：https://archive.apache.org/dist/hive/



## 2.1   最小化安装

<h4>安装步骤</h4>

1 解压`Hive`到本地路径

```shell
tar -zxvf apache-hive-3.1.2-bin.tar.gz
```

2  修改名称为 `hive-3.1.2`

```shell
mv apache-hive-3.1.2-bin hive-3.1.2
```

3  添加环境变量

```shell
vim ~/.bashrc1
```

添加一下内容

```shell
export HIVE_HOME=//opt/hive-3.1.2
export PATH=$PATH:$HIVE_HOME/bin
```

更新环境变量

```shell
source ~/.bashrc
```

4  初始化数据库（默认是derBy数据库）

创建数据库后会在当前目录下创建目录文件

```shell
schematool -dbType derby -initSchema
```

<h4>最小化使用</h4>

Hive的原理是通过`metastore`将元数据存放到数据库中，将数据存放在`HDFS`中，上一步已经将默认的`derby`数据库初始化成功，所以直接启动`metastore`即可以直接使用`Hive`,如果没有启动`metastore`那么命令行客户端会代替`metastore`的工作，但是性能不好，不推荐



1  进入在初始化的元数据目录的文件夹中

![2025-04-18_10-29-23](https://db.xinghai.ink/Typora/17449433724349248.png)

2  执行`Hive`

```shell
hive
```

![image-20250418103039303](https://db.xinghai.ink/Typora/17449434414068959.png)

3  查看数据库

[hive>]表示是在hive中执行的命令，在命令行中不用写

```hive
hive> show databases;
```

![image-20250418103237433](https://db.xinghai.ink/Typora/1744943559460933.png)

- 其中，default是默认数据库

4  创建表，插入数据，查看数据

  进入default

```hive
hive> use default;
```

![image-20250418103650434](https://db.xinghai.ink/Typora/17449438124982746.png)

查看表

```hive
hive> show tables;
```

![2025-04-18_10-37-10](https://db.xinghai.ink/Typora/17449438355948758.png)

创建表

```hive
hive> create table stu(id int, name string);
```

![image-20250418103839464](https://db.xinghai.ink/Typora/17449439215514708.png)

插入数据

```hive
hive> insert into stu values(1,"xiaoming");
```

![image-20250418103954654](https://db.xinghai.ink/Typora/17449439966919596.png)

查看表结构

```hive
desc stu;
```

![image-20250418104026061](https://db.xinghai.ink/Typora/17449440280759416.png)



查看数据

```hive
select * from stu;
```

![image-20250418104049039](https://db.xinghai.ink/Typora/1744944051024351.png)

<h4>观察HDFS</h4>

`hive`在`hdfs`的路径默认是`/user/hive/warehouse`

1  查看hdfs

```
hdfs dfs -ls /user/hive/warehouse
```

![image-20250418105616591](https://db.xinghai.ink/Typora/17449449797320518.png)

2  在刚才创建的stu表格数据被保存在了stu路径

```
hdfs dfs -cat /user/hive/warehouse/stu/*
```

![image-20250418105727475](https://db.xinghai.ink/Typora/17449450495215216.png)

文件以文本形式保存



## 2.2 Mysql配置

希望将`Hive`的元数据存储到`Mysql`中，则需要配置`Mysql`和`Hive`配置文件

### 2.2.1    安装mysql

首先是配置mysql，以Ubuntu为例，在hadoop01中安装mysql

```
apt-get install mysql-server
```

![image-20250430133712859](https://db.xinghai.ink/Typora/17459914358997302.png)

### 2.2.2    启动mysql

启动由于我的电脑没有systemctl工具，这里就用service去启动

```
service mysql start
```

![image-20250430133849891](https://db.xinghai.ink/Typora/17459915317731073.png)

使用systemctl工具的启动方式

```
systemctl start mysql
```

### 2.2.3    配置mysql

首先在root权限中可以直接使用mysql命令进入mysql

```
sudo mysql
```

![image-20250430134020868](https://db.xinghai.ink/Typora/17459916234527755.png)

需要修改的有两点

- 默认root用户不能以密码登入，所以需要修改策略
- 给root设置密码

修改策略

进入mysql数据库

```
use mysql
```

查看root用户信息

```
select * from user where user='root' /G;
```

![image-20250430134305289](https://db.xinghai.ink/Typora/17459917872376125.png)

根据信息可见

其中，Host是localhost，说明只能本地登入，plugin是auth_socket说明不能用账号密码登入，这里都修改一下

```mysql
alter user root@localhost identified with mysql_native_password by 'root';
```

![image-20250430140124352](https://db.xinghai.ink/Typora/17459928879366093.png)



> <h4>由于 Hadoop 和 Hive 的 Guava 库版本不兼容，所以第四步可能会有问题</h4>
>
> 解决方法：
>
> [`$HADOOP_HOME`为`Hadoop`目录]
>
> [`$HIVE_HOME`为`Hive`目录]
>
> 
>
> 一、检查`Hive`与`hadoop`的`Guava`
>
> 查看`Hadoop`的`Guava`
>
> ```shell
> cd $HADOOP_HOME/share/hadoop/common/lib/
> find guava*
> ```
>
> 查看 `Hive`的`Guava`
>
> ```shell
> cd $HIVE_HOME/lib
> find guava*
> ```
>
> 二、替换掉低版本的guava
>
> 删除低版本的`guava`
>
> ```shell
> rm $HADOOP_HOME/share/hadoop/common/lib/guava-19.0.jar
> ```
>
> 复制高版本的`Guava`
>
> ```shell
> cp $HIVE_HOME/lib/guava-27.0-jre.jar $HADOOP_HOME/share/hadoop/common/lib
> ```

# 第三章 Hive的操作
