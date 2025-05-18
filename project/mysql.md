## 前言

在写这个笔记的时候已经是在用mysql做项目了，所以mysql基本的命令不会出现，这里主要记录的是mysql服务器搭建以及与项目相关的问题

## 下载MySQL

下载deb仓库包，然后用apt安装这个deb包，然后直接用apt安装mysql-server

### 官网下载dep仓库

打开[官网](https://dev.mysql.com/downloads/)，选择apt仓库

![image-20240820093802928](https://db.xinghai.ink/Typora/17349915041358533.png)

下载仓库

![image-20240820093901108](https://db.xinghai.ink/Typora/17349915100830595.png)

将deb包传入Linux

![image-20240820094006086](https://db.xinghai.ink/Typora/17349915146093204.png)

用apt命令安装deb仓库包

```shell
xinghai@matebook:~/app$ sudo apt-get install ./mysql-apt-config_0.8.32-1_all.deb
Reading package lists... Done
Building dependency tree
Reading state information... Done
Note, selecting 'mysql-apt-config' instead of './mysql-apt-config_0.8.32-1_all.deb'
mysql-apt-config is already the newest version (0.8.32-1).
The following packages were automatically installed and are no longer required:
  libmecab2 mecab-ipadic mecab-ipadic-utf8 mecab-utils mysql-community-client-core mysql-community-client-plugins
  mysql-community-server-core
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 49 not upgraded.
xinghai@matebook:~/app$
```

这里是已经安装了

安装mysql

```
sudo apt-get install mysql-server
```

安装完成

## 用户管理

MySQL用户主要包括两种：root用户和普通用户。root用户为超级管理员，拥有MySQL提供的所有权限，而普通用户的权限取决于该用户在创建时被赋予的权限有哪些。实际开发中很少直接使用root用户，权限过大，操作不当会具有很大的危险性

MySQL中有一个自带数据库mysql，其中有多个和用户权限有关的数据库表。

-   user表中存储了允许连接到服务器的用户信息以及全局级（适用于所有数据库）的权限信息。这是最关键的表；

-   db表中存储了某个用户对相关数据库的权限（数据库级权限）信息；
-   表级权限表tables_priv，可以实现单张表的权限设置；
-   列级权限表columns_priv，可以实现单个字段的权限设计；

### 创建用户

**命令**

```
create user "username"@"host" identified by "passwd"
```

-   username：将要创建的用户名
-   host：指定可以登入的主机，如果是本地则用localhost，如果想让用户从任意主机上远程登入，则用通配符%，还可以指定ip范围，不指定主机默认为通配符
-   password：该用户登入密码，密码可以为空

### 修改密码

修改用户就是将创建用户的create改为alter，修改用户可以修改host，passwd等参数

```
alter user "username"@'host' identified by 'passwd'
```

### 删除用户

```mysql
drop user 'username'@'host'
```

### 修改用户名

```mysql
rename user 'old_username'@'host' to 'new_username'@'host';
```

### 授予权限

mysql权限管理机制，可以给不同的用户不同的权限

```mysql
grant privileges on dbname.tablename to 'username'@'host'
```

-   privileges,用户操作的权限，包括select，insert，update等，如果要授予全部的权限则使用all，默认创建的用户除了登录没有其他权限
-   dbname，数据库名称
-   tablename，表名称，如果要授予该用户数据库所有表的权限，则用*表示

### 撤销权限

和授予权限相对应

```mysql
revoke privilege on dbname.tablename from 'username'@'host'
```

## 刷新权限

```
flush privileges;
```



## 角色管理

角色管理就相当于用户组

基本命令如下

-   CREATE ROLE 角色创建

-   DROP ROLE 角色删除
-   GRANT 为用户和角色分配权限
-   REVOKE 为用户和角色撤销权限
-   SHOW GRANTS 显示用户和角色的权限
-   SET DEFAULT ROLE 指定哪些帐户角色默认处于活动状态
-   SET ROLE 更改当前会话中的活动角色
-   CURRENT_ROLE() 显示当前会话中的活动角色

### 创建角色

```mysql
create role 'role1','role2';
```



## 远程登入

默认情况下，mysql只允许本地登入，如果要开启远程连接，则需要修改/etc/mysql/my.conf文件

```vim
找到 bind-address = 127.0.0.1
改为 bind-address = 0.0.0.0
```

**关于远程连接到mysql操作数据库时反应慢的问题**

当远程访问mysql时, mysql会解析域名, 所以会导致访问速度很慢, 会有2,3秒延时！

修改mysql安装目录下的my.cnf，加上下面这个配置可解决此问题。

```tex
[mysqld]
skip-name-resolve
```



## 数据库迁移



## 相关命令

相关命令不做详解

**查看表结构**

```mysql
show create table 表名称
```

**查看表结构**

```mysql
desc 表名称
```



## GPT

### mysql yum仓库是什么？

>   MySQL YUM仓库是一个由MySQL官方维护的在线软件仓库，专门用于通过YUM（Yellowdog Updater, Modified）包管理器安装和管理MySQL软件。YUM是一种在基于RPM（Red Hat Package Manager）包管理的Linux发行版（如Red Hat、CentOS和Fedora）中常用的工具，可以自动解决包依赖关系，并使安装和升级软件变得更加方便。
>
>   通过使用MySQL YUM仓库，你可以轻松地安装、更新和管理MySQL服务器和客户端的各种版本和组件，而无需手动下载和安装RPM包。以下是一些使用MySQL YUM仓库的主要步骤和好处：
>
>   ### 使用MySQL YUM仓库的步骤
>
>   1.  **添加MySQL YUM仓库**：
>
>       -   首先，你需要下载并安装MySQL YUM仓库的RPM包。这通常可以通过以下命令完成：
>
>           ```
>           bash
>           复制代码
>           sudo rpm -Uvh https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
>           ```
>
>           注意：链接和包名可能根据MySQL版本和Linux发行版的不同而变化。请从MySQL官网获取最新的链接。
>
>   2.  **查看可用的MySQL版本和组件**：
>
>       -   安装YUM仓库后，你可以查看仓库中可用的MySQL版本和组件：
>
>           ```
>           bash
>           复制代码
>           yum repolist all | grep mysql
>           ```
>
>   3.  **选择并启用你需要的MySQL版本**：
>
>       -   MySQL YUM仓库包含多个版本的MySQL，你可以通过启用或禁用特定的仓库来选择要安装的版本。例如，启用MySQL 8.0社区版本：
>
>           ```
>           bash复制代码sudo yum-config-manager --enable mysql80-community
>           sudo yum-config-manager --disable mysql57-community
>           ```
>
>   4.  **安装MySQL服务器**：
>
>       -   使用以下命令来安装MySQL服务器：
>
>           ```
>           bash
>           复制代码
>           sudo yum install mysql-community-server
>           ```
>
>   5.  **启动并配置MySQL服务器**：
>
>       -   安装完成后，你可以启动MySQL服务器并进行初始配置：
>
>           ```
>           bash复制代码sudo systemctl start mysqld
>           sudo systemctl enable mysqld
>           ```
>
>       -   获取临时root密码并进行安全设置：
>
>           ```
>           bash复制代码sudo grep 'temporary password' /var/log/mysqld.log
>           sudo mysql_secure_installation
>           ```
>
>   ### 使用MySQL YUM仓库的好处
>
>   -   **简化安装和升级**：YUM仓库可以自动解决依赖关系，简化了MySQL的安装和升级过程。
>   -   **获得最新更新和安全补丁**：通过YUM仓库，你可以方便地获取MySQL的最新更新和安全补丁，确保你的数据库系统保持最新和安全。
>   -   **多版本管理**：MySQL YUM仓库支持多个MySQL版本，你可以根据需要选择和切换不同版本的MySQL。
>   -   **官方支持**：MySQL YUM仓库由MySQL官方维护，提供了可靠的支持和更新。
>
>   总之，使用MySQL YUM仓库可以大大简化MySQL在Linux系统上的安装和维护工作，提高管理效率和系统安全性。