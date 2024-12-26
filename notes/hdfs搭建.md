## 数据科学流水线和Hadoop生态系统

​	数据科学流水线是一种教学模型，用于教授对数据进行全面统计分析所需的工作流，如图 1-1 所示。在每个环节中，分析人员要转换初始数据集，然后从各种数据源增强或采集数据，再通过描述性或推断性的统计方法将数据整理为可以计算的正常形式，最后通过可视化或报告的形式生成结果。这些分析过程通常用于回答特定问题，或用于调查数据与某些业务实践间的关系，以进行验证或决策。

![](https://db.xinghai.ink/Typora/1734991337022048.jpeg)

​										图 1-1：数据科学流水线

​	这个原始的工作流模型引领了大多数早期的数据科学思想。最初关于数据科学应用程序的讨论围绕着如何创建有意义的信息可视化——这也许令人意外，主要是因为这个工作流旨在生成帮助人们进行决策的依据。通过对大型数据集的聚合、描述和建模，人们能够更好地根据模式（而不是单个数据点）作出判断。数据可视化是新生的数据产品，它们从数据中产生价值，帮助人们基于学习到的内容采取行动，然后再从这些行动中生成新数据。然而，面对呈指数增长的数据量和数据增长速度，这种以人力驱动的模型并不是一个可扩展的解决方案，这也正是许多企业都为之抓狂的原因。根据预测，到 2020年，我们每年生成和复制的数据将达到 44ZB，即 44 万亿 GB。即使实际规模只达到预测规模的一小部分，手动的数据准备和挖掘方法也根本无法及时提供有意义的信息。

​	除了规模上的局限，这种以人为中心的单向工作流也不能有效地设计能够学习的自适应系统。机器学习算法已经广泛应用于学术界之外，非常符合数据产品的定义。因为模型会拟合现有的数据集，所以这些类型的算法可以从数据中获取价值，然后通过对新的观察值作出预测来产生新的数据。如果要创建一个框架，支持构建可扩展和可自动化的解决方案，从而能解释数据和生成有用的信息，就必须修改数据科学流水线，使其包含机器学习方法的反馈循环。

​	大数据工作流考虑到可扩展性和自动化的目标，我们可以将人力驱动的数据科学流水线重构为包括采集、分段、计算和工作流管理这 4 个主要阶段的迭代模型（如图 1-2 所示）。与数据科学流水线一样，这种模型其实就是采集原始数据并将其转换为有用的信息。关键的区别在于，数据产品流水线是在操作化和自动化工作流的步骤中构建起来的。通过将采集、分段和计算这 3 个步骤转换为自动化工作流，最终产生可重用的数据产品。工作流管理步骤还引入了反馈流机制，来自其中一个作业执行的输出可以自动作为下一次迭代的数据输入，因此为机器学习应用程序提供了必要的自适应框架。

![](https://db.xinghai.ink/Typora/17349913394646487.jpeg)

​										图 1-2：大数据流水线

​	采集阶段既是模型的初始化阶段，也是用户和模型之间的应用交互阶段。在初始化期间，用户指定数据源的位置或标注数据（另一种数据采集形式）；在交互期间，用户消费模型的预测结果并提供用于巩固模型的反馈。分段阶段是转换数据的阶段，使其变为可消费的形式并存储起来，从而能够用于处理。本阶段还负责数据的归一化和标准化，以及一些计算数据存储中的数据管理工作。计算阶段是真正“干活”的阶段，主要负责挖掘数据以获取有用的信息，执行聚合或报告，构建用于推荐、聚类或分类的机器学习模型。工作流管理阶段执行抽象、编排和自动化任务，使工作流的各步骤可用于生产环境。此步骤应能产生自动按需运行的应用程序、作业或脚本。Hadoop 已经演变成了包含各种工具的生态系统，可以实现上述流水线的部分环节。例如，Sqoop 和 Kafka 可用于数据采集，支持将关系数据库导入 Hadoop 或分布式消息队列，以进行按需处理。在 Hadoop 中，像 Hive 和 HBase 之类的数据仓库提供了大规模的数据管理机会；Spark 的 GraphX、MLlib 或 Mahout 库提供了分析包，供大规模计算和验证使用

## Hadoop安装

​	安装Linux（3台），配置局域网和IP，三台机器主机映射,主机名称分别为hadoop01、hadoop02、hadoop03
​	安装Hadoop以root用户进行
​	使用Hadoop以Hadoop用户进行

Hadoop是基于java语言开发的，要运行Hadoop就必须安装jdk

### **下载jdk：**

​	[oracle官网](https://www.oracle.com/cn/java)

### **下载Hadoop：**

​	[apache Hadoop官网](https://hadoop.apache.org/)

![image-20240414145206341](https://db.xinghai.ink/Typora/17349913452994227.png)

在根目录下面创建export/server文件夹，用于存放Hadoop和jdk

![image-20240414145649939](https://db.xinghai.ink/Typora/173499134859235.png)

将Hadoop和jdk放到server文件夹内

![image-20240414150231183](https://db.xinghai.ink/Typora/1734991350612634.png)

### **安装jdk：**

jdk以rpm格式打包，直接用[rpm命令](..\Linux\Linux命令.md)执行安装

安装好jdk，改好文件名称

![image-20240414155915527](https://db.xinghai.ink/Typora/17349913531611142.png)

### **安装Hadoop：**

使用[tar命令](..\Linux\Linux命令.md)解压至当前文件夹即可

```shell
[root@hadoop01 server]# tar -zvfx hadoop-3.4.0
```

改名

![image-20240414160547068](https://db.xinghai.ink/Typora/17349913585996263.png)

## 配置环境

### 将jdk添加到环境变量

添加jdk文件当中的bin目录和lib目录添加至环境变量

```
JAVA_HOME=/export/server/jdk
export PATH=$PATH:$JAVA_HOME/bin:$JAVA_HOME/lib
```

更新环境变量

![image-20240414164047046](https://db.xinghai.ink/Typora/17349913664622784.png)

### 将Hadoop添加到环境变量

将Hadoop中的bin和sbin目录添加到环境变量

![image-20240414164409860](https://db.xinghai.ink/Typora/17349913688079064.png)

![image-20240414164349779](https://db.xinghai.ink/Typora/17349913706242.png)

## 时钟同步

因实际要求保证服务器之间[时间同步](https://so.csdn.net/so/search?q=时间同步&spm=1001.2101.3001.7020)。
方式：1、通外网。直接时间服务器同步。
2、本地搭建时间服务器进行同步。
其实这两种方式可合并为一种。

安装ntp服务

```shell
[root@hadoop01 hadoop]# yum install ntp
```

后面的暂时不会。。。

## Hadoop配置与启动详解

一下配置先在一台主机完成，稍后再复制过去

### hadoop-env.sh配置

在Hadoop中，配置文件都会统一放在$HADOOP_HOME/etc/hadoop当中，文件夹如图

![image-20240424224855768](https://db.xinghai.ink/Typora/17349913731008756.png)

我们将要对这里的配置文件进行配置

​	在配置之前，我们尝试一下能不能启动Hadoop，之前我们对hadoop的环境变量进行设置，也就是将$hadoop_home/bin添加到环境变量文件/etc/profile当中，我们可以直接看一下$hadoop_home/bin到底有什么，我们打开它，可以看见

![image-20240424225225531](https://db.xinghai.ink/Typora/17349913748788521.png)

​	这里面放置的都是可执行文件，也就是命令，我们之前把这个目录添加到环境变量当中，说明我们可以在任意目录下面执行这个目录里面放置的可执行文件。我们试着可不可以执行hadoop命令

![image-20240424225401843](https://db.xinghai.ink/Typora/17349913788196068.png)

​	可以看见，执行Hadoop后，系统并没有指出Hadoop命令不存在，反而提出一个错误，表示Hadoop找不到java的家目录，之前提到过，Hadoop是需要运行在java上面的，于是我们安装了java，但是Hadoop并不知道java在哪里，所以Hadoop就不能被启动成功，为了解决这个问题，我们要在hadoop的配置文件当中指明java的路径，也就是直接告诉hadoop，java在哪个位置

​	我们打开hadoop的配置文件，$hadoop_home/etc/hadoop,我们需要修改的是hadoop-env.sh的文件，这个文件看后缀就知道是个shell脚本文件，那这个文件是什么呢？hadoop-env.sh 文件是Hadoop 的一个环境变量配置文件，注意，是hadoop当中的环境变量文件，并不对全局变量环境起效果，这个文件用于配置Hadoop 的全局环境变量，我们将要配置的是$JAVA_HOME

我们实战开始，首先用vim打开hadoop-env.sh文件，可以看到

![image-20240424230947162](https://db.xinghai.ink/Typora/17349913809067347.png)

基本上都是注释文件，但还是可以发现文件中有 export JAVA_home的字样，我们需要修改的就是这个，我们直接将java的目录写在后面

![image-20240424231520993](https://db.xinghai.ink/Typora/17349913828907402.png)

​	如上图所示，但请注意，把前面的注释去掉，也就是将前方的#号删除，因为注释下的变量没有任何意义

​	我们保存关闭文件之后，hadoop环境变量会立即生效，我们再次启动一下hadoop

![image-20240424231646975](https://db.xinghai.ink/Typora/17349913870249608.png)

可以发现，执行hadoop命令后，会弹出一大堆帮助，这个时候就说明hadoop的环境变量设置成功了

### Hadoop介绍

​	这里主要介绍Hadoop是什么，我们已经可以使用Hadoop命令了，这个时候说明输入Hadoop命令Hadoop就启动了吗？其实不然Hadoop是一个框架，它是由Java语言来实现的。Hadoop是处理大数据技术.Hadoop可以处理云计算产生大数据，hadoop并不是云计算。它和云计算密不可分。Hadoop产生是互联网的产物，也是必然。大家都知道，我们上网时需要服务器的。假如世界上只有一台电脑，根本不需要服务器。如果有10台服务器，100台，1000台，上万台，那么我们该如何让大家相互通信，共享知识，所以我们产生了互联网。
​    互联网产生，全世界都可以通信，知识如此居多，我们像获取更多的知识，想获取新技术，获取新知识，通过什么，国内通过百度，国外也有许多，比如Google。可是百度和谷歌的用户有多少，多了不说，最起码有上亿的用户。并且这些用户每天上百度，上谷歌，又会产生多少数据，查询多少数据。那么他们怎么承受如此多用户。
​    这不是一台电脑、一台服务器能完成的事情。Hadoop就是一个解决方案。Hadoop是一个分布式方案，能够把压力分摊到其他服务器。至于如何做到的，这也就是我们需要学习的。

​	Hadoop 框架主要由三大模块组成，这三个模块协同运行以形成 Hadoop 生态系统：

​	Hadoop Distributed File System (HDFS)：作为 Hadoop 生态系统的主要组件，HDFS 是一个分布式文件系统，可提供对应用数据的高吞吐量访问，而无需预先定义架构。

​	Yet Another Resource Negotiator (YARN)：YARN 是一个资源管理平台，负责管理集群中的计算资源并使用它们来调度用户的应用。它在整个 Hadoop 系统上执行调度和资源分配。

​	MapReduce：MapReduce 是一个用于大规模数据处理的编程模型。通过使用分布式和并行计算算法，MapReduce 可以沿用处理逻辑，并帮助编写将大型数据集转换为可管理数据集的应用。

​	简单来说，HDFS就是用来存储文件的，当然，他不可能是单一的硬盘，而是运行再多台服务器上的存储系统，当我们存储数据的时候，HDFS就会把数据分成多份，存入不同的服务器上，MapReduce是用来处理和计算数据的，而yarn就是负责管理计算机的资源，起到分配性能的作用。就好像一个公司有三大部门，每一个部门负责不同的工作，缺一不可。所以，想要启动HADOOP的完整功能就需要一一启动Hadoop集群的组件。

## HDFS配置

​	上面所说，HDFS是一个分布式是存储系统，而这个系统采用的是一台管理系统和多台存储节点系统，也就是一个部门，一个人负责管理和协调，一堆人负责干活（存储文件），而那个负责人，我们叫做NameNode，干活的工人，我们叫做DataNode，一个NameNode管理多台DataNode，我们要启动Hadoop当中的HDFS可不是启动某个主机上的DataNode,而是启动整个HDFS系统上的所有节点，也就是老大（NameNode）和小弟(DataNode)全部启动，一个都不能放过。

​	我们在之前设置Hadoop环境变量当中，把Hadoop家目录下的sbin文件夹也配置成了环境变量，那么我们去看看，$HADOOP_HOME/sbin里面到底有什么

![image-20240425133403914](https://db.xinghai.ink/Typora/1734991395792463.png)

​	可以看到，这一堆绿色的就是可执行文件，这里面放置的都是Hadoop组件的管理命令，其中包括start-dfs.sh，也就是启动HDFS生态的命令，好了，新的问题出现了,HDFS生态如果要启动，HDFS怎么知道哪个主机是NameNode，哪些是DataNode呢？这就是我们要学习的HDFS配置。

​	我们现在的目标是正常的启动hdfs，其他的现在的先不管，到后面hdfs文章再做介绍，想要启动hdfs，基础的配置就是设置谁是老大（Namenode），谁是小弟（Datanode），只要设置好这个，hdfs的启动就不成问题，那么介绍配置的时候先简单提一下hdfs的启动过程，假设我们现在有三台主机，我们在任意一台主机执行一键启动hdfs的命令，那么这台主机所执行的流程如下，首先在配置文件当中寻找namenode的主机，找到namenode的主机后就给namenode主机发送启动namenode的命令，当然，他只管发送命令，至于namenode能不能启动，这个是决定不了的，发送完成命令后继续在配置文件中寻找datanode的主机，找到datanode主机后，给该主机发送启动namenode的命令，至此，启动完成，所以，我们需要配置的无非就是namenode的主机和datanode的主机，对应的文件就是workers和core-site.xml

​	我们打开Hadoop的统一配置文件夹的目录，$HADOOP_HOME/etc/hadoop，我们可以看到当中有一个workers文件，这个文件就是用来配置从节点的文件，也就是规定，谁是DataNode，注意，在3.0版本之前这个文件叫做slave，也就是把之前的奴隶改成了现在的工人。接下来我们配置一下

首先我们在主节点的主机配置NameNode，其他主机配置DataNode，hadoop01用vim打开workers

![image-20240425183226000](https://db.xinghai.ink/Typora/17349913999144711.png)

​	可以看到，这里的localhost代表的是自己，因为现在配置的是hadoop01的主机，也就是主节点，这里就不把自己当工人（从节点）了，把localhost删除，添加hadoop02和hadoop03这两个主机名称，就可以将hadoop02和hadoop03收入到hadoop01麾下打工。

![image-20240425184221655](https://db.xinghai.ink/Typora/17349914014629574.png)



​	关于workers文件的内容，我们刚才在里面输入的都是hadoop02和hadoop03的主机名字，那么，hadoop01主机怎么知道hadoop02和hadoop03是哪个主机呢？这一点，会Linux的都需要知道，我们之前在/etc/host文件里面设置的就是主机名和ip的映射关系，这里面看似设置的是主机名称，实则Hadoop会在host文件中找到这个名称对应的ip地址。

![image-20240425185210262](https://db.xinghai.ink/Typora/17349914037302697.png)

​	设置好从节点之后需要配置core-site.xml文件，也就是设置集群中的老大节点，namenode，这个从名字可以看出是一个核心文件，看后缀可以看出是xml文件，xml是一个规定好的格式的语言，就是一个文本，我们都按照这个格式去写，方便程序交换和提取数据

core-site.xml也是放在hadoop的统一配置文件夹当中，用vi打开

![image-20240425190856766](https://db.xinghai.ink/Typora/1734991405367306.png)

会html的都知道，<!--“内容”-->这个格式表示的就是注释的意思，没有实际意义，我们需要配置的就是<configuration></configuration>键值对当中的内容，如下：

```xml
<configuration>
        <property>
         <name>fs.defaultFS</name>
         <value>hdfs://hadoop01:8020</value>
        </property>
</configuration>
```

​	介绍一下格式，这里的configuratino就是配置的意思，而两个configuration表示在两个configuration的中间写入配置的信息，其他标签对的写法都差不多，比如<property></property>表示的是一个配置信息，配置信息在property中间写入，配置信息由键和值组成，键就是name,值就是value，比如第一条信息，键就是fs.defaultFS,值就是hdfs://hadoop01:8020,这就是告诉配置文件，我要配置的是叫fs.defaultFs的东西，我要把它配置成hdfs://hadoop01:8020。fs.defaultFS配置的是namenode的主机和端口，只有这样，hdfs才能正确的找到namenode。

至此，配置完成

配置完成后，我们需要在所有主机上都复制一遍，因为三台主机的配置文件都一样，所以我们直接把/export这一整个目录复制过去

![image-20240502220936252](https://db.xinghai.ink/Typora/17349914116704416.png)

执行上面这个命令，scp命令是ssh当中的命令，意思是远程复制文件，-r是表示复制一整个文件夹，紧接着/export是需要复制的目录，后面的root是目标主机的用户名，因为只有root用户才有权限将目录复制到根目录，所以采用目标主机的root用户，@hadoop02是主机，冒号后面是目录，这里复制到的地方是对方的更目录，整体的意思就是，将本地主机当中的/export文件夹以hadoop02主机当中的root用户发方式复制到对方主机的根目录当中。

执行命令后，输入对方主机的root用户的密码，等待复制完成。

复制完成之后，继续用同样的命令，复制到hadoop03主机当中

![image-20240502221653570](https://db.xinghai.ink/Typora/17349914161804788.png)

完成后，我们需要将hadoop和jdk当中的命令设置环境变量，这样，在linux当中的任意一个文件夹位置当中都可以执行hadoop和java的命令，hadoop02和hadoop03没有设置过，所以都要设置，具体设置如下，在/etc/profile当中添加以下配置：

![image-20240502221911043](https://db.xinghai.ink/Typora/17349914203151097.png)

全部设置好后，集群就搭配完成了

在启动之前，需要对namenode的那台主机进行namenode的格式化，格式化的作用是初始化一些必要的参数，增加一些目录，具体的作用，在hdfs文章中会讲到。

因为我们选用hadoop01作为namenode，所以，我们在hadoop01上面执行以下命令格式化namenode

![image-20240502222356267](https://db.xinghai.ink/Typora/17349914251690876.png)

执行完成之后，就可以正常启动hdfs了

hdfs --daemon start namenode

启动namenode的命令

jps用来查看进程

![image-20240502222613020](https://db.xinghai.ink/Typora/17349914288755002.png)

hdfs --daemon start datanode

启动datanode的命令，这里我们在hadoop02和hadoop03当中启动

![image-20240502222738749](https://db.xinghai.ink/Typora/17349914322648585.png)

![image-20240502222753991](https://db.xinghai.ink/Typora/17349914360672188.png)



hdfs --daemon stop namenode

hdfs --daemon stop datanode

停止namenode和停止datanode的命令



当我们启动成功之后，我们可以在浏览器当中输入namenode的主机ip加上9870端口，这个类似于hdfs给出的客户端

![image-20240502223107756](https://db.xinghai.ink/Typora/17349914400821419.png)

我们点击上方的datanodes按钮

![image-20240502223139889](https://db.xinghai.ink/Typora/17349914458101552.png)

可以看到，我们两台datanode都在正常运行当中，hdfs搭建完成。

## 参考资料

大数据学习笔记. (n.d.). Retrieved April 25, 2024, from https://chu888chu888.gitbooks.io/hadoopstudy/content/

Apache Hadoop 概览. (n.d.). Retrieved from https://cloud.google.com/learn/what-is-hadoop?hl=zh-cn

