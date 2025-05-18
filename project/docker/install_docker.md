# Linux安装docker

简而言之，Docker 是一个可供开发者通过**容器**(container)来构建，运行和共享应用(application)的平台。用容器来部署应用被称为**集装箱化**(containerization)

## 安装命令

```shell
sudo apt-get install docker.io
```

> docker.io是是**Ubuntu官方维护的docker版本**，存在于Ubuntu的官方库中，使用sudo apt install docker.io 命令可以方便简洁地获取

## 启动docker

docker默认会被systemctl管理，所以可以通过以下命令启动docker

```shell
sudo systemctl start docker
```

自启动

```shell
sudo systemctl enabel docker
```

## 关于非root用户使用docker报错的问题

docker默认只有root用户和docker的用户组才能使用docker，在启动docker时，docker就默认生成了一个docker用户组

```shell
xinghai@matebook:~$ cat /etc/group
root:x:0:
daemon:x:1:
...............................
...................
docker:x:120:
xinghai@matebook:~$
```

解决报错的办法就是，将需要使用docker的用户`添加到docker用户组`中

```shell
sudo usermod -aG docker <you_username>
```

- <you_username> 填写需要使用docker的用户名

**示例**

> 比如我的用户是xinghai，就输入以下命令，然后输入明码就成功了
>
> ```shell
> xinghai@matebook:~$ sudo usermod -aG docker xinghai
> [sudo] password for xinghai:
> xinghai@matebook:~$
> ```
>
> 设置好组信息后，需要更新一下shell的组信息
>
> ```shell
> xinghai@matebook:~$ newgrp docker docker i
> ```
>
> 现在使用一下docker
>
> ```shell
> xinghai@matebook:~$ docker images
> REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
> xinghai@matebook:~$
> ```
>
> 成功

## 关于国内无法拉取镜像的问题

现在国内大部分镜像源已经关闭无法使用了，但还是保留了几个

```
docker.1ms.run
```

毫秒镜像，每个月免费10个G

**使用方法**

> 例如拉取mysql镜像
>
> ```
> docker pull docker.1ms.run/mysql
> ```
>
> 这样就可以了
