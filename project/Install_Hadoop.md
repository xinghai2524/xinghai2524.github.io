# Hadoop 配置

# 一    安装 Linux

这里使用`Ubuntu`搭建`hadoop` , 打开`ubuntu server`官网https://cn.ubuntu.com/download/server/step1

点击`下载Ubuntu Server 24.04.1 LTS`

![image-20250209170435913](https://db.xinghai.ink/Typora/17390918782599614.png)

下载好后，打开`VMware`, 新建虚拟机

![image-20250209204645351](https://db.xinghai.ink/Typora/17391052170775812.png)

具体配置如下![image-20250209204918387](https://db.xinghai.ink/Typora/17391053655096533.png)

按照提示安装Ubuntu，在网络选项中，先不连接网络，这样能加快安装速度

![image-20250209205229160](https://db.xinghai.ink/Typora/1739105551583956.png)

输入账号密码登入，就安装好了

![image-20250209210151609](https://db.xinghai.ink/Typora/17391061142092364.png)

# 二    配置网络

在使用linux之前需要配置好局域网

在VmWare中，配置虚拟网卡，用于组建局域网

![image-20250209210512938](https://db.xinghai.ink/Typora/1739106315468062.png)



将子网ip设置为一个`网段`（就是最末尾是0的ip），然后点击NAT，将网关设置为这个网段的第二个ip

![image-20250209210636737](https://db.xinghai.ink/Typora/17391063988556435.png)

设置好网关之后，在`ubuntu`里面打开`/etc/netplan`文件夹，由于Ubuntu使用netplan管理网络，所以在这里找到配置文件进行配置



![image-20250209210927321](https://db.xinghai.ink/Typora/17391065693381455.png)

这里的配置文件是 `50-cloud-init.yaml`，使用vim进行配置

```shell
sudo vim 50-cloud-init.yaml
```

配置文件如下

```yaml
network:
    ethernets:
        ens33:
            dhcp4: no
            addresses: [192.168.56.101/24]
            gateway4: 192.168.56.2
            nameservers:
                addresses: [223.5.5.5, 8.8.8.8]
    version: 2
```

![image-20250209211533219](https://db.xinghai.ink/Typora/17391069356011717.png)

配置完成后，保存退出

使用 `netplan apply`命令应用配置

```shell
sudo netplan apply
```

![image-20250209211655630](https://db.xinghai.ink/Typora/17391070173532767.png)

这时，使用`ip a`命令查看网络，就可以看到网络配置成功了，`ens33`网卡的ip为配置文件的ip

![image-20250209211811408](https://db.xinghai.ink/Typora/17391070929542947.png)

使用`ping`命令检测网络是否可用

![image-20250209211912403](https://db.xinghai.ink/Typora/17391071543354309.png)

至此，网络配置完成

# 三    配置SSH

为了有更高的开发效率，一般会使用搭建ssh，然后从ssh客户端进行远程开发

搭建ssh，首先需要下载ssh

```
sudo apt-get install ssh
```

![image-20250209212214619](https://db.xinghai.ink/Typora/17391073363287241.png)

这里输入Y，然后等待安装完成

![image-20250209212310872](https://db.xinghai.ink/Typora/17391073933102071.png)

安装完成后，使用`systemctl`命令启动`ssh`，并且设置为`开机自启动`

**启动ssh**

```
sudo systemctl restart ssh
```

![image-20250209212436850](https://db.xinghai.ink/Typora/17391074786707587.png)

**设置为开机自启动**

```
sudo systemctl enable ssh
```

![image-20250209212546207](https://db.xinghai.ink/Typora/17391075482076845.png)



为了让ssh客户端可以用账号密码登入，所以需要修改ssh配置使用`vim`编辑`ssh`的配置文件`/etc/ssh/sshd_config`

```shell
sudo vim /etc/ssh/sshd_config
```

![image-20250209214832345](https://db.xinghai.ink/Typora/17391089144841855.png)

将`PasswordAuthentication yes`，取消注释,然后重启`ssh`

```shell
sudo systemctl restart ssh
```

最后在ssh客户端中连接服务器

![image-20250209215229521](https://db.xinghai.ink/Typora/1739109151431949.png)

成功

# 四    安装jdk

Hadoop 是基于 java开发的，所以运行hadoop需要安装java，**Java 8**（JDK 1.8）：这是 Hadoop 3.x 最广泛支持和推荐的版本，所以这里下载Java8

## 4.1    下载jdk

打开[官网](https://www.oracle.com/cn/java/technologies/downloads/)，往下滑，找到java8

![image-20250209231249933](https://db.xinghai.ink/Typora/173911397226344.png)

然后往下滑，找到对应的版本，由于`ubuntu`不支持`rpm`，所以我这里下载`x64`的`tar.gz`版本

![image-20250209231352116](https://db.xinghai.ink/Typora/17391140343043573.png)

**下载好后上传到Ubuntu中**

![image-20250209231436639](https://db.xinghai.ink/Typora/17391140783147619.png)



## 4.2    安装jdk

在压缩包的目录下，使用`tar`命令给压缩包解压

```shell
tar -zxvf jdk-8u441-linux-x64.tar.gz
```

解压成功后，会有一个解压的文件夹

![image-20250209231659094](https://db.xinghai.ink/Typora/17391142210925257.png)

为了方便后续使用，将这个文件夹名称改成`java`

```shell
mv jdk1.8.0_441 java
```

然后打开j`ava`目录，打开里面的`bin`目录，再使用`./java`命令测试是否成功

![image-20250209231918816](https://db.xinghai.ink/Typora/1739114361404327.png)

可以看到，我这里成功了

## 4.3    配置环境变量

为了方便后续使用，这里配置一下环境变量，这样使用`java`就不用每次都去`bin`目录里面调用了

使用vim 编辑家目录的` .bashrc`

```
 vim ~/.bashrc
```

在最后添加

```bash
export JAVA_HOME=/home/hadoop01/app/java/java
export PATH=$PATH:$JAVA_HOME/bin
```

![image-20250209232504606](https://db.xinghai.ink/Typora/1739114707013793.png)

然后保存退出,使用`source ~/.bashrc`刷新环境变量

```
source ~/.bashrc
```

最后在任意一个目录使用`java`

```shell
java -version
```

![image-20250209232639879](https://db.xinghai.ink/Typora/17391148017486765.png)

# 五    安装Hadoop

## 5.1    下载Hadoop

浏览器搜索`Hadoop`，打开官网

![image-20250210035325544](https://db.xinghai.ink/Typora/17391308091547387.png)

在官网中，选择`下载`,这里选择最新版本

![image-20250210035425372](https://db.xinghai.ink/Typora/17391308676170883.png)

任意选择一个连接进行下载，下载后传入`Ubuntu`中

![](https://db.xinghai.ink/Typora/17391308943195992.png)

## 5.2    配置Hadoop

将`Hadoop`上传到`Ubuntu`中之后，使用`tar`命令进行解压

```shell
tar -zxvf hadoop-3.4.1.tar.gz
```

![image-20250210035824508](https://db.xinghai.ink/Typora/17391311065324244.png)

解压后，给文件夹改个名

```shell
 mv hadoop-3.4.1 hadoop
```

进入`hadoop`的`bin`目录，这里是所有`hadoop`的命令

![image-20250210040323119](https://db.xinghai.ink/Typora/17391314051374903.png)

执行其中的`hadoop`命令

```shell
./hadoop
```

![image-20250210040510805](https://db.xinghai.ink/Typora/17391315128529673.png)

可以发现执行成功了，但如果提示找不到`Java`的错误，就有可能没有配置好`Java`的环境变量，好在Hadoop也是可以直接指定某个`Java`

`hadoop`目录的`etc/hadoop/hadoop-env.sh`是Hadoop基础的配置文件，在个文件中可以指定`Java`的家目录

```shell
vim hadoop-env.sh
```

![image-20250210040912793](https://db.xinghai.ink/Typora/17391317545679104.png)

加入`java`的目录即可

![image-20250225230845659](https://db.xinghai.ink/Typora/17404961388048708.png)

