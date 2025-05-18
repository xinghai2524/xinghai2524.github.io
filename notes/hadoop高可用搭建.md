安装ha模式的集群

HA：High Availability 高可用

高可用集群

服务器挂掉是正常现象，简单模式的hadoop集群如果一台服务器挂掉了那么整个集群就有可能挂掉了

高可用的集群表示：即使某几台服务器挂掉了，任然不影响服务的使用

在hdfs和yarn中，如果有多个小弟节点，那么如果其中几个节点宕机了，依然不影响服务的正常运行，那么如果是NameNode和Resourcemanager宕机了，那么整个集群就废了，zookeeper就是用来解决这个问题的，所以Hadoop高可用一般来说就是Hdfs的namenode和Yarn的resourcemanager的高可用，创建一个吃干饭的节点来备用，如果namenode和reourcemanager宕机了，就切换到备用节点

zookeeper用于帮助实现hadoop的HA高可用

## HDFS HA实现原理

-   每个hdfs都可以部署两个Namenode，其中一个处于active状态，一个属于standby状态

-   standby Namenode和active Namenode会进行数据同步，以便随时跟换

-   当active Namenode服务器的命名空间发生改变时，它会将日志写入每个DataNode的JournalNode当中

-   standby NameNode会一直监控Journal的变化，将变化运用到的自己的命名空间当中

    

-   standby NameNode和active Namenode切换依靠Zookeeper集群和FailoverController服务

-   本地每一个NameNode都会配置FailoverController服务实例，它会定期监控本地的Namenode状态，并与zkeeper集群保持会话状态

-   Zookeeper会分配给active NameNode一个独占锁，表明他是主节点

-   当active Namenode发生错误时，会返回错误到本地的FailoverController中，然后FailoverController与Zookeeper集群会话断开连接并失效，此时Zookeeper集群会向standby Namenode发起会话，并为它分配新的独占锁,切换为active状态

 如果有两个NameNode，一个是服务状态，还有一个是空闲状态，也就是备用的节点，如果active状态的节点宕机了，那么standy状态的节点就会马上顶上，为了实现这个结果，最主要的就是两台节点的数据必须相同，也就是必须实时共享数据，为了共享实时的数据就不得不新开一个服务，用来同步两台机器的数据了，这个服务叫做journal Nodes（shared Edits）

​	第二个问题，现在有了两台Namenode，也实现了数据同步，按道理来说如果active状态的Namenode死掉了，那么就直接手动切换standy状态的Namenode就可以了，但是对于一个大型数据库，如果有着千万并发量的服务器来说，手动切换消耗的时间造成的损失是巨大的，那么就必须让Hadoop在一台Namenode宕机了，就立马切换到另一台Namenode去，面对这种情况，就需要zookeeper集群发挥作用了，zookeeper集群的ZKFailoverController作为独立进程运行，检测Namenode的健康状态，在主NameNode故障时借助Zookeeper实现自动主备选举和切换

## YARN HA实现原理

-   resourcemanager 和 nodemanager组成了yarn的核心
-   与hdfs类似 resourcemanager可以部署两个实例，其中一个处于active状态，一个处于standby状态
-   两个resourcemanager选举通过zookeeper实现，当active状态的resourcemanager宕机或者重启时，就会触发选举

yarn高可用对于hdfs来所比较简单，因为没有hdfs中对于数据的维护，它少了一个数据同步，它只需要把它的状态信息进行处理就好了， 通过zookeeper的一个监控机制，检测resourcemanager的状态，当resourcemanager出现问题的时候，zookeeper就立马切换到备用的resourcemanager

## zookeeper

zookeeper维护了类似与文件系统一样的znode，当znode发生变化时会通知zookeper客户端

# 搭建

## 安装ZooKeeper

