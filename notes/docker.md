## 前言

在计算机高速发展的今天，在一台服务器上运行一千个docker容器，已经成为现实

如果说主机时代比拼的是单个主机的物理性能，那么在云计算时代，更看重的是凭借虚拟技术构建的集群处理能力

### 什么是容器？

容器是一种虚拟化技术，用于将应用程序及其所有依赖项打包在一起，以便在不同的计算环境中进行移植和运行。容器提供了一种隔离的运行环境，使不同应用程序能够在独立的文件系统、网络和进程空间等独立运行环境中运行，提升了安全性和稳定性。容器技术的出现，使得应用程序的开发、测试、部署和管理变得更加便捷和高效。

### **容器的优势是什么？**

-   可移植性

    容器已经成为应用分发和交付的标准技术，将应用与底层运行环境进行解耦，使得应用程序可以在不同的计算环境中快速移植和运行。

-   高效性

    相比于传统的虚拟机技术，容器更加轻量级，启动和停止速度更快，占用的资源更少。容器共享操作系统和硬件资源，提高了资源利用率，降低了运行成本。

-   环境隔离

    容器提供了一种隔离的运行环境，每个容器都有自己的文件系统、网络和进程空间，保证了应用程序之间的相互隔离。这样可以提高应用程序的安全性和稳定性，避免了不同应用程序之间的冲突和干扰。

-   可伸缩性

    容器可以根据需求进行水平和垂直扩展，快速实现应用程序的弹性伸缩。通过容器编排工具，可以自动管理和调度容器的部署和扩展，提高了应用程序的可伸缩性和可靠性。

### **容器有哪些实际应用？**

容器在各种应用场景中有着广泛的应用，以下是其中几个主要应用场景：

-   应用程序开发和测试

    容器提供了一个一致的运行环境，使得开发人员可以在开发和测试阶段快速构建和部署应用程序。容器可以将开发环境和生产环境保持一致，提高了开发效率和质量。

-   微服务架构

    微服务架构将应用程序拆分为多个小型的、独立部署的服务。容器可以为每个服务提供一个独立的运行环境，使得微服务之间互相隔离，提高了整体系统的可维护性和可伸缩性。

-   持续集成和持续部署

    容器可以与持续集成和持续部署工具集成，实现自动化的构建、测试和部署。容器可以快速启动和停止，提供了快速迭代和发布的能力，加快了软件交付的速度。

### **容器有哪些类型和技术？**

在容器技术领域，主要类型和技术包括以下几种：

-   containerd:

    containerd 是一个行业标准的容器运行时，用来管理整个容器生命周期，包括容器的创建、执行、暂停、恢复和销毁。

-   Docker

    Docker 是最流行的容器化平台，使用 Docker 镜像来创建容器，提供了一个全面的工具集来构建、运行和管理容器。

-   Kubernetes

    Kubernetes 是一个开源的容器编排系统，用于自动化部署、扩展和管理容器化应用程序。虽然它本身不是容器运行时，但它管理着容器的生命周期。Kubernetes 已经是事实容器编排标准，在企业级落地容器生产环境的唯一优选。

上述提到的一些技术是目前容器生态系统中最主要的组成部分。还有一些其他的容器技术和工具如CRI-O、Podman、LXC/LXD、rkt (Rocket)、Buildah、Skopeo 等，它们在构建和管理容器镜像方面有特定的用途。这个领域还在不断发展，随着新技术的出现和旧技术的淘汰，容器技术的类型和范围可能会有所变化。

### **容器是如何工作的？**

容器技术基于操作系统级的虚拟化技术，利用Linux内核的命名空间和控制组等特性，实现了容器的隔离和资源管理。容器使用了一种称为容器镜像的打包格式，包含了应用程序及其依赖项，以及运行时所需的文件系统、网络和进程空间等。容器镜像可以通过容器运行时创建和启动，形成一个独立的运行环境。

### **容器和虚拟机有什么区别？**

容器和传统的虚拟机技术有所不同。传统的虚拟机技术是通过在物理服务器上运行一个完整的操作系统实例来实现虚拟化，每个虚拟机都有自己的内核和操作系统。而容器是在宿主机的操作系统上运行，共享宿主机的内核和操作系统，每个容器只包含应用程序及其依赖项。

相比于传统的虚拟机技术，容器具有更快的启动和停止速度，更小的资源占用，更高的可伸缩性和更好的性能。容器还提供了更好的环境隔离和更高的应用程序密度，可以在相同的硬件资源上运行更多的应用程序实例。

容器和虚拟机之间的主要区别在于虚拟化层级、资源利用效率、启动速度和性能以及隔离性。

| **对比项**   | **虚拟机**                   | **容器**         |
| ------------ | ---------------------------- | ---------------- |
| 虚拟化层级   | 硬件级别                     | 操作系统级别     |
| 资源利用效率 | 低，占用大量的内存和存储资源 | 高，占用资源较少 |
| 启动速度     | 慢，几十秒到几分钟           | 快，几秒到几十秒 |
| 隔离性       | 严格隔离                     | 轻量级隔离       |

相比于传统的虚拟机技术，容器具有更快的启动和停止速度，更少的资源占用，更高的可伸缩性和更好的性能。容器还提供了更好的环境隔离和更高的应用程序密度，可以在相同的硬件资源上运行更多的应用程序实例。

### Linux容器

在Linux系统当中集成一个linux容器（Linux containers，LXC）技术，`容器有效的将单个操作系统管理的资源划分到孤立的组当中，以更好的在孤立的组之间平衡有冲突的资源使用与需求`

在LXC的基础上，DocKer进一步的优化了容器的使用体验，让用户无需关注底层操作，更加简单明了地管理和使用容器

简单地讲，Docker容器理解为一种轻量级别的沙盒，每个容器内运行着一个应用，不同的容器相互隔离，`容器之间可以通过网络互相通信`

## 核心概念和安装配置

核心三大概念

-   镜像（Image）
-   容器（Container）
-   仓库（RePository）

### 镜像

Docker镜像类似于虚拟机的镜像，可以将它理解为一个只可读的模板，例如，一个镜像包含一个基本的操作系统环境，里面安装了Apache应用程序，或者用户需要的其他软件，可以把它称为一个Apache镜像

`镜像是创建Docker的基础`

### 容器

Docker容器类似于一个轻量级别的沙箱，Docker利用容器来运行和隔离应用

`容器是从镜像创建的应用运行的实例`,这些容器都是彼此互相隔离的，互不可见的

可以把容器看作是一个建议版本的Linux系统环境，保活root用户权限，进程空间，用户空间和网络空间，以及运行在其中的应用程序打包而成的盒子

>   镜像只是可读的，容器从镜像启动的时候，会在镜像的最上层创建一个可写层