[官网](https://zookeeper.apache.org/)

将官网下载下来的zookeeper传输到export/server当中

![image-20240514154446925](https://db.xinghai.ink/Typora/17349912749975104.png)

解压到当前文件夹

```shell
[hadoop@hadoop01 server]$ tar -zxvf apache-zookeeper-3.9.2-bin.tar.gz -C ./
apache-zookeeper-3.9.2-bin/docs/
apache-zookeeper-3.9.2-bin/docs/images/
apache-zookeeper-3.9.2-bin/docs/skin/
apache-zookeeper-3.9.2-bin/docs/images/2pc.jpg
apache-zookeeper-3.9.2-bin/docs/images/bk-overview.jpg
apache-zookeeper-3.9.2-bin/docs/images/favicon.ico
apache-zookeeper-3.9.2-bin/docs/images/state_dia.dia
apache-zookeeper-3.9.2-bin/docs/images/state_dia.jpg
apache-zookeeper-3.9.2-bin/docs/images/zkAuditLogs.jpg
apache-zookeeper-3.9.2-bin/docs/images/zkarch.jpg
.................................................
pache-zookeeper-3.9.2-bin/lib/jackson-annotations-2.15.2.jar
apache-zookeeper-3.9.2-bin/lib/jackson-core-2.15.2.jar
apache-zookeeper-3.9.2-bin/lib/jline-2.14.6.jar
apache-zookeeper-3.9.2-bin/lib/metrics-core-4.1.12.1.jar
apache-zookeeper-3.9.2-bin/lib/snappy-java-1.1.10.5.jar
[hadoop@hadoop01 server]$ ls
apache-zookeeper-3.9.2-bin  apache-zookeeper-3.9.2-bin.tar.gz  hadoop  jdk
[hadoop@hadoop01 server]$ 
```

删除压缩包，修改文件夹名称为zookeeper

```bash
[hadoop@hadoop01 server]$ ls
apache-zookeeper-3.9.2-bin  apache-zookeeper-3.9.2-bin.tar.gz  hadoop  jdk
[hadoop@hadoop01 server]$ rm apache-zookeeper-3.9.2-bin.tar.gz && mv apache-zookeeper-3.9.2-bin zookeeper
[hadoop@hadoop01 server]$ ls
hadoop  jdk  zookeeper
[hadoop@hadoop01 server]$ 
```

![image-20240514154902253](https://db.xinghai.ink/Typora/17349912771804821.png)

到此，zookeeper安装成功

## 配置环境变量

```bash
export ZOOKEEPER_HOME=/export/server/zookeeper
export PATH=$PATH:$ZOOKEEPER_HOME/bin
```

## 修改配置

配置文件一般来说都放在zookeeper的conf目录下

```bash
[hadoop@hadoop01 server]$ tree zookeeper/conf
zookeeper/conf
├── configuration.xsl
├── logback.xml
└── zoo_sample.cfg

0 directories, 3 files
[hadoop@hadoop01 server]$ 
```

### zoo.cfg

在conf目录下有一个zoo_sample.cfg,这个文件就是zoo的样本文件，把样本文件复制一份，改名为zoo.cfg

```bash
[hadoop@hadoop01 conf]$ ls
configuration.xsl  logback.xml  zoo_sample.cfg
[hadoop@hadoop01 conf]$ cp zoo_sample.cfg zoo.cfg
[hadoop@hadoop01 conf]$ ls
configuration.xsl  logback.xml  zoo.cfg  zoo_sample.cfg
[hadoop@hadoop01 conf]$ 
```

修改里面的内容，在zoo.conf的最下方添加内容

```bash
# 添加三个节点的主机名和访问端口号
server.1=hadoop01:2888:3888
server.2=hadoop02:2888:3888
server.3=hadoop03:2888:3888
# 添加Zookeeper的日志目录路径
dataLogDir=/export/server/zookeeper/logs
# 添加Zookeeper的数据目录路径
dataDir=/export/server/zookeeper/data
```



### Myid

创建myid配置文件，myid文件登记的是每个Zookeeper的节点ip号，id号不能重复

在zoo.cfg文件设置的数据目录路径下面创建一个myid配置文件，并将节点编号写入

![image-20240514170252761](https://db.xinghai.ink/Typora/1734991283244511.png)

## 启动zookeeper

启动zookeeper,需要依次启动各个主机上面的Zookeeper

命令

```bash
zkServer.sh start
```

查看状态：

```bash
zkServer.sh status
```

## 修改Hadoop配置

### core-site.xml

这个文件可以设置zookeeper的地址和端口号，直接在这个文件的其他配置项后面加上

```xml
<property>
	<name>ha.zookeeper.quorum</name>
    <value>hadoop01:2181,hadoop02:2181,hadoop03:2181</value>
</property>
```

## HDFS HA

hadoop高可用包含两个反面，一个是数据同步的方面，一个是自动切换的方面，其实不用zookeeper也可以实现数据同步，但不能自动切换和选举，zookeeper就是用来解决这个问题的

### 手动切换

在hdfs中，有一个journalNode组件，这个组件类似于hdfs，也是一个分布式存储系统，但不是主从结构，它的主要作用就是同步Namenode产生的edit数据，关于journalnode的存储机制，必须一半以上的jornalnode都同步了这个edit才算把这个edit上传成功

所以现在配置的hdfs集群和之前不一样，因为现在多了一个NameNode集群，一台是active状态，其他是standby状态standby状态的主机会定时的从journalnode存储系统中同步namenode元数据

手动切换的配置结构

| hadoop01    | hadoop02    | hadoop03    |
| ----------- | ----------- | ----------- |
| NameNode    | NameNode    |             |
| JournalNode | JournalNode | JournalNode |
| DataNode    | DataNode    | DataNode    |

**core-site.xml**

这个配置有一点需要注意，就是fs.defaultFS配置，它本来是记录namenode的节点url的，在hdfs和mapreduce都发挥作用，但是如果搭建HA时，当namenode宕机了，客户端继续从这个配置信息当中获取url，则对应的就是那台宕机的主机，不符合我们HA的要求

于是乎，这个配置文件也接收一个变量名称，用于指定namenode的集群，而这个名称会在hdfs-site.xml中进行配置，所以这里直接个namenode集群起一个名字就好了

```xml
<property>
	<name>fs.defaultFS</name>
    <value>hdfs://ns</value>
</property>
```

这样就可以了至于它对应哪些namenode的ip和端口，和namenode的分配问题，都在hdfs-site.xml中配置

**hdfs-site.xml**

这个配置文件还是比较重要的

逐条对配置进行解析

```xml
<property>
    <name>dfs.namenode.name.dir</name>
    <value>/export/data/nnode</value>
</property>

<property>
	<name>dfs.datanode.data.dir</name>
    <value>/export/data/dnode</value>
</property>
```

这些配置是设置namenode和datanode的存储路径的,之前配置过，这里不多介绍

```xml
<property>
	<name>dfs.journalnode.edits.dir</name>
    <value>/export/jdata/edits</value>
</property>
```

这个配置是用来设置journalnode的日志数据的本地存放数据，但不仅仅只存放日志，上面提及过，journal是类似于一个分布式存储系统，用来存放namenode的元数据，而这个目录也会被journalnode用来存放元数据，对此我还请来了catgpt回答：

在 Hadoop 的配置中，`dfs.journalnode.edits.dir` 是一个参数，用于配置 JournalNode 存储编辑日志的目录。JournalNode 是 Hadoop HDFS 高可用（HA）架构中的一个重要组件，用于记录 NameNode 的元数据变更。

-   **默认值**：如果没有明确配置 `dfs.journalnode.edits.dir`，JournalNode 会使用默认的临时目录路径。为了避免存储空间的问题和临时目录被清理的风险，通常需要明确配置这个目录，指向一个稳定且有足够存储空间的位置。
-   **重要性**：正确配置 `dfs.journalnode.edits.dir` 对于 HDFS 高可用性非常重要，因为 NameNode 的元数据变更记录在 JournalNode 上，如果存储路径不当或空间不足，可能会导致数据丢失或服务中断。



```xml
<property>
	<name>dfs.nameservices</name>
    <value>ns</value>
</property>
```

在上面的core-site.xml中，我们将hdfs的访问路径设置成了ns，也说过了那其实是一个变量名称，而这个配置就是用来定义ns是namenode集群的路径的意思，再次用gpt回答一下：

在 Hadoop HDFS 的配置中，`dfs.nameservices` 参数用于指定集群中的命名服务（NameService）的名称。这个参数是配置 HDFS 高可用性（HA）和联邦（Federation）时所必需的。以下是对该配置项的详细解释：

-   **`<name>dfs.nameservices</name>`**: 这是配置项的名称，用于指定 HDFS 集群中命名服务的名称。
-   **`<value>ns</value>`**: 这是配置项的值，表示命名服务的名称。在这个例子中，命名服务的名称是 `ns`。

 联邦（Federation）

在 HDFS 联邦配置中，你可以定义多个命名服务，每个命名服务都有自己的独立命名空间。以下是一个简单的联邦配置示例：

![image-20240517144415366](https://db.xinghai.ink/Typora/17349912884924376.png)

-   **`dfs.nameservices`**：指定了集群中的命名服务名称，在高可用配置中用于标识 NameNode 集群，在联邦配置中用于标识多个独立的命名空间。
-   **高可用性（HA）配置**：确保在主备 NameNode 之间正确切换。
-   **联邦（Federation）配置**：允许多个独立的命名空间，提高 HDFS 的可扩展性和管理灵活性。

通过正确配置 `dfs.nameservices` 以及相关参数，HDFS 可以实现高可用性和联邦，从而提高系统的可靠性和扩展性。

```xml
<property>
	<name>dfs.ha.namenodes.ns</name>
	<value>n1,n2,n3</value>
</property>
```

```xml
 <property>
    <name>dfs.namenode.rpc-address.ns.n1</name>
    <value>hadoop102:8020</value>
  </property>
  <property>
    <name>dfs.namenode.rpc-address.ns.n2</name>
    <value>hadoop103:8020</value>
  </property>
  <property>
    <name>dfs.namenode.rpc-address.ns.n3</name>
    <value>hadoop104:8020</value>
  </property>
```

这两个配置文件放在一起讲，我们知道ns已经被指定成hdfs当中的namenode的访问地址，那么这里就是用来配置这个访问地址具体是指向哪些ip

dfs.namenode.namenodes.ns配置项ns下面有哪些namenode，但是这里还是用的变量，变量对应的ip和地址在下面的dfs.namenode.rpc-address.ns.n1中配置，其中ns代表的是ns命名空间，n1代表的是ns当中的具体主机，value当中设置的就是真正的ip地址和端口，这么讲有点绕，对此我专门用了gpt：

不能直接在 `dfs.ha.namenodes.mycluster` 中使用 `hadoop01:8020` 的格式。你需要为每个 NameNode 提供单独的 RPC 地址配置。这样做是为了清晰地定义每个 NameNode 的网络地址，使得集群能够正确地处理 NameNode 的高可用性和故障切换。

在配置 Hadoop NameNode 高可用性时，`dfs.ha.namenodes.mycluster` 是用来列出集群中所有 NameNode 的标识符，这些标识符在后续的配置中被引用，以便明确每个 NameNode 的具体地址和端口等信息。因此，直接在 `dfs.ha.namenodes.mycluster` 中使用 `hadoop01:8020` 的格式是不行的。你需要为每个 NameNode 提供单独的配置来指定它们的 RPC 地址和其他相关信息。

在配置 Hadoop 的高可用性 NameNode 时，`dfs.ha.namenodes.<nameservice>` 只能列出标识符，用来标识集群中所有的 NameNode。这些标识符（如 `nn1` 和 `nn2`）之后会被用来具体配置各个 NameNode 的 RPC 地址、HTTP 地址等。实际的网络地址（主机名和端口）需要在其他配置项中单独指定。



以上的解释，我的理解是：

首先dfs.nameservices配置的是各种命名空间名称，dfs.ha.namenode.(命名空间名称)配置的是这个命名空间的具体主机的名称，dfs.namenode.rpc-address.(命名空间名称).(主机名称)配置的是命名空间里面具体的主机的ip和端口号

具体结构了解之后，解释一下关于rpc的，这里的配置项名称用的是rpc-address这个意思是，它用rpc协议来进行通信，是用来构建客户端和服务器，服务器和服务器之间的连接的



```xml
 <property>
    <name>dfs.namenode.http-address.mycluster.nn1</name>
    <value>hadoop102:9870</value>
  </property>
```

http地址就不多说了，配置好启动之后，直接在浏览器输入hadoop01:9870访问，这个可以不配置，会有默认的配置信息，但为了可读性最好写上

```
<property>
<name>dfs.namenode.shared.edits.dir</name>
<value>qjournal://hadoop01:8485;hadoop02:8485;hadoop03:8485/mycluster</value>
</property>
```

这个配置项配置的是namenode的元数据在journalnode中的存放路径，注意：这不是本地的路径而是一整个集群的存放路径，这里三台主机代表的不是namenode，代表的是journalnode服务的主机和端口

gpt：

具体地说，这个配置项的含义如下：

-   **dfs.namenode.shared.edits.dir**: 这是一个配置属性，指定了共享编辑日志的存储位置。
-   qjournal://hadoop102:8485;hadoop103:8485;hadoop104:8485/mycluster:
    -   **qjournal**: 表示使用 Quorum Journal Manager (QJM) 进行共享编辑日志的管理。
    -   **hadoop102:8485;hadoop103:8485;hadoop104:8485**: 这是三个 JournalNode 的地址和端口，HDFS 集群会使用这些 JournalNode 来存储和管理编辑日志。这里有三个节点（`hadoop102`、`hadoop103` 和 `hadoop104`），端口号都是 8485。
    -   **mycluster**: 这是 Journal 集群的标识符，用于区分不同的 Journal 集群。

```xml
<property>
	<name>dfs.client.failover.proxy.provider.mycluster</name> 			<value>org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider</value>
</property>
```

这个配置是故障转移，当客户端访问active状态下的服务器出现故障，就会转到其他的namenode的服务器地址，前提是服务器在配置文件配置过

`dfs.client.failover.proxy.provider.mycluster` 这个配置项是针对客户端的，它指定了客户端用于故障转移的代理提供者。这个配置告诉客户端系统如何处理故障转移，以便在主 NameNode 发生故障时自动切换到备用 NameNode。

具体来说，这个配置项告诉客户端系统使用哪种故障转移代理提供者来管理故障转移过程。例如，`org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider` 是一个内置的故障转移代理提供者，它通过配置文件中指定的所有 NameNode 地址来实现故障转移。

客户端会根据这个配置项来选择合适的故障转移代理提供者，并使用它来处理故障转移

1.  **第一次连接**：
    -   客户端通常会尝试连接到配置的NameNode地址列表中的第一个地址。
    -   如果连接成功，它会与该NameNode建立连接，并在之后的请求中使用该连接。
    -   如果连接失败，客户端会尝试连接配置的其他NameNode地址，直到成功连接或尝试完所有地址。
2.  **连接成功后的行为**：
    -   一旦客户端成功连接到一个NameNode，它会在此之后继续使用该连接，直到连接断开。
    -   如果在连接成功后，Active NameNode出现问题，通常客户端不会立即断开连接，而是继续使用现有的连接，直到检测到问题或收到来自NameNode的错误响应。
3.  **故障转移**：
    -   如果客户端在连接期间检测到与Active NameNode的连接失败，或者收到Active NameNode的错误响应，它将尝试使用配置的故障转移策略进行切换。
    -   如果设置了`dfs.client.failover.proxy.provider.mycluster`，客户端将根据该配置进行故障转移，尝试连接到备用的NameNode。
    -   在故障转移期间，客户端会尝试连接到备用NameNode，并继续处理请求，以确保服务的连续性。

```xml
  <property>
    <name>dfs.ha.fencing.methods</name>
    <value>sshfence</value>
  </property>
```

这个配置是用来保证hdfs不脑裂，也就是不同时出现两个active状态的namenode，当故障恢复时或者说故障转移后，之前的namenode突然复活了，然后出现了多个active 状态的namenode，这个配置就是切断active状态的方式，这里用的是ssh方式，就是通过ssh登入到对应的namenode然后弄死他

gpt的解释是：

![image-20240517172513312](https://db.xinghai.ink/Typora/1734991293194948.png)