### 仓库

Docker仓库类似于代码仓库，是Docker集中存放镜像文件的场所

**仓库注册服务器**：仓库注册服务器是用来存放仓库的地方，一个仓库可以有多个版本的镜像，一个仓库注册服务器有多个仓库，常见的仓库注册服务器有阿里云、腾讯云以及最大的官方注册仓库Docker Hub

>   可以看出，Docker利用仓库管理镜像的设计理念与Git代码仓库的概念非常类似，实际上，Docker设计上借鉴了Git的很多优秀的思想

## 安装Docker引擎

Docker引擎是Docker容器的核心组件，可以在主流的操作系统当中使用

这里再centerOs当中安装docker，遇到了很多问题

-   我在官网上面寻找安装包，windows版本的倒是容易安装，但是前面提到过，docker是基于linux系统的容器改进的，所以windows本身是不支持的，之所以能在windows安装docker是因为，安装docker的时候自动安装了虚拟机，在windows安装是容易，但是不会用，难以理解整个操作逻辑，所以暂时搁置
-   我继续在官网上面寻找Linux版本的安装方法，在我苦苦寻找几次后果然找到了，不仅仅有Ubuntu版本的，还有CentOS版本的教程，几乎是手把手教，但是我不会英语，看不懂，结果放弃了，我又回到了书本上
-   开始我为什么不按照书本上面的做呢，这里简单的解释一下安装的流程，就是CentOS是用yum命令安装程序的，但是yum命令查找应用的时候是在它的yum仓库里面查找的，就是仓库里面有的应用才可以被搜索到并且下载，很显然，既然我提到了这个yum仓库那就意味着yum仓库里面根本没有docker，那么就需要在yum仓库里面添加docekr的仓库，按照书本上的方法，添加仓库首先需要`yum-config-manager`工具，这个工具需要下载`yum-utils`才有，有了`yum-config-manager`工具就可以把仓库添加到yum当中，所谓的仓库实际上就是一个以repo为后缀的文件，当然，docker的仓库还得在docker官网上面寻找，所以就觉得太麻烦，然后想在网上找简单一点的教程
-   很显然，网上找的就更加看不懂了，那么就老老实实的看书吧，当我用yum-config-manager --add-repo `http://download.docker.com/linux/centos/docker-ce.repo`,发现网络错误，当我用浏览器打开这个链接的时候就发现无法打开，我寻思着链接没打错啊，于是乎我用了点魔法，然后发现居然可以打开了，这时候我才恍然大悟，原来这玩意是被墙了啊，我又运行了这个命令，发现还是网络错误，这时候才知道，主机的魔法不能影响到虚拟机，也就是windows开的VPN在虚拟机就没用了，反正我在windows都能访问了，我直接windows下载传到centos，然后用`yum-config-manager --add-repo `添加本地的不就好了，就在我为添加成功仓库而窃窃自喜时，发现用`yum install docker-ce`命令死活下载不了,我恍然大悟，连仓库都被墙了我还指望国家能对安装包网开一面？按照书本的方法，失败
-   于是乎我在网上找哇找，找哇找，终于给我找到了，[下载docker教程](https://blog.csdn.net/u011397981/article/details/130616038)，不管怎么说，这个教程都是救大命的

>   开机自启动docker
>
>   ```shell
>   systemctl enable docker
>   ```
>
>   启动docker
>
>   ```shell
>   systemctl start docker
>   ```
>
>   查看dokcer版本信息
>
>   ```shell
>   [root@center yum.repos.d]# docker version
>   Client: Docker Engine - Community
>   Version:           26.1.4
>   API version:       1.45
>   Go version:        go1.21.11
>   Git commit:        5650f9b
>   Built:             Wed Jun  5 11:32:04 2024
>   OS/Arch:           linux/amd64
>   Context:           default
>   
>   Server: Docker Engine - Community
>   Engine:
>    Version:          26.1.4
>    API version:      1.45 (minimum version 1.24)
>    Go version:       go1.21.11
>    Git commit:       de5c9cf
>    Built:            Wed Jun  5 11:31:02 2024
>    OS/Arch:          linux/amd64
>    Experimental:     false
>   containerd:
>    Version:          1.6.33
>    GitCommit:        d2d58213f83a351ca8f528a95fbd145f5654e957
>   runc:
>    Version:          1.1.12
>    GitCommit:        v1.1.12-0-g51d5e94
>   docker-init:
>    Version:          0.19.0
>    GitCommit:        de40ad0
>   ```
>
>   当然，最好不要用root用户

在这之前需要配置一下docker的镜像，前面提到过docker被封掉了，所以要么使用加速器，要么使用加速镜像，目前Linux无GUI版本的加速器没有找到，所以就不考虑了，镜像加速我想到了阿里云，也在其官网上找到了加速的方法具体如下

在官网中找到[教程](https://help.aliyun.com/zh/acr/user-guide/accelerate-the-pulls-of-docker-official-images)，根据其教程就可以找到配置的方法

可以通过修改daemon配置文件`/etc/docker/daemon.json`

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://5djz3whb.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```



## 使用Docker镜像

镜像是三大核心概念当中最重要的

### **获取镜像**

```shell
docekr pull <image>[:TAG]
```

-   image 代表的是镜像的名称
-   TAG是镜像的标签，对于镜像来说，如果不显式的指定TAG则会选择lates标签，这会下载最新版本的镜像，一般来说，latest标签代表的是镜像内容会随着新版本变化而变化，就是内容是不稳定的，所以生产环境当中最好不要使用latest标签

pull支持的选项

-   -a，--all-tags=true|false	是否获取仓库中的所有镜像，默认为否
-   --disable-content-trust	取消内容校验，默认为真
-   --registry-mirror=proxy_URL 指定代理镜像服务器

**示例**

```shell
[xinghai@center docker]$ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
7b1a6ab2e44d: Pull complete
Digest: sha256:626ffe58f6e7566e00254b638eb7e0f3b11d4da9675088f4781a50ae288f3322
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

利用镜像创建一个容器，在其中运行bash应用

```bash
[xinghai@center docker]$ docker run -it ubuntu bash
root@d31b10e34836:/# echo "hello word"
hello word
root@d31b10e34836:/# exit
exit
[xinghai@center docker]$
```

### **查看镜像信息**

命令

```bash
docker images 或者 docker image ls
```

这个命令可以列出本地主机上面已有的镜像的基本信息

```bash
[xinghai@center docker]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    ba6acccedd29   2 years ago   72.8MB
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
[xinghai@center docker]$ docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    ba6acccedd29   2 years ago   72.8MB
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
```

-   repository	来自于哪个仓库，比如ubuntu表示Ubuntu系列的基础镜像
-   tag	标签，表示不同版本的标签，标签只是一个标记而已，不能标记镜像的内容
-   image id	镜像的id，镜像的唯一标识，如果两个镜像的id相同，说明他们实际上是一个镜像，只是具有不同的标签名称而已
-   created	创建的时间，说明镜像的最后更新时间
-   size 	镜像的大小，这里镜像的大小只是表示了该镜像的逻辑的体积大小，实际上由于相同的镜像层本地只会存一份，物理上占用的存储空间会小于各逻辑镜像的体积之和

images**子命令选项**

-   -a,--all=True|False 列出所有镜像，包括临时文件，默认为否
-   --digests=true|false列出镜像的数字摘要值
-   man docker-images 查看命令选项

### 添加镜像标签

语法

```shell
docker tag <images> <images>
```

docker tag添加标签实际上起到了添加链接的作用，本质上还是指向同一个镜像

**示例**

```shell
[xinghai@center docker]$ docker tag 5a214d77f5d7 myubuntu:444
[xinghai@center docker]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    ba6acccedd29   2 years ago   72.8MB
myubuntu     444       5a214d77f5d7   2 years ago   63.1MB
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
[xinghai@center docker]$
```

### 查看镜像具体信息

```shell
docker inspece <image>
```

**示例**

```shell
[xinghai@center docker]$ docker inspect 5a214d77f5d7
[
    {
        "Id": "sha256:5a214d77f5d747e6ed81632310baa6190301feeb875cf6bf9da560108fa09972",
        "RepoTags": [
            "myubuntu:444",
            "ubuntu:18.04"
        ],
        "RepoDigests": [
            "ubuntu@sha256:0fedbd5bd9fb72089c7bbca476949e10593cebed9b1fb9edf5b79dbbacddd7d6"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2021-10-01T02:23:24.179667784Z",
        "DockerVersion": "20.10.7",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "bash"
            ],
            "Image": "sha256:de5a48194cb6a383c018b7c57fa642457688605c5d6d4941db88fecabd225a55",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 63136384,
        "GraphDriver": {
            "Data": {
                "MergedDir": "/var/lib/docker/overlay2/b61c8235758ab3adc83477d9ae4b6ca6c9e481007443e536b60afd707c2682fd/merged",
                "UpperDir": "/var/lib/docker/overlay2/b61c8235758ab3adc83477d9ae4b6ca6c9e481007443e536b60afd707c2682fd/diff",
                "WorkDir": "/var/lib/docker/overlay2/b61c8235758ab3adc83477d9ae4b6ca6c9e481007443e536b60afd707c2682fd/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:824bf068fd3dc3ad967022f187d85250eb052f61fe158486b2df4e002f6f984e"
            ]
        },
        "Metadata": {
            "LastTagTime": "2024-07-28T13:54:55.762848439+08:00"
        }
    }
]
[xinghai@center docker]$
```

inspect命令可以获取一个镜像的详细信息，包括制作作者，适应架构，各层的数字信息摘要等

上面返回的是一个json格式的信息，如果我们只需要其中一项内容时，可以用-f指定

**语法**

```shell
 docker inspect -f {{".Os"}} <image>
```

**示例**

```shell
[xinghai@center docker]$ docker inspect -f {{".Os"}} ubuntu:18.04
linux
[xinghai@center docker]$
```

### 查看镜像历史

镜像是由多个层组成的，使用history命令就可以知道各层的创建信息

```shell
[xinghai@center docker]$ docker history ubuntu
IMAGE          CREATED       CREATED BY                                       SIZE      COMMENT
ba6acccedd29   2 years ago   /bin/sh -c #(nop)  CMD ["bash"]                  0B
<missing>      2 years ago   /bin/sh -c #(nop) ADD file:5d68d27cc15a80653…   72.8MB
```

由于信息太长被截断了，可以使用前面提到的--on-trunc选项来输出完整的信息

```shell
[xinghai@center docker]$ docker history --no-trunc=true ubuntu
IMAGE                                                                     CREATED       CREATED BY
                                                                      SIZE      COMMENT
sha256:ba6acccedd2923aee4c2acc6a23780b14ed4b8a5fa4e14e252a23b846df9b6c1   2 years ago   /bin/sh -c #(nop)  CMD ["bash"]                                                                     0B
<missing>                                                                 2 years ago   /bin/sh -c #(nop) ADD file:5d68d27cc15a80653c93d3a0b262a28112d47a46326ff5fc2dfbf7fa3b9a0ce8 in /    72.8MB
[xinghai@center docker]$
```

### 搜寻镜像

`docker search`命令可以搜索仓库当中的镜像，语法为

```shell
docker search [option] keyword
```

选项包括

-   -f, --filter 过滤输出内容
-   --format string 格式化输出内容
-   --limit int 限制输出结果个数
-   --no-trunc不截断输出结果

**示例**

搜索stars大于100的关键字是hadoop的镜像

```shell
[xinghai@center docker]$ docker search --filter=stars=100 hadoop
NAME                       DESCRIPTION                        STARS     OFFICIAL
apache/hadoop              Apache Hadoop convenience builds   100
sequenceiq/hadoop-docker   An easy way to try Hadoop          672
[xinghai@center docker]$
```

### 删除和清理镜像

使用`docker rmi `或者 `docker image rm`命令可以删除镜像,语法为,image可以是标签或者ID

```
docker rmi image [image....]
```

-   如果选择的是ID，那么就删除这个ID所有的不同标签的镜像
-   如果选择的是标签，那么就只会删除这一个标签

支持的选项包括

-   -f,-force 强制删除，即使有容器依赖他
-   -no-prune 不要清理未代标签的父镜像

当这个镜像创建过容器时，该镜像是不能被直接删除的

>   使用`docker ps -a`k可以看到本机上所有的容器

如果想要强制删除镜像可以使用-f参数，但并不推荐，推荐的方法是，用`docker ps -a`找到该镜像创建的容器，然后使用`docekr rm <container>`删除容器，最后使用`docekr rmi <image>`删除镜像

### 清理镜像

使用docker一段时间后，系统中可能会遗留一些临时的镜像文件，以及一些没有被使用的镜像，可以通过`docker image prune`命令来进行清理

示例

```shell
[xinghai@center docker]$ docker image prune
WARNING! This will remove all dangling images.
Are you sure you want to continue? [y/N] Y
Total reclaimed space: 0B
[xinghai@center docker]$
```

支持选项包括

-   -a 删除所有无用的镜像，不光是临时镜像
-   -filter 之清理符合给定条件的镜像
-   -f force强制删除镜像，而不进行确认提示

### 创建镜像

创建镜像有三种方法

-   基于已有镜像的容器创建
-   基于本地模板导入
-   基于Dockerfile创建

主要的命令是commit,import和build子命令

#### 基于已有的容器创建

命令

```shell
docker [container] commit [options] container [repository[:tag]]
```

options包括

-   -a,--autor=''作者信息
-   -c,--change=[]提交时候执行Dockerfile指令，包括cmd|entrypoint|env|expose|label|onbulld|user|volume|workdir等
-   -m,--message=‘’提交信息
-   -p，--pause=true:提交时暂停容器运行

**示例**

```bash
[xinghai@center docker]$ docker run -it ubuntu:18.04
root@07282d149b2e:/# touch test
root@07282d149b2e:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  test  tmp  usr  var
root@07282d149b2e:/# exit
exit
[xinghai@center docker]$ #此时容器的id为07282d149b2e
[xinghai@center docker]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED              STATUS                          PORTS     NAMES
07282d149b2e   ubuntu:18.04   "bash"    About a minute ago   Exited (0) About a minute ago             stupefied_gagarin
[xinghai@center docker]$ docker commit -m "Added a new file" -a "Docker Newbee" 07282d149b2e test:0.1
sha256:39f34b15173312fa5f4b2f74d40a5765e5cc1408ec059a2c586e93c5c1934f1f
[xinghai@center docker]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
test         0.1       39f34b151733   20 seconds ago   63.1MB
ubuntu       latest    ba6acccedd29   2 years ago      72.8MB
ubuntu       18.04     5a214d77f5d7   2 years ago      63.1MB
[xinghai@center docker]$
```

#### 基于本地模板导入

命令

```
docker [image] import [options] file|URL|-[repository[:tag]]
```

**示例**

首先需要在[OpenVZ](https://wiki.openvz.org/Download/template/precreated)下载系统模板

```bash
[xinghai@center ~]$ ls
ubuntu-16.10-x86_64.tar.gz
[xinghai@center ~]$ docker import ubuntu-16.10-x86_64.tar.gz mya:a
sha256:47a84edfa06a32d7e3ddefd8fc1e75a6135bd646b066e05b87a48f2ef3c7b0cf
[xinghai@center ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
mya          a         47a84edfa06a   24 seconds ago   503MB
ubuntu       latest    ba6acccedd29   2 years ago      72.8MB
ubuntu       18.04     5a214d77f5d7   2 years ago      63.1MB
[xinghai@center ~]$ docker run -it mya:a bash
root@b3133fa92a6f:/# ls
bin  boot  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@b3133fa92a6f:/# exit
exit
[xinghai@center ~]$
```

#### 基于dockerFile创建

利用dockerfile创建是最常见的方式，dockerfile是一个文本文件，利用给定的指令描述基于某个父镜像创建新镜像的过程

**流程**

-   在工作目录下创建名为Dockerfile的文件
-   在dockerfile当中编写指令
-   执行`docker build -t [imagesname[:tag]]`

**示例**

```shell
[xinghai@center ~]$ echo "from debian:stretch-slim" >> Dockerfile
[xinghai@center ~]$ docker build -t debian:3 .
[+] Building 20.6s (5/5) FINISHED                                                                      docker:default
 => [internal] load build definition from Dockerfile                                                             0.0s
 => => transferring dockerfile: 121B                                                                             0.0s
 => [internal] load metadata for docker.io/library/debian:stretch-slim                                          20.5s
 => [internal] load .dockerignore                                                                                0.0s
 => => transferring context: 2B                                                                                  0.0s
 => CACHED [1/1] FROM docker.io/library/debian:stretch-slim@sha256:5913f0038562c1964c62fc1a9fcfff3c7bb340e2f5db  0.0s
 => exporting to image                                                                                           0.0s
 => => exporting layers                                                                                          0.0s
 => => writing image sha256:e5a142062025cb0acb134e0c3b3368f745aff19ff35506b1038ccf3ae966968f                     0.0s
 => => naming to docker.io/library/debian:3                                                                      0.0s
[xinghai@center ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
debian       3         e5a142062025   2 years ago   55.3MB
ubuntu       latest    ba6acccedd29   2 years ago   72.8MB
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
[xinghai@center ~]$
```

### 存出镜像

如果要将镜像导出到本地，可以使用`docker save`命令，支持`-o,-output string`参数,到处镜像到本地文件当当中

**示例**

```shell
[xinghai@center ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
debian       3         e5a142062025   2 years ago   55.3MB
ubuntu       latest    ba6acccedd29   2 years ago   72.8MB
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
[xinghai@center ~]$ docker save -o debian-aaa.tar debian:3
[xinghai@center ~]$ ls
debian-aaa.tar  Dockerfile  ubuntu-16.10-x86_64.tar.gz
[xinghai@center ~]$
```

之后，用户就可以复制debain-aaa.tar给其他人

### 载入镜像

可以使用docker load将导出的tar文件导入到本地镜像库当中，支持 `-i , -input string`选项，从指定的文件中读入镜像内容

**示例**

```shell
[xinghai@center ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    ba6acccedd29   2 years ago   72.8MB
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
[xinghai@center ~]$ ls
debian-aaa.tar  Dockerfile  ubuntu-16.10-x86_64.tar.gz
[xinghai@center ~]$ docker load -i debian-aaa.tar
Loaded image: debian:3
[xinghai@center ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
debian       3         e5a142062025   2 years ago   55.3MB
ubuntu       latest    ba6acccedd29   2 years ago   72.8MB
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
[xinghai@center ~]$
```

这将导入镜像以及相关的元数据，包括标签等，导入成功后就可以正常使用镜像和创建容器了

### 上传镜像

上传镜像的意思就是将我自己制作好的镜像，然后上传到注册服务器的仓库当中，这样就可以使用`docker pull <image>`命令拉取镜像了

但是在这之前，还是要考虑到docker被封这件事，也就是说，docker Hub是用不了的，那么就只能用国内的镜像仓库代替了，这里用的还是阿里云,[具体教程](https://help.aliyun.com/zh/acr/user-guide/create-a-container-registry-personal-edition-instance)

**示例**

>   **登入账号**
>
>   ```shell
>   docker login --username=aliyun3480602784 registry.cn-guangzhou.aliyuncs.com
>   ```
>
>   **上传镜像**
>
>   ```shell
>   docker push registry.cn-guangzhou.aliyuncs.com/xinghai2524/test:[镜像版本号]
>   ```

## 操作Docekr容器

**容器**是docker最重要的一个核心概念，简单来说，容器是镜像的一个运行实例，所不同的是，镜像是一个静态的只读的文件，而容器带有运行时需要的可写文件层，同时，容器中的应用进程处于运行状态

### 创建容器

新建容器就是将镜像创建成一个可以运行的实例

**命令**

`docker create`

**示例**

```shell
[root@center ~]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
test         0.1       e5a142062025   2 years ago   55.3MB
[root@center ~]# docker create -it test:0.1
6b34c5e225f06bd983b840cfa1e245cbcb2a38f625760ec9a0ef94ed7e20faea
[root@center ~]# docker ps -a
CONTAINER ID   IMAGE      COMMAND   CREATED          STATUS    PORTS     NAMES
6b34c5e225f0   test:0.1   "bash"    16 seconds ago   Created             laughing_noyce
[root@center ~]#
```

**支持的选项**

支持选项有很多，这里只是举几个典型，具体看书，找教程

-   -i,--interactive=true|false	保持标准输入打开，默认是false
-   -t,--tty=true|false	是否分配一个伪终端，默认是false
-   -w,--workdir=""容器内部默认工作目录

### 启动容器

默认创建的容器都是处于停止状态，需要启动容器

**命令**

```shell
docker start [container]
```

**示例**

拿上面的test:0.1举例

```shell
[root@center ~]# docker ps -a
CONTAINER ID   IMAGE      COMMAND   CREATED          STATUS    PORTS     NAMES
2b4b654eec64   test:0.1   "bash"    10 seconds ago   Created             gallant_perlman
[root@center ~]# docker start 2b4b654eec64
2b4b654eec64
[root@center ~]# docker ps -a
CONTAINER ID   IMAGE      COMMAND   CREATED          STATUS         PORTS     NAMES
2b4b654eec64   test:0.1   "bash"    24 seconds ago   Up 2 seconds             gallant_perlman
```

### 新建并启动容器

除了创建容器后通过start命令来启动容，还可以直接新建并启动容器

**命令**

```shell
docker run container
```

该命令等价于`docker create`,`docker start`的组合

**示例**

输出一个hello word然后关闭容器

```shell
[root@center ~]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
test         0.1       e5a142062025   2 years ago   55.3MB
[root@center ~]# docker run test:0.1 /bin/echo "hello word"
hello word
[root@center ~]# docker ps -a
CONTAINER ID   IMAGE      COMMAND                   CREATED         STATUS                     PORTS     NAMES
37f668afd721   test:0.1   "/bin/echo 'hello wo…"   9 seconds ago   Exited (0) 8 seconds ago             wonderful_solomon
```

当利用docker来创建并启动容器的时候，实际上，docker在后台执行的操作包括：

-   检查本地是否存在该镜像，如果不存在则从公有仓库当中下载，
-   利用这个镜像创建一个容器，并启动该容器
-   分配一个文件系统给容器，并在只读的镜像层外面挂载一个可读写层
-   从宿主主机配置的网络接口当中桥接一个虚拟接口到容器当中去
-   从网桥地址池配置一个ip给容器
-   执行用户指定的应用程序
-   执行完毕后停止容器

例如，利用一个本地没有的镜像创建容器，并允许bash程序

```shell
[root@center ~]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
test         0.1       e5a142062025   2 years ago   55.3MB
[root@center ~]# docker run -it ubuntu:18.04 /bin/bash
Unable to find image 'ubuntu:18.04' locally
18.04: Pulling from library/ubuntu
284055322776: Pull complete
Digest: sha256:0fedbd5bd9fb72089c7bbca476949e10593cebed9b1fb9edf5b79dbbacddd7d6
Status: Downloaded newer image for ubuntu:18.04
root@500d13271d09:/# echo "hello word"
hello word
root@500d13271d09:/# exit
exit
[root@center ~]# docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS                     PORTS     NAMES
500d13271d09   ubuntu:18.04   "/bin/bash"   28 seconds ago   Exited (0) 5 seconds ago             funny_wiles
[root@center ~]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
test         0.1       e5a142062025   2 years ago   55.3MB
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
```

从上面的示例可知，本地并没有ubuntu:18.04,所以从公有仓库当中下载了，下载之后创建容器，然后运行bash这个程序，但是这个程序只有用户输入exit退出的时候这个程序才算结束，当程序结束的时候，容器也就关闭了

**关于` -it`选项的问题**

>   ### 容器的基本概念
>
>   Docker 容器是一个独立的运行环境，可以包含应用程序及其所有依赖项。容器通常用于运行应用程序的实例，无论是短暂的任务还是长期运行的服务。
>
>   ### 交互式与非交互式操作
>
>   在使用容器时，有时需要与容器进行交互（例如通过命令行输入命令），有时则不需要。例如：
>
>   -   **交互式操作**：你可能需要进入容器内部，手动执行一些命令或进行调试。
>   -   **非交互式操作**：你可能只是启动一个服务，容器运行在后台，不需要任何人工输入。
>
>   ### 设计 `-i` 和 `-t` 的原因
>
>   为了满足不同的操作需求，Docker 提供了不同的选项来控制标准输入和伪终端：
>
>   1.  **保持标准输入打开（`-i`）**：
>       -   当你需要在容器运行期间向其发送输入时，使用这个选项。
>       -   例如，运行一个需要用户输入的脚本，或者通过管道向容器传递数据。
>   2.  **分配伪终端（`-t`）**：
>       -   伪终端提供一个用户友好的终端环境，使得输出格式和交互体验更好。
>       -   例如，运行一个交互式的 shell（如 bash），你希望有命令行编辑和历史记录

### 守护态运行容器

所谓守护态运行容器，说人话就是后台运行，至于输出结果怎么查看，那就要用到另外一个命令了，这里就一并讲了

守护太运行直接加`-d`参数

```shell
docker run -di ubuntu:18.04 /bin/bash  -c "ping www.baidu.com"
```

**示例**

```shell
[xinghai@center ~]$ docker run -di ubuntu:18.04 /bin/echo "ping www.baidu.com"
18820bca829730b313620bcd45df739fb32d90f714d49adc88aecc19d3a97cdb
[xinghai@center ~]$ docker logs 18820bca829730b313620bcd45df739fb32d90f714d49adc88aecc19d3a97cdb
ping www.baidu.com
[xinghai@center ~]$
```

可以看到，后台运行的容器是不会直接输出结果的，而是返回个id，这个是容器的id，而程序在后台运行，运行完成后台自动结束

通过上面可以发现可以通过`docekr logs [id]`的形式获取到容器的返回的内容

关于`docker logs`选项如下

-   -details	打印详细信息
-   -f	follow	持续保持输出
-   -t	显示时间信息
-   -tail strng	输出最近的若干日志
-   -until string	输出某个时间之前的日志

### 停止容器

`docker stop [container]`命令可以用来停止一个正在运行的容器

这个时候可以用`docker container prune`命令清除停止运行的所有容器

`docker restart [container]`可以用来重启容器

可以通过`docker kill`命令强行停止容器

**示例**

```shell
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[xinghai@center ~]$ docker create -it ubuntu:18.04
fbbc31f2299ea6183ea1e3e20438bbf45c95e698079a5d223f407eb9fef6c379
[xinghai@center ~]$ docker start fbbc31f2299ea6183ea1e3e20438bbf45c95e698079a5d223f407eb9fef6c379
fbbc31f2299ea6183ea1e3e20438bbf45c95e698079a5d223f407eb9fef6c379
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS         PORTS     NAMES
fbbc31f2299e   ubuntu:18.04   "bash"    17 seconds ago   Up 3 seconds             eager_cohen
[xinghai@center ~]$ docker kill fbbc31f2299ea6183ea1e3e20438bbf45c95e698079a5d223f407eb9fef6c379
fbbc31f2299ea6183ea1e3e20438bbf45c95e698079a5d223f407eb9fef6c379
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS                       PORTS     NAMES
fbbc31f2299e   ubuntu:18.04   "bash"    30 seconds ago   Exited (137) 5 seconds ago             eager_cohen
[xinghai@center ~]$ docker container prune
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] Y
Deleted Containers:
fbbc31f2299ea6183ea1e3e20438bbf45c95e698079a5d223f407eb9fef6c379

Total reclaimed space: 0B
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### 暂停继续容器

暂停容器执行

```shell
docker pause
```

继续容器执行

```shell
docker unpause
```

示例

```shell
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED         STATUS    PORTS     NAMES
e636051f0e2f   ubuntu:18.04   "bash"    6 seconds ago   Created             awesome_lalande
[xinghai@center ~]$ docker start e636051f0e2f
e636051f0e2f
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS          PORTS     NAMES
e636051f0e2f   ubuntu:18.04   "bash"    27 seconds ago   Up 10 seconds             awesome_lalande
[xinghai@center ~]$ docker pause e636051f0e2f
e636051f0e2f
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS                   PORTS     NAMES
e636051f0e2f   ubuntu:18.04   "bash"    36 seconds ago   Up 19 seconds (Paused)             awesome_lalande
[xinghai@center ~]$ docker unpause e636051f0e2f
e636051f0e2f
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS          PORTS     NAMES
e636051f0e2f   ubuntu:18.04   "bash"    44 seconds ago   Up 27 seconds             awesome_lalande
```

### 进入容器

在使用-d参数的时候，启动容器会进入后台，用户无法查看到容器内的信息，也无法进行操作，这个时候就需要进入容器内部进行操作了

**语法**

`attach命令`

```shell
docker [container] attach [--detach-keys[=[]]] [--no-stdin] [--sig-proxy=[=true]] container
```

三个主要选项

-   --detach-keys	指定退出attach模式的快捷键，默认是ctrl+p+ctrl+q，有时候需要退出attach模式但是不结束终端，并且保持容器运行，就可以用这个方法退出
-   --no-stdin=true|fales	石否关闭标准输入，默认是打开标准输入

如果，同一个容器在多个终端中用attach打开，哪个多个attach进入的伪终端是共享的，就相当于多台机器共享同一个终端

比如

![image-20240730091213397](https://db.xinghai.ink/Typora/17349907242212772.png)

这是两个终端，同时用attach进入同一个容器的情况，可以发现，如果操作其中一个终端，那么另一个终端都是同步的，也就相当于他们在操作同一个终端，那么如果终端堵塞了，那么个堵塞也会同步到所有终端当中，为了解决这个问题，docker提供了一个更加便捷的命令

`exec命令`

```shell
docker exec [-d|--detach] [--detach-keys[=[]]] [-i|interactive] [--privileged] [-t|--tty] [-u|--user=[=USER]] container command [arg...]
```

比较重要的参数有

-   -d ,--detach	在容器中后台执行命令
-   --detach-keys=""	指定容器切换回后台的按键
-   -e, --env=[]	指定环境变量列表
-   -i，--interactive=true	打开标准输入，接收用户输入，默认为false
-   --privileged=true|false	是否给执行命令以高权限，默认为false
-   -t，--tty=true|false	是否分配伪终端，默认为false
-   -u,--user	执行命令的用户名或者id

**示例**

```shell
[xinghai@center ~]$ docker exec -it e636051f0e2f /bin/bash
root@e636051f0e2f:/# ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
root@e636051f0e2f:/# exit
exit
[xinghai@center ~]$
```

每用一个exec执行程序都相当于一个独立进程，用exec执行bash打开终端

简单的理解就是attach命令用来连接容器里面的唯一的终端，exec就是让容器以新的进程执行程序，程序包括bash



>   容器创建的时候，按理来说需要制定默认命令，这个默认命令在容器每一次启动的时候都会执行
>
>   **例如**
>
>   ```shell
>   [xinghai@center ~]$ docker images
>   REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
>   ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
>   [xinghai@center ~]$ docker create -i ubuntu:18.04 echo "hello word"
>   b312107056ad2ee9a36b33266d84da40e320625a3b1761efc3b01008cd0065b0
>   [xinghai@center ~]$ docker ps -a
>   CONTAINER ID   IMAGE          COMMAND               CREATED         STATUS    PORTS     NAMES
>   b312107056ad   ubuntu:18.04   "echo 'hello word'"   4 seconds ago   Created             eloquent_chatterjee
>   [xinghai@center ~]$ docker start b312107056ad && docker logs b312107056ad
>   b312107056ad
>   hello word
>   [xinghai@center ~]$ docker start b312107056ad && docker logs b312107056ad
>   b312107056ad
>   hello word
>   hello word
>   [xinghai@center ~]$ docker start b312107056ad && docker logs b312107056ad
>   b312107056ad
>   hello word
>   hello word
>   hello word
>   [xinghai@center ~]$ docker start b312107056ad && docker logs b312107056ad
>   b312107056ad
>   hello word
>   hello word
>   hello word
>   hello word
>   ```
>
>   这里给定一个默认命令是输出hello word，然后么一次启动容器的时候都会执行一次hello word

如果不指定默认命令，那么默认命令就是启动shell，一般就是`/bin/bash`或者`/bin/sh`

但是bash命令依赖于终端，如果创建容器没有指定-t，那么启动容器后启动bash就会直接停止退出，那么容器也就会退出，所以就会出现创建容器没有指定-t和默认命令时，启动容器，容器会直接停止

### 删除容器

**命令**

```shell
docker rm <container>
```

支持的选项包括

-   -f,--force=false,是否强行终止并删除一个运行中的容器
-   -l，--link=false，删除容器的连接并保留容器
-   -v，--volumes=false删除容器挂载的数据卷

**示例**

```shell
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND               CREATED          STATUS                      PORTS     NAMES
b312107056ad   ubuntu:18.04   "echo 'hello word'"   43 minutes ago   Exited (0) 42 minutes ago             eloquent_chatterjee
[xinghai@center ~]$ docker rm b312107056ad
b312107056ad
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[xinghai@center ~]$
```

### 导出导入容器

某些时候需要将容器从一个系统迁移到另一个系统，此时可以用docker容器的导入和导出功能

导出命令

```shell
dokcer export <container>
```

支持的选项包括

-   -o string,指定导出的tar文件名

**导入命令**

```shell
docker import <container>
```

**示例**

创建一个容器，并导出导入容器

```shell
[xinghai@center ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       18.04     5a214d77f5d7   2 years ago   63.1MB
[xinghai@center ~]$ docker create -it ubuntu:18.04
5ac3e5c42147fcb22b28c37f2a19e19d2815388b34aa4a1bbcf09a656bb5b7f7
[xinghai@center ~]$ docker start 5ac3e5c42147fcb22b28c37f2a19e19d2815388b34aa4a1bbcf09a656bb5b7f7
5ac3e5c42147fcb22b28c37f2a19e19d2815388b34aa4a1bbcf09a656bb5b7f7
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS         PORTS     NAMES
5ac3e5c42147   ubuntu:18.04   "bash"    20 seconds ago   Up 4 seconds             practical_mclean
[xinghai@center ~]$ docker export -o ubuntu 5ac3e5c42147
[xinghai@center ~]$ ls
ubuntu
[xinghai@center ~]$ docker rm -f 5ac3e5c42147 && docker rmi ubuntu:18.04
5ac3e5c42147
Untagged: ubuntu:18.04
Untagged: ubuntu@sha256:0fedbd5bd9fb72089c7bbca476949e10593cebed9b1fb9edf5b79dbbacddd7d6
Deleted: sha256:5a214d77f5d747e6ed81632310baa6190301feeb875cf6bf9da560108fa09972
[xinghai@center ~]$ docker ps -a && docker images
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
[xinghai@center ~]$ docker import ubuntu ubuntu:18.04
sha256:ce57623815a66a5596d7f9629d4f99c8491a82322420240ae08c23ea4dffe519
[xinghai@center ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
ubuntu       18.04     ce57623815a6   4 seconds ago   63.1MB
[xinghai@center ~]$
```

### 查看容器

查看容器和查看镜像命令差不多

```
docker container inspect
```

**示例**

```shell
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED              STATUS    PORTS     NAMES
45e47ce017d7   ce57623815a6   "/bin/bash"   About a minute ago   Created             quirky_jennings
[xinghai@center ~]$ docker container inspect 45e47ce017d7
[
    {
        "Id": "45e47ce017d7fadf57c69eeecd5832445b77ceea93c37328fbfb51216836d467",
        "Created": "2024-07-30T06:22:05.706487985Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "created",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
.......................................................................
```

**查看容器内部进程**

```shell
docker top container
```

示例

```shell
[xinghai@center ~]$ docker top 45e47ce017d7
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                22410               22389               1                   14:26               ?                   00:00:00            /bin/bash
[xinghai@center ~]$
```

**查看统计信息**

```shell
docker stats container
```

这里命令可以查看到容器的cpu，内存，存储，网络等使用情况的统计信息

**示例**

```shell
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS         PORTS     NAMES
45e47ce017d7   ce57623815a6   "/bin/bash"   7 minutes ago   Up 2 minutes             quirky_jennings
[xinghai@center ~]$ docker stats 45e47ce017d7
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT   MEM %     NET I/O     BLOCK I/O   PIDS
45e47ce017d7   quirky_jennings   0.00%     400KiB / 3.682GiB   0.01%     656B / 0B   0B / 0B     1
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT   MEM %     NET I/O     BLOCK I/O   PIDS
45e47ce017d7   quirky_jennings   0.00%     400KiB / 3.682GiB   0.01%     656B / 0B   0B / 0B     1
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT   MEM %     NET I/O     BLOCK I/O   PIDS
45e47ce017d7   quirky_jennings   0.00%     400KiB / 3.682GiB   0.01%     656B / 0B   0B / 0B     1
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT   MEM %     NET I/O     BLOCK I/O   PIDS
45e47ce017d7   quirky_jennings   0.00%     400KiB / 3.682GiB   0.01%     656B / 0B   0B / 0B     1
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT   MEM %     NET I/O     BLOCK I/O   PIDS
45e47ce017d7   quirky_jennings   0.00%     400KiB / 3.682GiB   0.01%     656B / 0B   0B / 0B     1
[xinghai@center ~]$
```

### 其他容器命令

**复制文件**

```shell
docker cp [options] <data> <container>:<path>
```

支持的选项包括(option)

-   -a,打包模式，复制文件会带有原始的uid/gid信息
-   -L跟随软连接，当源路径时软链接时，默认只复制链接信息，使用该选项会复制链接的目标内容

**示例**

```shell
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS          PORTS     NAMES
45e47ce017d7   ce57623815a6   "/bin/bash"   48 minutes ago   Up 44 minutes             quirky_jennings
[xinghai@center ~]$ ls
ubuntu
[xinghai@center ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS          PORTS     NAMES
45e47ce017d7   ce57623815a6   "/bin/bash"   48 minutes ago   Up 44 minutes             quirky_jennings
[xinghai@center ~]$ ls
ubuntu
[xinghai@center ~]$ docker cp ubuntu 45e47ce017d7:/tmp/
Successfully copied 65.5MB to 45e47ce017d7:/tmp/
[xinghai@center ~]$ docker attach 45e47ce017d7
root@45e47ce017d7:/# cd tmp
root@45e47ce017d7:/tmp# l
ubuntu
root@45e47ce017d7:/tmp#
```

**查看变更**

```shell
docker diff <container>
```

这个命令用于查看容器内文件系统的数据修改

**示例**

```shell
[xinghai@center ~]$ docker diff 45e47ce017d7
C /tmp
A /tmp/ubuntu
C /root
A /root/.bash_history
[xinghai@center ~]$
```

**查看端口映射**

```shell
docker container port <container>
```

这个命令可以查看容器内端口映射的情况

**更新配置**

```shell
docker container update
```

这个命令可以更新容器内的一些运行配置，主要是一些资源限制份额

### 关于导入导出

**`docker save`**：保存镜像的所有信息，包括历史和元数据。

**`docker load`**：从 tar 文件中恢复完整镜像，包括历史和元数据。

**`docker export`**：导出容器的文件系统快照，不包括历史和元数据。

**`docker import`**：从文件系统快照创建新镜像，不保留历史和元数据。

**`docker commit`**：保存容器的当前状态为新镜像，保留当前元数据，但不保留完整的构建历史。

## 访问docker仓库

仓库是集中存放镜像的地方，又分为公共仓库和私有仓库，和github差不多

注册服务器是存放仓库的地方，而仓库是存放镜像的地方

对于仓库地址，`registry.cn-guangzhou.aliyuncs.com/xinghai2524`来说，`registry.cn-guangzhou.aliyuncs.com`是注册服务器地址，`xinghai2524`是仓库名称

### 关于仓库

由于docekr Hub被封，这里用阿里云的仓库举例

阿里云给每位用户都提供仓库的服务，仓库可以设置成共有仓库和私有仓库

具体方法看[配置镜像仓库](https://help.aliyun.com/zh/acr/user-guide/create-a-container-registry-personal-edition-instance)

**相关命令**

登入

```shell
docker login <url>
```

搜索

```shell
docker search <image>
```

拉取

```shell
docker pull <image>
```

上传

```shell
docker push <image>
```

### 搭建本地私有仓库

Docker 官方提供了一个名为 `registry` 的镜像，这个镜像就是用来运行 Docker Registry 服务的。通过运行这个镜像的容器，你可以在本地搭建一个私有的 Docker 镜像仓库，用来存储和分发自己的 Docker 镜像

安装docker 后可以通过官方提供的registry镜像来简单搭建一套本地私有仓库环境

```shell
docker run -d -p 5000:5000 registry:2
```

**相关参数**

-   -d，后台运行
-   -p，容器和主机的端口映射
-   -v，指定仓库的本地路径，这个本地路径指的是容器内部的本地路径

**示例**

```shell
C:\>docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
mongodb      1         164a70fc6c88   21 hours ago    1.4GB
ubuntu       latest    35a88802559d   2 months ago    78.1MB
registry     2         cfb4d9904335   10 months ago   25.4MB

C:\>docker run -d -p 5000:5000 registry:2
41a9f4039921ff27d3d7c026354685248dd76cfb7fe1fc04ce290ab36a18b21b

C:\>docker ps -a
CONTAINER ID   IMAGE          COMMAND                   CREATED         STATUS                      PORTS                    NAMES
41a9f4039921   registry:2     "/entrypoint.sh /etc…"   5 seconds ago   Up 4 seconds                0.0.0.0:5000->5000/tcp   exciting_shamir
470d6272e7a5   164a70fc6c88   "/bin/bash"               21 hours ago    Exited (255) 11 hours ago                            blissful_moser

C:\>docker tag mongodb:1 localhost:5000/mongodb:1

C:\>docker push localhost:5000/mongodb:1
The push refers to repository [localhost:5000/mongodb]
8572abb1924a: Pushed
a30a5965a4f7: Pushed
1: digest: sha256:2d5280c48b73024e8cf4aec989952e6d107b6ea3cf7cc92d96d3d810fb745e79 size: 742

C:\>curl localhost:5000/v2/_catalog
{"repositories":["mongodb"]}

C:\>
```

`localhost:5000/v2/_catalog`这个地址可以看到docker仓库有哪些镜像

## Docker数据卷

### 创建数据卷

docker提供volume子命令管理数据卷，数据卷可以挂载到容器的内部，相当于mount行为，创建数据卷的作用仅仅是给数据卷命名，也可以不创建数据卷然后直接挂载本地目录到容器内部

**命令**

```
docker volume create <volume_name>
```

**示例**

```shell
xinghai2524@matebook:~$ docker volume create test
test
xinghai2524@matebook:~$
```

可以使用`volume ls`查看数据卷列表,使用`volume inspect <volume_name>`查看数据卷详细信息

```shell
xinghai2524@matebook:~$ docker volume ls
DRIVER    VOLUME NAME
local     test
xinghai2524@matebook:~$ docker volume inspect test
[
    {
        "CreatedAt": "2024-08-18T22:24:24+08:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/test/_data",
        "Name": "test",
        "Options": null,
        "Scope": "local"
    }
]
xinghai2524@matebook:~$
```

自动创建的数据卷和自己创建的数据卷只会放在`/var/lib/docker/volumes`目录当中，只有直接挂载本地目录才能指定路径

可以使用prune命令删除无用数据卷，可以使用rm命令删除数据卷

```shell
xinghai2524@matebook:~$ docker volume ls
DRIVER    VOLUME NAME
local     test
local     test1
xinghai2524@matebook:~$ docker volume rm test
test
xinghai2524@matebook:~$ docker volume ls
DRIVER    VOLUME NAME
local     test1
```

## 绑定数据卷

在**创建容器**时，可以将本地的任意路径挂载到容器内作为数据卷，这种形式创建的数据卷称为绑定数据卷

**命令**

```shell
docker run <image> [options] --mount <volume>
```

-   image,容器镜像
-   options，选项
-   volume,数据卷，支持三种数据卷
    -   volume，普通数据卷，比如自己创建的和自动创建的
    -   bind，绑定数据卷，

## 其他

### 关于ubuntu镜像当中命令少的问题

这里选择安装命令，脚本如下

```shell
#!/bin/bash

# 更新包管理器
apt-get update

# 安装常用命令和工具包
apt-get install -y sudo              # sudo 命令
apt-get install -y net-tools         # ifconfig 等网络工具
apt-get install -y iproute2          # ip 命令
apt-get install -y curl wget         # curl 和 wget
apt-get install -y iputils-ping      # ping 命令
apt-get install -y nano vim          # 文本编辑器 nano 和 vim
apt-get install -y procps            # ps, top, kill 等进程管理工具
apt-get install -y tar gzip zip unzip # tar, gzip, zip 等压缩工具
apt-get install -y coreutils findutils # ls, df, du, find 等文件管理工具
apt-get install -y git               # Git 版本控制系统
apt-get install -y adduser			 # adduser命令

# 清理不必要的包缓存
apt-get clean

# 显示安装完成的信息
echo "常用命令和工具包已安装完成。"
```



## 总结

**行百里者半九十，有志当世之务者,不可不戒,不可不勉**

## 参考

- 什么是容器？. (n.d.). https://www.aliyun.com/getting-started/what-is/what-is-container

- 逆流°只是风景-bjhxcc. (2023, May 11). *【Linux】Linux下安装Docker（图文解说详细版）*. CSDN. https://blog.csdn.net/u011397981/article/details/130616038

- 官方镜像加速. (2024, December 13). Aliyun. https://help.aliyun.com/zh/acr/user-guide/accelerate-the-pulls-of-docker-official-images#section-hif-tpa-zl8

- 创建个人版实例. (2024, October 18). Aliyun. https://help.aliyun.com/zh/acr/user-guide/create-a-container-registry-personal-edition-instance

  

