# Docker概述

## Docker为什么要出现

一款产品：开发---上线 是两套不同的环境，有时会遇到在自己的电脑上可以运行的软件在别的机器上无法运行，因为配置环境不同，而环境配置又是一件很麻烦的事情。

我们发布一个项目（jar+（Redis，MySql，jdk，ES，，，）），项目不能带上安装环境打包，在之前需要配置环境，而使用Docker可以解决这个问题。

java---apk---发布（应用商店）----张三使用----安装即可用

java---jar（环境）---打包项目带上环境（镜像）---（Docker:商店）----下载我们的镜像



Docker给出以上解决方案

Docker通过隔离机制，可以将服务器利用到极致

## Docker的历史

Docker 是 [PaaS](https://baike.baidu.com/item/PaaS) 提供商 dotCloud 开源的一个基于 [LXC](https://baike.baidu.com/item/LXC) 的高级容器引擎，源代码托管在 [Github](https://baike.baidu.com/item/Github) 上, 基于[go语言](https://baike.baidu.com/item/go语言)并遵从Apache2.0协议开源。

Docker自2013年以来非常火热，无论是从 github 上的代码活跃度，还是[Redhat](https://baike.baidu.com/item/Redhat)在RHEL6.5中集成对Docker的支持, 就连 [Google](https://baike.baidu.com/item/Google/86964) 的 Compute Engine 也支持 docker 在其之上运行。

一款开源软件能否在商业上成功，很大程度上依赖三件事 - 成功的 user case(用例), 活跃的社区和一个好故事。 dotCloud 之家的 PaaS 产品建立在[docker](https://baike.baidu.com/item/docker)之上，长期维护且有大量的用户，社区也十分活跃，接下来我们看看docker的故事。

虚拟机：在Windows中虚拟出一个真实的电脑，十分笨重

容器：Docker也是一种虚拟化技术，轻巧

```shell
vm:linux centos  原生镜像（一个电脑，几个g）隔离，需要开多个虚拟机
Docker：隔离，镜像机制（最核心的环境4M左右即可，4m+jdk+mysql），运行镜像即可
```

Docker是基于go语言的开源项目

官网：https://www.docker.com/

文档地址：官网doc

仓库地址：https://hub.docker.com/   docker push/pull

## Docker能干什么

![技术分享图片](http://image.mamicode.com/info/201805/20180511225652192444.png)

虚拟机缺点：

1、资源占用多（虚拟硬件，运行一个完整的操作系统，然后在这个操作系统上安装和运行软件）

2、冗余步骤多

3、启动时间长

容器化技术：

1、容器化技术不是一个完整的操作系统

2、容器内的应用直接运行在宿主机的内容

3、容器是没有自己的内核的，也没有虚拟我们的硬件。

4、每个容器是相互隔离的，每个容器都有自己的文件系统，互不影响

**应用更快的交付应用和部署**

传统：一堆帮助文档，安装程序

Docker：打包镜像发布测试，一键运行

**更便捷的升级和扩容**

使用了Docker，我们部署应用就和搭积木一样！

把项目打包成一个镜像，镜像带着环境直接能运行，服务器A出现问题可以直接在服务器B上直接运行！

**更高效的利用资源**

Docker是内核级的虚拟化，可以在一个物理机上运行多个容器示例！

# Docker安装

## Docker的基本组成

![img](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1596773147713&di=e7307f9d148c29e0e499c16a820cf8b9&imgtype=0&src=http%3A%2F%2Fn1.itc.cn%2Fimg8%2Fwb%2Frecom%2F2016%2F07%2F04%2F146760293629296553.PNG)

镜像：好比类，是一个模板 通过模板创建多个容器

容器：是方法，是镜像的实例，项目运行的地方 启动，停止，删除；目前可以把容器看作一个小型的Linux系统

仓库：是存储镜像的地方（Docker hub，阿里云）

一般要配置镜像加速，国外的仓库比较慢

## 安装Docekr

```shell
环境准备
```

1、熟悉Linux系统

2、Centos7

3、使用xshell操作阿里云的服务器

```shell
环境查看
```

```shell
#系统内核
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# uname -r
3.10.0-957.21.3.el7.x86_64
```

```shell
#系统版本
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# cat /etc/os-release
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

```



```shell
安装
```

查看帮助文档

```shell
#1、卸载旧的版本
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
#2、安装需要的安装包
sudo yum install -y yum-utils

#3、设置镜像的仓库
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo   

方法2
$ cd /etc/docker
$ cat daemon.json 
{
"registry-mirrors": [
"https://kfwkfulq.mirror.aliyuncs.com",
"https://2lqq34jg.mirror.aliyuncs.com",
"https://pee6w651.mirror.aliyuncs.com",
"https://registry.docker-cn.com",
"http://hub-mirror.c.163.com"
],
"dns": ["8.8.8.8","8.8.4.4"]
}

#更新软件包索引 
yum makecache faster 
#4、安装Docker
yum install docker-ce docker-ce-cli containerd.io

#5、启动Docker
systemctl start docker

#6、查看是否启动成功
docker --version
```

```shell
#7、测试hello-world
docker run hello-world
```

![image-20200807100217344](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807100217344.png)

```shell
#8、查看hello-world镜像
docker images

[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
docker.io/ubuntu        16.04               fab5e942c505        13 days ago         126 MB
docker.io/hello-world   latest              bf756fb1ae65        7 months ago        13.3 kB
```

卸载docker

```shell
#1、卸载依赖
yum remove docker-ce docker-ce-cli containerd.io
#2、删除安装环境
rm -rf /var/lib/docker
# /var/lib/docker   Docker的默认工作路径！
```

一些命令:

```shell
---重启docker
systemctl daemon-reload
systemctl restart docker

---查看docker是否运行成功
ps -ef |grep docker

---docker查看本地镜像
dicker image ls
```

## 阿里云镜像加速

虽然已经换成了阿里云的镜像源，但是还不够快，需要配置阿里云镜像加速

```shell
#1、登录阿里云，到容器镜像服务
```

![image-20200807100343111](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807100343111.png)

```shell
#2、登录，输入密码
```

![image-20200807100900893](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807100900893.png)

![image-20200807101023713](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807101023713.png)



![image-20200807101203549](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807101203549.png)

```shell
#3、配置使用，四个步骤
sudo mkdir -p /etc/docker

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://5ymqdd0h.mirror.aliyuncs.com"]
}
EOF

sudo systemctl daemon-reload

sudo systemctl restart docker
```

![image-20200807101451535](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807101451535.png)

## 底层原理

**Docker是怎么工作的**

Docker是一个C-S结构的系统，Docker的守护进程运行在主机上，通过Socket从客户端的访问

Docker-Server接收到Docker-Client的请求，就会执行这个命令

![image-20200807101905509](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807101905509.png)

**Docker为什么比虚拟机快**

![img](https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3029876800,3884924252&fm=26&gp=0.jpg)

1.Docker有着比虚拟机更少的抽象层，由于Docker不需要Hypervisor实现硬件资源虚拟化，运行在Docker容器上的程序直接使用的都是实际物理机的硬件资源，因此在CPU、内存利用率上Docker将会在效率上有明显优势。

2.Docker利用的是宿主机的内核，而不需要Guest OS，因此，当新建一个容器时，Docker不需要和虚拟机一样重新加载一个操作系统，避免了引导、加载操作系统内核这个比较费时费资源的过程，当新建一个虚拟机时，虚拟机软件需要加载Guest OS，这个新建过程是分钟级别的，而Docker由于直接利用宿主机的操作系统则省略了这个过程，因此新建一个Docker容器只需要几秒钟。



 # Docker的常用命令

## 帮助命令

```shell
#从Docker官方文档能看到所有的docker命令
docker --version
docker info
docker 命令 --help
```

## 镜像命令

**docker images  --- 查看所有镜像**

```shell
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker images --help
Usage:	docker images [OPTIONS] [REPOSITORY[:TAG]]
List images

#可选项
Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --help            Print usage
      --no-trunc        Don't truncate output
  -q, --quiet           Only show numeric IDs

```

**docker search 镜像名(mysql)  ---  搜索镜像**

```shell
#Docker Hub是一个大仓库，可以直接在该网站进行搜素，也可以通过命令进行索索
```

**docker pull  镜像名  --- 下载镜像**

```shell
docker pull mysql:tag #通常会加上版本名字，不然会选择最新版 

[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker pull mysql
Using default tag: latest
Trying to pull repository docker.io/library/mysql ... 

latest: Pulling from docker.io/library/mysql
bf5952930446: Pull complete #layer 分层下载
8254623a9871: Pull complete #如果再下载别的mysql版本，有些层不会重复下载
938e3e06dac4: Pull complete 
ea28ebf28884: Pull complete 
f3cef38785c2: Pull complete 
894f9792565a: Pull complete 
1d8a57523420: Pull complete 
6c676912929f: Pull complete 
ff39fdb566b4: Pull complete 
fff872988aba: Pull complete 
4d34e365ae68: Pull complete 
7886ee20621e: Pull complete 
Digest: sha256:c358e72e100ab493a0304bda35e6f239db2ec8c9bb836d8a427ac34307d074ed #签名
Status: Downloaded newer image for docker.io/mysql:latest #真实地址

以下两种方式是等价的
docker pull mysql
docker pull docker.io/mysql:latest

```

**docker rmi 容器id  --- 删除镜像**

```shell
docker rmi -f 容器id               #可以加多个容器id
docker rmi -f $(docker images -aq) #删除所有镜像
```

## 容器命令

说明：有了镜像才可以创建容器，先下载centos镜像来测试学习

```shell
docker pull centos
```

**新建容器并启动**

```shell
docker run [可选参数] imagesid 

#参数说明
--name="Name"  容器名字 tomcat01 tomcat02 用来区分容器
-d             以后台方式运行 ja nohup
-it            使用交互模式运行，进入容器查看内容
-p             指定容器端口 8000:8000
    -p ip:主机端口:容器端口
    -p 主机端口:容器端口（常用）
    -p 容器端口（不往外面走）
    容器端口
-P（大p）       随即指定端口

#测试，启动并进入容器
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker run -it centos /bin/bash
[root@646bda0434d6 /]# ls  #容器内就相当于一个小型centos，内部的centos极简，甚至很命令都没有
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@646bda0434d6 /]# exit  退出

```

列出所有运行的容器

```shell
docker ps    当前在运行的
docker ps -a 所有运行过的容器
-n=?         显示最近创建的容器
docker ps -q 只显示容器的编号

```

**退出容器**

```shell
exit    #直接容器停止并退出
Ctrl + p + q  #容器不停止退出
```

![image-20200807111833504](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807111833504.png)

***删除容器**

```shell
docker rm 容器id  #不能删除正在运行的容器，如果强制删除用 -f
docker rm -f $(docker ps -aq)
docker ps -a -q|xargs docker rm   #也是进行一个一个的删除
```

**启动和停止容器的操作**

```shell
docker start 容器id  #类似Linux命令
docker stop 容器id
docker restart 容器id
docker kill 容器id 
```

![image-20200807112927041](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807112927041.png)

1.docker run

docker run 只在第一次运行时使用，将镜像放到容器中，以后再次启动这个容器时，只需要使用命令docker start 即可。
docker run相当于执行了两步操作：将镜像放入容器中（docker create）,然后将容器启动，使之变成运行时容器（docker start）。

2.docker start
docker start的作用是，重新启动已存在的镜像。也就是说，如果使用这个命令，我们必须事先知道这个容器的ID，或者这个容器的名字，我们可以使用docker ps找到这个容器的信息。

**其它常用命令**

```shell
#docker run -d 容器名:版本号/容器id
docker run -d centos #后台运行

#发现centos停止了
#常见的问题，docker容器后台运行就必须有一个前台进程，docker发现没有应用就会停止后台
#nginx,容器启动后发现自己没有提供服务，就会立即停止，会觉得们没有程序了
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker run -d centos
9764f954e0bdb028a1250a26dcb3f53bfba43255c179224e93c0ab5341b7164a
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

```

查看日志

```shell
#1、必须先启动一个容器才能查看容器的日志
docker logs 容器id
docker logs -f -t --tail 10 容器id  如果没有日志

#2、自己编写一段shell脚本
"while true;do echo lmqlmqlmq;sleep 2;done"

#如果-C(大写)运行后会停止，docker ps看不到容器信息,用-c
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker run -d centos /bin/bash -c "while true;do echo lmqlmqlmq;sleep 2;done"
16affb1398622758ff995ae0f08ab46517d57bea6d6e4837d6f344561cfcec22
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
16affb139862        centos              "/bin/bash -c 'whi..."   4 seconds ago       Up 3 seconds                            unruffled_mcclintock

#3、显示日志
-tf           #显示日志，-t带上时间戳，-f
--tail number #要显示的日志条数
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker logs -f -t --tail 10 16affb139862
2020-08-07T03:53:14.637801000Z lmqlmqlmq
2020-08-07T03:53:16.639865000Z lmqlmqlmq
2020-08-07T03:53:18.641960000Z lmqlmqlmq
2020-08-07T03:53:20.644091000Z lmqlmqlmq
2020-08-07T03:53:22.646119000Z lmqlmqlmq
```

**查看容器中的进程信息**

```shell
#docker top 容器id 
```

![image-20200807115853883](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807115853883.png)

**查看镜像元数据**

```shell
docker imspect 容器id

docker inspect --help
Options:
  -f, --format string   Format the output using the given Go template
      --help            Print usage
  -s, --size            Display total file sizes if the type is container
      --type string     Return JSON for specified type
```

```shell
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker inspect 16affb139862
[
    {
        "Id": "16affb1398622758ff995ae0f08ab46517d57bea6d6e4837d6f344561cfcec22", #完整容器id，平常使用只是个缩写
        "Created": "2020-08-07T03:50:32.296721312Z",
        "Path": "/bin/bash", #默认控制台
        "Args": [ #写的脚本
            "-c",
            "while true;do echo lmqlmqlmq;sleep 2;done"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 29158,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-08-07T03:50:32.467204489Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image":     "sha256:831691599b88ad6cc2a4abbd0e89661a121aff14cfa289ad840fd3946f274f1f",
        "ResolvConfPath": "/var/lib/docker/containers/16affb1398622758ff995ae0f08ab46517d57bea6d6e4837d6f344561cfcec22/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/16affb1398622758ff995ae0f08ab46517d57bea6d6e4837d6f344561cfcec22/hostname",
        "HostsPath": "/var/lib/docker/containers/16affb1398622758ff995ae0f08ab46517d57bea6d6e4837d6f344561cfcec22/hosts",
        "LogPath": "",
        "Name": "/unruffled_mcclintock",
        "RestartCount": 0,
        "Driver": "overlay2",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "journald",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "docker-runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": null,
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DiskQuota": 0,
            "KernelMemory": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": -1,
            "OomKillDisable": false,
            "PidsLimit": 0,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0
        },
        "GraphDriver": {
            "Name": "overlay2",
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/f7ff5c54808cfacf85a01edf550227db9027a4cc8457993669d9cd913222ef59-init/diff:/var/lib/docker/overlay2/a6ba88ec2cab766fa44baff48685b2cf942dc4fe6b8fcbf460b5583e7f486458/diff",
                "MergedDir": "/var/lib/docker/overlay2/f7ff5c54808cfacf85a01edf550227db9027a4cc8457993669d9cd913222ef59/merged",
                "UpperDir": "/var/lib/docker/overlay2/f7ff5c54808cfacf85a01edf550227db9027a4cc8457993669d9cd913222ef59/diff",
                "WorkDir": "/var/lib/docker/overlay2/f7ff5c54808cfacf85a01edf550227db9027a4cc8457993669d9cd913222ef59/work"
            }
        },
        "Mounts": [],
        "Config": {
            "Hostname": "16affb139862",
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
                "/bin/bash",
                "-c",
                "while true;do echo lmqlmqlmq;sleep 2;done"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20200611",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "03759287d4941da9f17db05a68159926843166e4ecffdfbbf45e89653a312c08",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/03759287d494",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "261c952b5a1e07c7c66b0c103c950d5bd73eb736f60aa605e991813c9d7a27b1",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "b3b0057dba5f5e6edf86e2fe663cb8ebfc231bea3e705c5df22ed71c0fa28b5c",
                    "EndpointID": "261c952b5a1e07c7c66b0c103c950d5bd73eb736f60aa605e991813c9d7a27b1",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02"
                }
            }
        }
    }
]
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# 

```

**进入当前正在运行的容器**

```shell
#我们通常容器都是后台运行的，需要计入容器，修改一些配置

#命令
docker exec -it 容器id bashshell（通常用/bin/bash）
#测试
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker exec -it 16affb139862 /bin/bash
[root@16affb139862 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@16affb139862 /]# ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 03:50 ?        00:00:00 /bin/bash -c while true;do echo lmqlmqlmq;sleep 2;done
root      1948     0  0 04:55 ?        00:00:00 /bin/bash
root      1969     1  0 04:55 ?        00:00:00 /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 2
root      1970  1948  0 04:55 ?        00:00:00 ps -ef

#方式二
docker attach 容器id
#测试
正在执行当前的代码···

#区别
#docker exec    #进入容器后开启一个新的终端
#docker attach  #进入容器正在执行的终端，不会启动新的进程

```

**附:**

```shell
#exec
在一个正在运行的容器中执行命令，exec是针对已运行的容器实例进行操作，在已运行的容器中执行命令，不创建和启动新的容器。
#attach
将本机的标准输入（键盘）、标准输出（屏幕）、错误输出（屏幕）附加到一个运行的容器，也就是说本机的输入直接输到容器中，容器的输出会直接显示在本机的屏幕上。
```

**从容器内拷贝文件到主机上**

```shell
docker cp 容器id:容器内路径 目的主机路径

[root@iZ2zeimzcyvwdtmorvt1gfZ home]# docker attach ee6d5a40e3bf  #进入容器
[root@ee6d5a40e3bf /]# cd /home
[root@ee6d5a40e3bf home]# ls
[root@ee6d5a40e3bf home]# touch con.java  #容器内创建文件
[root@ee6d5a40e3bf home]# exit  #退出
exit
[root@iZ2zeimzcyvwdtmorvt1gfZ home]# docker cp ee6d5a40e3bf:/home/con.java /home   #拷贝到主机/home目录下
[root@iZ2zeimzcyvwdtmorvt1gfZ home]# ls
con.java  lmq-learn-cp.java

```



## 小结

![https://philipzheng.gitbooks.io/docker_practice/content/appendix_command/](https://images2015.cnblogs.com/blog/59618/201705/59618-20170519215116432-38667527.png)



## 作业练习

>**Docker安装Nginx**

```shell
#1、搜索镜像
docker search nginx

#2、下载/拉取镜像
docker pull nginx

#3、运行nginx (nginx默认是80端口，映射到外部3344端口)
#从公网的3344端口可以访问到docker里面的80端口的nginx服务
#注意需要在阿里云的安全组里面打开3344端口
-d       #后台运行
--name   #给容器取名字
-p       #暴露端口
docker run -d --name nginx01 -p 3344:80 nginx

#4、测试
#内部测试
curl localhost:3344

#5、进入容器
[root@iZ2zeimzcyvwdtmorvt1gfZ home]# docker exec -it nginx01 /bin/bash 
root@29c8c9dbaf17:/# whereis nginx  #查找nginx的位置
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@29c8c9dbaf17:/# cd /etc/nginx
root@29c8c9dbaf17:/etc/nginx# ls
conf.d	fastcgi_params	koi-utf  koi-win  mime.types  modules  nginx.conf  scgi_params	uwsgi_params  win-utf

#进入后就可以动态的修改nginx文件了
```

![image-20200807152022513](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200807152022513.png)

思考问题：每次修改nginx配置文件，都需要进入容器内部？十分的麻烦，如果可以在容器外部提供一个映射路径，达到在容器外面修改文件，容器内部就可以自动修改--------数据卷技术volume

> **作业2:使用docker来装一个tomcat**

```shell
#官方文档写法
docker run -it --rm tomcat:9.0 #用完容器后就删除，一般用来测试（不推荐）

#如果直接run，docker会自动帮我们下载
docker run -it tomcat /bin/bash 

#后台方式运行
docker run -d -p 3355:8080 --name tomcat01 tomcat

3547198c7a4a921f474e3d80ac283731a45d838a1866c96fa780cb2a0980a851

#查看
[root@iZ2zeimzcyvwdtmorvt1gfZ ~]# docker exec -it tomcat1 /bin/bash
root@7a2324070da3:/usr/local/tomcat# ls
BUILDING.txt	 NOTICE		RUNNING.txt  lib	     temp	   work
CONTRIBUTING.md  README.md	bin	     logs	     webapps
LICENSE		 RELEASE-NOTES	conf	     native-jni-lib  webapps.dist

#访问公网地址
http://39.105.9.190:3355/ #如果没有打开阿里云安全组就无法访问

#测试访问没有问题

#进入容器
docker exec -it tomcat1 /bin/bash
发现问题：1、Linux命令少了，2、没有webapps（因为阿里云的镜像默认是最小的，所有不必要的都剔除掉，保证最小可运行的环境）
将webapps.dist下文件拷贝到webapps下即可
```

![image-20200810104540967](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200810104540967.png)

![image-20200810104559523](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200810104559523.png)

思考问题:

我们以后部署项目每次都要进入容器内部十分麻烦？是不是可以在容器外部提供一个映射路径，webapps，我们在外部放置项目，在自动同步到内部

>作业：部署es+kibana

```shell
# es 暴露的端口非常的多
# es 十分的耗内存
# es 的数据一般需要需要放置到安全目录：挂载
# --net somenetwork ?网络配置，下面可以不带

#启动elasticsearch
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:tag

#启动以后linux很可能就卡住了,因为es十分耗内存，一两个G
#停止elasticsearch
docker stop elasticsearch_id

#查看docker stats
docker stats

#测试es是否能够成功

#测试完后赶紧关闭
```

## 可视化

- portainer(可视化工具，先用着)

```shell
docker run -d -p 8088:9000 \

--restart=always -v /var/run/docker.sock:/va/run/docker.sock --privileged=true portainer/portainer
```

- Rancher (CI,CD再用)

  

**什么是portainer**

Docker图形化界面工具，提供一个后台面板供我们操作

```shell
docker pull portainer/portainer
```

```shell
$ docker volume create portainer_data
$ docker run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

通过访问运行Portainer的服务器上的端口9000来使用Portainer。（22换成9000）（不常用）

![image-20200810125447756](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200810125447756.png)



# Docker镜像讲解

## 镜像是什么

镜像是一种轻量级、可执行的独立软件包,用来打包软件运行环境和基于运行环境开发的软件,它包含运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置文件。

所有的应用直接打包部署！

**如何得到镜像**

- 从远程仓库下载
- 朋友拷贝给自己
- 自己制作一个Dockerfile

## Docker镜像加载原理

>UnionFS（联合文件系统）

**UnionFS (联合文件系统)** **:** Union文件系统( UnionFS)是-种分层、 轻量级并且高性能的文件系统,它支持对文件系统的修改
作为- -次提交来- -层层的叠加,同时可以将不同目录挂载到同-一个虚拟文件系统下(unite several directories into a single virtual file system)。Union 文件系统是Docker镜像的基础。镜像可以通过分层来进行继承,基于基础镜像(没有父镜像) , 可以制作各种具体的应用镜像。
**特性:** 一次同时加载多个文件系统,但从外面看起来,只能看到一个文件系统,联合加载会把各层文件系统叠加起来,这样最终的
文件系统会包含所有底层的文件和目录

>Docker镜像加载原理

docker的镜像实际上由一层一层的文件系统组成,这种层级的文件系统UnionFS

bootfs(boot file system)主要包含boot loader和kernel, boot loader主要是引导加载kernel, Linux刚启动时会加载bootfs文件系统,在Docker镜像的最底层是bootfs。这一层与我们典型的Linux/Unix系统是一样的,包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了,此时内存的使用权已由bootfs转交给内核,此时系统也会卸载bootfs.

rootfs (root file system) , 在bootfs之上。包含的就是典型Linux系统中的/dev, /proc, /bin, /etc等标准目录和文件。rootfs就是
各种不同的操作系统发行版,比如Ubuntu , Centos等等。

![img](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCAFyAfQDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD3eiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKq3up2GmRiS/vra1Q9GnlVAfzNAFqiuG1P4weCNMBDaylwwOCtshc/4Vx9/+0Pp28x6PoN5eSZ48xggP5ZP6UA3bc9por57ufit8SdXyum6PaadGTlXMRZwPcucf+O1kXNv8Qdd3f2r4nljjY5aOOQgfgFwK6IYSvP4Ys4quY4Wl8dRfn+R9GX+uaTpcbPf6laWyrwTLMq4/M1x+qfGfwNpe9f7WN3Iv8FpE0m76Nwv6145F8ObJ5PN1DULu7k7ksFz+eT+tbNp4Q0Kzx5enxMR3ky5/WuuGVV5fFZHnVeIsJD4E5fK35no+l/GzwNqe0NqclnIxxsu4WXH1YZX9a7Cw8Q6NqqB7DVbO5UnAMUytn9a8KuvCeh3mfN06IE90G0/pWLP8ONO3+ZZXl3ayDoQwYD+R/WieVVo/C0xUuIsLL404/j+R9Q0V8xW+n+OtD/5BHimdkBzseRsH6g5Fa9v8T/ido/F9ptnqUYPLGHDY9thH8jXJPCV4fFFnpUsywlX4Ki/L8z6GorxKy/aHto38vWvDl3aP/0yfd+jAGuu034z+CNR4Oqm1b0uYmX9ea52rHYmmro7+iqOn61perLnTtRtLvAyRBMrkD3APFXqBhRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUVFcXVvZwma5nigiXq8rhVH4mgCWiuQ1T4o+DNJ3ifXbaR1/ggPmE/Tbx+tcbqX7Q3h+Bmj03Tb69f8AgJAjUn8ef0oA9hor5/ufjN461XK6P4at7SNhw8yvIw9wSVH6Gsm5vPibruft3iFrWNhgpCwQY+iAVvDDVp/DFnJVx+GpfHUS+Z9G3WoWViha7u4IFAyTJIF4/GuU1P4s+B9KyJteglfGdtsrTE+3yggfjXh6/D0XTiTVdYvLpvY/1bNatp4J0C0wRYiVh3lYt/8AWrrhldeW9kedV4hwcPhvL0X+djq7/wDaH0YHZpOi6heN6ybYxn8NxP6Vg3Hxd+IOrcaVoEFoh6M6E/qxAqb/AIlellEJtLUt90EqhP0q4jrIoZGDKehByK6qeUQv70/uPOrcSVLXp07Lz/pHL3DfEnW8f2j4nktU/uQSlCP++AM/nVKL4c2zuZdQ1G5uZDyxzjP4nJrt6xdf8PnW4lC39zaug48tvlP1FdP9n0acbxjzPzZwf21iq01GdTkXkv6ZDaeEPD1qRss4pGHeVt36dK24baC2TZBDHEv91FCj9K8yuvCt3oLG8v5ZbyzXg+ROyMPfof8APetC18e6RptmEtbe+kY/wzS7sfiSf0pUsTTpO04qH9ehdfA1q6UqNR1fy/F6fcehUVwlj8Rje3IhTR5nY9BE+4/liuh1HTB4k0yMSSXli/UBW2kH/aHeuqGJhVi3S1f3Hn1cDUoTSxHup+j/AATNdpolIDSoCemWFOBBGQcj2rziT4e6hFdI5uxewqeUMhjY/jzirrafd6aP9F0fUww7xX+R+v8AhWSxNVfHC33v8kdEsBh3b2VbmfyX5tP8Du6K4u28QeIoFEX/AAj91Pz96add36KK1INa1p+ZvD0qDviZSa1jioS7/c/8jnqYCrDdr/wKP+Z0FFYNx4rtLBkGpW11Zb+FMiZB/EZrRsdX0/UhmzvIpj6K3P5da0jWpyfKnqYzw1aEedxdu/T79i1LDFOhSWNJFP8AC6gise78I6FeZL6dEjHvENn8q26Kc6cJ/ErkU69Sk705NejOKuPhvp5bfZ3lxbsORznFWLe1+IOif8grxXPKijAjmlYjHoA24D9K62iuWeXYef2beh6NLO8bT+3f1Mi2+KXxJ0fA1HSLe/jUYyqcn3JQ1t2H7Q1ihVNa8P3tqwHzPCwfn2VsfzqOopraC4GJoY5B/tqDXJPJ4/Yl956VLiWov4kE/TT/ADO30v4x+BtU2qusrayN/BdxtHj6sRt/WuusdZ0zUo1ex1C1uVb7pilVs/ka8BvfCPh+4RnmsYogOS6HZj8q4zU9K8MaXIXsdfuYZx0EJ8zH4jH864a2XVKSu2vvt+Z62FzujiHyqMr+l/yPr+ivjnSfHfjOwmCaRrWoyxIflV/nX8Qcive/g3421jxno2oNrTRST2kyosqIELAgnkDjjHauBpo9hST2PS6KKKQwooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKa7rGhd2CqoyWJwAKAHUVzWpfELwlpP8Ax96/Yhv7scokP/jua43Uv2gPCdpxZw3163+xGEH5saAPV6K8EuPjn4p1HjQ/CccYP/LS4LyA/ltA/M1kXHiD4qa3/rtWTT4yfuwhY8f98jP61tDD1Z/DFs5quMw9L+JNL5n0dNcQ267p5o4l9XYKP1rmdT+JXg3SMi78QWYZTgpExlYfggJrwVvA19qLb9Z8QXdySclQxPP1Y/0rQtPAOgWuC1u87DvM5P6DArrhleIlurHm1c/wcPhbl6L/ADsdxqX7QfhmAlNNsdQv5AcA7BGpHqCST+lc9c/Gvxhqm5dE8MpAhPyyShnI+ucCpLbSrCzAFvZwR4/uoKt11wydfbl9x51XiZ/8u6f3s5m51X4pa5uF1rY0+JjkpAwQj6FBn9azj4AmvpjPrGt3d5MfvMzFifxYk129FdcMtw8d1f1PNq57jam0rei/zuc5aeBdBtcE2hmYd5XJrattPs7Ndttawwj/AKZxhf5VZrP1bWrLRLYT3suxWOFAGSx9hXSqdKirpJI4JVsTiZcrk5N9NWaFFcW3xL0kNhbe5YeuB/jUkXxH0V/vpcJ9Uz/Ks/ruH/nRs8qxqV/Zs7Cqdzq2nWblLi+t4mHUPIAazrbxloN0QFv0QntICtclr/gd72eXUdFuUuUlYu0e8Egn0PelWxMlDmoJS+ZeFwMXU5MW3TXS6O0k1bQb5DDJe2M6n+BnVh+RrMu/DmnvC8uiTi1uyMoYbgqhPuBXFaFBo+nzva+JdOmjmZvklk3BQPTA/nXcW3hnwxfxebZxoyn+KCdhj8jXPTqSxMdYxv66r8DsrUIYGXuzny97Jxf4pMwJYviDFH5AbzB2lRoyfzNZFzpni+GZZL6XUVQ8tJDKZNv4K1dz/wAIrLbc6drd/b/7LsJF/I/41HNL4s0wbtlnqkK8naDHIf6fpWc8K7e+5ffdf5m9LMFf90qevlyv8dPxK/hvU7OH93ceInuXIx5V0nlkH/gXJ/OukNhp1y3mm0tZSf4zGrfriuWTxV4d1Vjb6tZi3mBwy3EWcH61fTwvp0sa3Gk31zaBuVa2nyh/A5FdNGd42haSXnr+N/zOHE0uWfNU5qbfkrferfkzUutB0m9/1+nwMf7wQK35jmqTeHvso3WWrXloB0Vpd6D8GqI2nimzH7jUbO9UdBcQlG/NTWDr8XjPVLQ2ktjaiEkE/Zzyce5Joqzik5ezd/T9UGHpVJSUfbx5fN/pI6LPiO1Quk1hfRgZO7MbY+oyKyR8R7GFnju7OdJk4xGyupP1yK5ew8P+MLaYG3S5gI7mXA/nXo0OiW91p8A1e0tri72ASuIxy1ZUp16vwXj66r/M6MRSwmHf71qd/wCXRr1S0ONvPiJaXv7qbRUnhzwsrAn+XBq5pUena8wS3tNY04no0UreWPxzXVW3h7R7N98GnW6N67ATWkAFAAAAHYVpDDVZO9aSfy/Uwq4/DRjy4WDj58z/AC1Rw9z8OVuZw8mr3Mij/nr8x/OrFp8OtNtZ0m+1XTMhBGGCkH6iuxpksscMZklkWNB1ZzgD8a0+pYdPm5TB5rjZLk53+A8cDFFc9f8AjbQ7HIN2JnH8MI3fr0rAl+IF/esU0fSGf0eXJ/QYH61U8ZRhpzXflqTSyzFVVdQsu70X4noFUrzWNO09S13ewxezOM/lXBSW/izV/wDj91D7NGeqIcfotPtvBdijb7uaa5k77mwD/X9axeLqy/hw+/T8DqjltCn/ABqt/KKv+OxrXvxG0uIlLKGe7fsQuxT+fP6VlyeJPFmrcWVklpGf42HP1y3+FbNtptlZjFvbRR+4XmrVZtV5/HO3pp+JtGWEpfwqV33lr+Gxyh8MalqLh9X1aSXnOxWJA+meB+VaVp4W0q0wfs4lYd5Tu/TpWzRSjhqcXe1356jnja8ly81l2Wn5EflpFCVjRUUA4CjArqP2c/8AkE+IP+vqP/0E1zL/AOrb6Gum/Zz/AOQT4g/6+o//AEE1w5l9n5nrZF/y8+X6ntlFFFeWfQBRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFAHnPij40+GfDGp3OmOl5d3tudrrDGAgb0LEj9Aa4y4+POu6lkaD4WO0jAeVmkIPrwAK43WdGtNb+K/ie2uw+0SOylGwVOVGf1qE+HPEPh9jJomoNPCOfJf/AAPBrro4SU4qo03Hy3PNxWYwpTdFNKf97b7zorjxR8Vtb+9ew6ZGwwRGFXj8NxH6VlS+C9W1ZxJrniO8u2HZpGfH0LGmWXxBMEwttdsJLWUdXRTj8jz/ADrr7HUrLUovNs7mOZe+08j6jtXqYfCYOfwu789/u0Pn8bmOaU/iXKu6V19+pgWnw/0K3wZIpJz/ANNHOP0rctdH02xx9msbeIj+JYxn8+tXaK9KFClD4YpHh1cZiKv8SbfzDpRRRWpzhRRRQAjMqKWYgKBkk9q5y88d6BaEqLpp3H8MKFv16frXSEAjBGRWFe+DtCvpTJLYqrk5JjYpn8qxr+2t+6tfzOrCvC83+03t5W/Uy7vx/p0mi3E9hJi8QDbDOuD1x9D+dcd/wn+vl932iP6eWMV3c3gHQJbcxJbPEe0iSHcPzzXJ6r8OL+13PYTLdRjop+V/8DXl4qGO0lf/AMBPoMBUyjWNt39pL89joNP1Txk0EU0uk29zFIoYFZVQkHn+9W5qekQeI9JSK/geCQjco3AtG31HBrlND8ZHRbaHS9bs7iFoRtWQjt2yP8K7aw1aw1SPfZ3Ucw7hTyPqOtdeGlTqQ5XJu+6f/DXPNx0K9Cp7SNNRs9JRvZ/i0eWX/g7VtCu0uUtlvreNg2VXcCB2Zetdpo/jLRbyNYJ1SxuOjRSLtXPsen511dY2oWHh/UJDFerZNKeOXUP/ADzSjhHh23Rej6P/ADHUzFYyKjiottdY7/NbfkWZNM0nUY8vaWk6n+IIp/WsqbwPpe8yWT3NjL2aCUjFVZPAVvF82mane2bdgH3L+XB/WoJND8YWo/0XXFnUdBJ1/UU53f8AEpX9LP8AyYqVl/BxNvJ3X+aKmrw+I9Bt2knkh1fTh98Txhio9/8AGqGnXvhXVJVEsMukXZPEkMhVM/XtUmo6R44vYWguZvNifhlSRQD+VZEfgLX5GwbZF92kFefUdXn9yDa7SV/ue/4ntUI4d0v3taKl3i7fetn9x3J0HXYQG0/xHI6EcC4QPn8arTQeO4gVjnsZh2K8H9QK2vDGlXej6OlpeXAmdSSMdEHpWzXqRw6lFO7j5XPn6mNcKjjaM0uritfyPItQ8JeLNRvHurqzEsr9WE0Y/rW74Q8NeItI1FZZ3SC0P+tiMgbd+A4z716BRWdPLqUJ+0Td/U2rZ3Xq0XRcYqNrbf8ABCio57iC2j8yeaOJP7zsFH61zt/470OyyFuGuHH8MK5/XpXXUrU6fxux5tHDVqztTi36HTUV59L461jUCV0jSMKekkuW/wAAP1qq+n+J9XOdQ1QwoeqIcfoMCuV46L/hxcvwX4noRyipHWvNQ+d39yO6vte0rTgTd38MZ/u7st+Q5rm7z4j2CsY9PtJ7p+gJG0f4/wAqoWvgzTYTunMtw/fe2B+Qrat7G1tFAt7eOMD+6uKh1cTPtH8X/kbRw+Bpd5v7l/mYcmt+MNW4trdLGI/xEAH9ef0qAeE7q9cS6tqk07egYnH4murorN4dS1qNy9f8jVY109KMVD0Wv3sybTw3pVngrarIw/ik+b+fFaqqqABVAA6ACloyM4zyK2jCMNIqxz1Ks6jvNthRRVPUpPLsyxJEe5fMI7Jnn9KcnZXJjHmkkTLd2zzeUs8Zk/uhuamrJmuYJ2to7SJpVRw+6NflAHYHpzV20adzOZ0KfvPkUkHC7V/rmojO7saTpcqvt6lmiiq97dfY7Yy+TJKcgBIxknNW2krsyjFydkTP/q2+hrpv2c/+QT4g/wCvqP8A9BNcy/8Aq2+hrpv2c/8AkE+IP+vqP/0E15mZfZ+Z7+Rf8vPl+p7ZRRRXlH0IUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQB8yH/AJLH4o/3n/8AQlrpK5s/8lj8Uf7z/wDoS10lfR5b/u69WfD57/vj9EV7uxtb+ExXdvHMh7OucfT0rlL3wGkcv2nRr2WzmHIG44/Mciuzorqq0KdX4kefQxleh/Dlp26fccOniPxN4eYJrFj9rtxx5yf4jj8xXR6V4v0fVtqx3IimP/LKb5T+HY/hWoyhlKsAQeoNc/qngzSNSy4iNvMf44eOfcdKy5K9L4Jcy7P/ADOl1cHiP40OR947fNf5HVA5GR0orzwWHizw0d1hci/tV/5Zvzx9DyPwNaOnfEKzkk8jVLeSxnBw2QSv+Iq44yF+WouV+e33mU8sqNc9BqcfLf5rc7Kiora6gvIRLbTJLGejI2RUtdaaeqPOaadmFFFFAgooooAqala291ZSLPZpdgKSImAJJ9s9DXiuqObbU2e1sp9NKnhC7ZU/WvdahuLS3ul23EEco9HUGuLGYP6wlZ2a8v6Z6uW5l9Tb5o8yfn+mx4fNres6iohkvrqYYxsDHn6gdat2Pg7XtQwyWTxof45jsH68/pXsVvp9nac29rDEfVEAqzXLHKru9WbZ31OIXFcuHpqP9dlY5Lwx4X1PRJQ9xqrPFjm3TJQ/n/SutoqC5vLazj33NxFCvq7AZr0qdOFGHLHY8OvXq4qpzz1b7L/Inorlb74gaJaZEUkly47RLx+ZrGk8aa/qXy6VpQhQ9JJAWP15wP51lPG0Yuyd35anTTyrFTXM48q7vT8z0MkAZJwKy77xJo+m5F1qEKsP4VO5vyGTXCnS9e1h2Go6ztCn5o42zt9sDAFXbTwfpdvgyK9w/rI3H5CsXiq0/wCHC3r/AJI6Vl+Gp/xql32iv1ZZuviPbsxj0ywnuX7FxtH5DJqhJqfjLV/9WqWEJ78Kcfjk1vwWtvbLtghSMf7K4qas3CrP+JN/LQ1jUw1L+DSXrLX/AIByqeD3uZPN1PUZriQ9eSf1Na9p4f0uywYrSMsP4nG4/rWnRThh6cdUgqYyvUVnLTstF+AgAAwBgUtFFbHKFGRnGeRVGCSefUJ284C3iOwRhRy2OSTSMoGto0Z5MR80Dp1+XP61HP1NfZ62b6XL9FFFWZGVBePFe3MPkyXBL7g8fIH+yc8Aip7Lzje3byxeWW2YGc9vWlN3bW4nEQJdG+cAdXPbPrT7W5llllhniEckeD8rbgQc47exrGNrpXOmd+VtRtov0LVVNRaJbUGVQw3rgMcDOeM+1W6p6nFLNZ7IUDsXX5W+6wzyD7VpP4XYypW51crmXzJERrgysGH7u3X5R9T6VqVnSxSokZmnWFN6gJAnHXoSf/rVo1ML63Kq2srBSEhRkkAeppar3lnFfW/kTbjGSCQpxnFW720Mo2vrsTP/AKtvoa6b9nP/AJBPiD/r6j/9BNcy/EbfQ1037Of/ACCfEH/X1H/6Ca8zMvs/M9/Ivt/L9T2yiiivKPoQooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigD5kP/ACWPxR/vP/6EtdJXNn/ksfij/ef/ANCWukr6PLf93Xqz4fPf98fogooor0DxgooooAKo6hpGn6pHtvLWOX0Yj5h9D1q9RUyipKzVyoTlB80XZnET+CbzTpjc6BqUkL/883bGfbPf8RSw+MtZ0aQQa/prlRx50Yxn39DXbUySKOaMpKiuh6qwyK5vqvJrRly/ivuPQ/tD2i5cVBTXfZ/eitpfiPStYUfZLtC+OY3+Vx+BrVrjdS8CaZdsZbRnsp+oaP7ufp/hWcJvF/hnggalZr65YgfzH60/rFWn/Gjp3X+W5LwWHr64apZ9paP5PZnodFcnpnxA0m8Gy7L2Uo6iTlfzFNvviHo9qStuJbp+g2Lgfma0+uUOXm5kYf2Zi+fk9m7/ANddjrqRmVQSxAA7k155J4t8Tapxp2mpaxno7jcfzOB+lVm8P61qh3arq77T1RST+HYVk8cn/Ci3+C/E6Y5S4/x6ij5bv7l/mdrf+KtE07Inv4i4/gj+ds/QdPxrnLn4jCV/L0rTJp27NJxn8Bmo7TwlpNrgmJpmHeVs/p0rZigigXbDEka+ijFZueJnu1H01ZtGlgaW0XN+bsvuRzsl14z1fhpVsIj/AHcKf0yf5UyLwYksnm6jfTXMh5Y56/iea6mio+rRes25erNfr04q1JKC8l+u5lDStM0m0lnitI1MaFt7LuP61Y02O5W2El3P5kkgDbQoCr7CrM8KXEDwyDKOpVh7VnmCazgCzatsgXgMyKGx6bjx+lVyqDuloZqbqRalLVvrr924rxqPEMTwDDeS32jHccbc++c1p1T09rIo4tJVlOcu27cxPvVyrgtL9zOq3dJ9NApGYKpZiAoGST2papasobSboFyg8snIGf0qpOybIhHmkl3AXk04zaWxZD0lkO1T9B1P5U+zS6VpzdSI25wUCdFGBx+eahgm1KeFc20Ns2OS7bsfQD/EVLZ200D3DTT+aZHDA4xgbQMY7dKzi22nr+RtJKKa0/N/fsW6KKRmCqWYgAdSa1OcqPYfv3liuJYfMOXVCME+vI4NLEYba5FsqtvkUvvY5L465PrVS11IPcXaxiS4xLhPLGQBgd+lWooZpbtbmdVj2KVRAcnnqSaxTT1idMoyjpUfT/hi5RRRWxzGZFZ3HnlJAghE5m3hslvQY7Y/pVm0j2TXDPMskzMCwAxtGOBTDFNKZWuZ2jiViFVDtBX1J61HpkSRS3JgJNuzBkY85OOcHuKxSs1odMneLbf9epo1R1K8W2WICTDtKg2qMsRuGeOtXqpve6cz/PcW+4EfeYA5FXN6WvYypL3r2uDia82q0Jih3BiXI3HHsOlXKgW8tX+7cwn6SCob3VrHT1zc3CIcZ25yT+FF4xV2x8s5tRUfkXarX8lzFalrVY2lyB+8bAA7msJPEWoaxcG18P6VNdS/3tpIH4Dp+JrotO+E/iTXSs3iHVBZwnkwRfM2PTA4H6/SuSrjqaVo6no0MqqtqVSyXn/kY+oeKNMs1aMS+fLjGyIZ5+vSui+C/jDSPCFnqcGvyT2IvJkkhlkt3KEAEHJAOOvfiu40H4ceGfD+1rewWecf8trn943+A/AV081tBcReVPBHLH02OoI/I151etOs1zdD2cJQp4VNQu773NvTdd0nWIhJpupWl2h7wyq38q0K8tvvhx4avJTPDaPY3HaaykMTD8uP0qGPRPG2h4Oh+Lmu4Vxi21WISDA7bxz+WK5uVnaqsWesUV5lH8Q/FWk8eIfB7yoOtxpUnmD/AL4PI/M1s6V8VfCOqSiA6mLO5zgw3qGFgfx4pGiaex2lFRwzw3MKzQSpLEwyrxsGB+hFSUDCiiigAooooAKKKKACiiigAooooAKKKKACiiigD5kP/JY/FH+8/wD6EtdJXNn/AJLH4o/3n/8AQlrpK+jy3/d16s+Hz3/fH6IKKKK9A8YKKKKACiiigAooooAKKKKAOL+IdjaroyXa28a3HnqpkC4YjB4J79Kn0fTbK3sbeSK1iWRowS+3Jzj1o+In/Itp/wBfC/yarWnf8g22/wCuS/yrzXGP1mWnRHuRqT+oQV3u/wBC1RRVSTU7OK6e3luEjkQBiHOOtbuSW5yxjKXwq5boqp/amn/8/tv/AN/BViKaOeMSRSK6HoynIpKSezBwlHVofRRRVEkN3cC1tJbhhkRqWxUFnaKVW5uMS3DjJc87c9l9BVuSNJY2jkUMjDBB7iqEOmRCMLHd3LQdkEvy49M9f1rOSfNfc2g48jV7MbsSbXUlgAHkxsszr/ETjC++ME1p1Xja3tpo7ONQjMhdVA7AjP8AOrFOCtcmpK9u1tApCQAScY96WqEunyy2N1A93JI84I3OBhPoBTk2tkKKTersSPqNuGKRlppP7sS7vzPQfiag0x3ku9RaRDG3nL8hIJHyL6VZe4tbJVjZ0j44UDn8hTrWS2mV5rZkYO2XZe5Axz+Qqd5K7NNFB2i7Pr8yemvGkilZEVlPZhkU6itDAzbq5SxE5tYAzjDynOAOw/H2qYzSrqUUe7MUsRO3H3SO/wCtU7m3vAt7DHB5i3DbkcMBjpwc/Sr9tburmecqZiNoC9EHoP8AGsVzOVjqkoKN9/8Ahl+RZooqCe2MzAieaLHaNsZrVnMkm9SNbGNpXkuP3zFsqH5Cj2HT8at4wMCufv8AUrLTsiTV7guP4EKsf5VV02fxR4gnKaDZ3U0R+XzZkXaPfOAB+ZrlniadLR7noU8BXrq6287o6eWaKBC8sioo6ljgVgXnizT438q0ja8mPACLxn69/wAK6nS/gxe37rceJ9Ydu/2e3OT+LHgfgPxr0bRPB2geHkUadpsMbj/lqw3Of+BHmuSpj5y0grHoUcqpQ1qO78tEeMWPg7xp4sw32GLS7Jv+WkyhCR7D7x/Qe9d1oXwY0OwKzarLLqU45IY7Y8/Qcn869KorilJyd5O56UEoLlgrIr2dhaadbrBZWsNtCvRIUCgfgKsU13SNC8jKqKMlmOAK5+/8deGdPjlabWLVmjUkpHIGY47DHepCzZ0VFcNY/FzwheybDfPbn1miKj866zT9Y03VU32F9b3I6/upAxH4UDcWty7RRRQIKoajomlavH5eoada3S/9NYgxH0PUVfooA4pvhtYWcrT6Bqep6JMf+fS5bYfqpPIqeO4+JWif6q903XoF52XCeRKfbI4/lXXUUrItVJI5yH4s/YGEfifw1qulHgGZI/Pi9zuXt9M11Wj+NvDOvAf2ZrdnOx58vfscfVWww/Kq5UMpVgCD1BrA1TwP4b1glrvSbfzD/wAtIx5bD8VxS5TRVu6PRgQRkciivJU8F6xo53+G/F2pWgByLe7IuIj7c84/OrUfiv4haKNup6DY61CvBmsJTFIfcqcg/QAUrM0VSLPUKK8/s/jB4beVYNVS90acnGy+gKj/AL6GRXaafq2natD52nX1vdR4BzDIGx9cdKRZcooooAKKKKACiiigAooooA+ZD/yWPxR/vP8A+hLXSVxerWniJPGvibxBpVsLqOG/lgnRRk7Qc/d64wByK0dF8Y6fqpEMp+y3XQxyHgn2Ne7l2IpqmqbdmfI55gq0qzrxV42W3Q6OiiivWPnAooooAKKKKACiiigAooooA5L4if8AItp/18L/ACarWnf8g22/65L/ACqr8RP+RbT/AK+F/k1WtO/5Btt/1yX+Vee/95l6I9mP+4w/xP8AQtVnONPgv7meWRPNKJvV/wCEc4/OtGs2a1tbXUJNRnbc8gVUTbkgj09TVVOhFG12m3t066h5ct79yIW1uf4ig8xvoP4fx5q7b20VpAsMKBUHb+tV7S9N/BOYkaJ0YoPMGcEe1Gl3cl3aMZ1VZo5GikC9NwPalFxuvMqop8rT0S6F2iiitTnIbtQ9nMpk8oFCN/8Ad461l6dqFy1uIEsTJ5YCrLGdsTj1BP8AQGteaJZ4XicZRwVP0qoLnYPs9lAZvK+UndhVx2zWU17yd7HRTa5HG1/0IY4bxtahnnVNggdfkzhSSvBJrUqla30kt09rcW/kzKocYbcrLnGQatJKju6qwLIcMB2OM/1pwtbRk1eZtJrZdB9VtQuWtNPnnUZZFyM1ZqgPtd6JFYrbw7mTG3c7AHGeeAD9DTm9LLcmmle72Q+JbWxtzLJKmSMvMx5Y+tQaRLDcyXlzEf8AWSDK4IxhRjPuRz+NS2ukWVoBsi3Ed3O7+fSrioqliqgFjk4HXtUxjLS/QuU4Wkldt9f+AOqvPdCBgvkTyZGcxpuAqdmCqWYgAdSTWLf+KtMssqshnkH8MXP69KdScYK8nYVGlOpK0I3L39pL/wA+t3/34NRTa5Z22PtHnQgnGZImA/lVSws/Gfisj+y9NNnat/y3l+UY+p/oK7DRvgnaB1ufEWpTX03UxREqn4seT+lcFTH2+DU9allSetXTyTuzh5fFguJhbaRZT3s7HC7UPP0HWtjT/h3418SYk1SddKtG58sn5yP90f1P4V7NpWhaXokIi02wgtlxgmNACfqeprRrkqYirU+JnoUcLQo/BHXu9WcLoPwm8M6MVkntjqNwOd918y5/3en55rzfx/4t8ZaXrVzpu6TSrFGK262q7A8fYhx7ehFfQVUtT0mw1m0a11G0iuYW/hkXOPp6VztHVGet3qfKVhfeIdR1OKKyvtQmvZWxHsnfeT9c17Z4L0z4l2c0R1e9t2s8jfFdyebLjvgr3+pqHV/grZeeLzw7qU+nXKncqOSyg+xHzD9a5ZPil4l8J6g+mX89jrKQHaZFY5+m8d/qDS23NW+de6e+0Ag9Dmvl/wARfE3xJ4iZka7+x22eIbYlR+J6msjTPEfiO1uUTTtTv/OY4VEkZix9Md6fMT7F2Po/x74YufFfhp9PtLs284cSLkkK5APytjtz+gr5s1vwzrPh66aDU7CWEjo+Mo3uGHBr6J8AXnjC7sWbxPbQxptHkuRtlY/7SjjH5GuumghuYminiSWNuquoIP4Ghq5MZuGh8z+APCGkeKZZxqWtJZNERsgBAeQeoJ4xXocnwr8J6avnDxFcWci8rL9pVSp9a6XVfhX4T1Usx0/7NIf47Zyn6dP0rkr74DWzktZa7MvotxCH/UEfypWK503vY09J8V6N4VldL/x9/a1vjCxtEZnB/wB9Qf1rSX4w+DWYA306j1Ns/wDQVwx+A2p9tZtPxjarFl8GdFS58jUfFUbzg4aCDYjA+nJJ/SnqDUO56NZfEXwjqDBYNdtQx6CXMX/oYFdDBdW90ge3nilU8go4b+VcNB8HPB8UW17W4mbH33uGz+mBWPr/AMK9K0bS7jUNJ1y70qSFS4Mk/wC7OBnHY/qfpRqRaL2Z6vRXzNovxZ8VaRtR7tL2EfwXS7v/AB4YP616z4S+LOjeI5IrS6U6ffPwEkbKOf8AZb/GhNBKnJHoFFFFMgKKK5/xD4z0fw5iK6nMt43+rtIBvlc9hgdPxoBK5tXNpbXkRiureKeM9UlQMD+BryvxVZ+B9OvvJ0m3uRr2f3cOiyMjK3YnHyr/ADrQl/4Szxj/AMfkp0DST/y7wHNxKP8Aab+GtzR/D+maDB5Wn2qRk/ekPLv7ljyadrg6ih1M/wCE+reLk8XXeheJNQluIl0/7VHFM4keM+YoGX6k4J7mvZK8p8J/8lov/wDsCD/0alerVm1ZnXTk5RTYUUUUiwooooAKKKKAPHfBX/Ib8Yf9hmWneKfh1oniYNM0ItL4/wDLxAACx/2h0P1603wV/wAhvxh/2GZa6/enmGPcu8DJXPOPXFarY4ajam2jwm8s/FvgF8XsR1HSgcLOhLBR9eq/Q8VuaR4i07WowbaYCX+KF+GH+P4V606LIhR1DKwwVYZBFeeeJvhNp2pyNe6LL/Zl9nIC/wCrY/Qcr9R+VdlDG1aOj1R5uKy7D4nX4Zd1t80JRXFNrWv+ErlbLxNYu0ROEuV5z+PRv511Wn6nZ6pAJrOdZV74PI+o7V7NDFU63wvXsfN4vL6+FfvrTuti3RRRXScQUUUUAFFFFAHJfET/AJFtP+vhf5NVrTv+Qbbf9cl/lVX4if8AItp/18L/ACarWnf8g22/65L/ACrz3/vMvRHsx/3GH+J/oWqyYpo28Q3S3DBXiRBAGOPlIyxH48fhWtWZqN3pSkLd+VLIDgIF3tn04qqmyd9iaGrcbN3XQp6deCNr2KBTLcNcsVVegHqT2Fa1jbC1tgm7c5Yu7erE5NUWk1AQY07TooF7eawB/wC+R/U1JoTq2nEZk8xZXEokxkPnJHHbms6btJJm1dXg5Luut3/wDToooroOIrah539n3H2cEzeWdmOuapWWrWCWkcUBdpEXBhSMlwe4I/xrSni8+CSIsV3qVyOopttbRWsKxRKAAMZxyfc1m4y5ro2jOCp8slrczrePUZrmW5eKO3ZwFG87iqjoMDjv61bsLOS0e5eSbzWmkD5xj+ED+lXKZLNFBGZJpFjQdSxwKFBR1bCVWU9Et/69RzBihCkBscE1S8nUv+fuH/v1/wDXrLvPF9lE/lWccl3MThVQcE1dsPCvjrxVhvJXSrN/4pcocfT7xrnq4ulHrd+R24fL8RLVpJef9XIb3UG09c3Oq26H+6IssfwBrMtdc1zVrs2+jWUt8x4BWA8e/B4/GvT9C+DGhaewn1SabVLjqfM+SPP+6OT+Jr0GzsbTTrcQWdtFbxDokaBR+lcE8XUl8Oh6tPA0YL3lzP0SR4zp3wm8R62yy+I9UFpEefs8Tb2H5fKP1r0TQPh14Z8PbHt9OSe4XkT3I8xgfUZ4H4Cuqormbbd3qdadlyx0XkAAAwBgVl6/b6xc6aV0S9htLwHIaaPerD09vrWpRSA8on8eeNfCsmzxJ4dW5gBx9ptc7T+IyPzxXRaH8VPC2tbY2vfsVwePKuhs59m6frXaMqupVgCp4II4NeZfE3wPbXWjvd6N4ehmvy3zvC2xlHqFHDGlqi04y0aPRZtQs7e0N1NdQx24GTK0gC4+tefa18avD+nXBhsIZtRKnDSR/In4E9fyrwG4kvYk+xXL3CLGc+RISAp/3T0qvg4zjgUuY1VFdT6K0n40eGb91juxcWDtxmVNyD8R/hWhqvw+8I+L4xqEUUatL832mycAP7nHB/nXj3gPwbofiOVX1TX4bc54s0O2R/8AgTcD8M19D6Lomn+H9MjsNMgENuhJAznJPUk9zTWu5E7RfunmQ+A+n/agx1i4MGfu+WN351avvgrZRSLc6Bq15p90n3GLZwfXIwRXqdFOyJ9pLueR/aPin4T/ANdDHrtmv8S/O+Pww36GtDTPjPpLyC31uxutMnBwxZC6g/zH5GvTKztT0HStZjKajp9vcgjGZEBP59aLBzJ7oTTNf0jWYhJpuo21yvpHICR9R1FaVeZap8F9IkkNxot/d6XcDldrb0/oR+dczqus+Ovhs8SXer2eo27H5I5W3sR9OGApX7hyp/Cz3Oua1/wL4c8SSPLe2SLdt1uITsk/Ejr+NeOa98aNe1W0W3soYtNBXEkkTFnY+xP3R+vvXCrrmrJP566ndiXOd3nNnP50OSLjSlvc9f1P4Qa3agnQPElxsH3YZpXTH4qf6Vweu+CPHVtltRsr+7Rf+WiSmcY/Akj8a0PC3xJ8aR38drbs+rluPs8qFyR7EcivoawmuLjT7ea7tvs1w8YaSHdu2NjkZ70rJjcpQ3PlTRvBuv6/cSwafpzvJEAziRljwP8AgRGfwrsdH+CfiK4nRtQmt7GIMCcPvf8ADHH619B1S1TV9P0Wza71G7itoV/idsZ9gO9PlRLqyexYtofs9rDBvZ/LRU3sclsDGT71na74m0jw5bedqd4kRP3Ix80jn0VRya5Cfxd4g8Ukw+F7L7DYnhtTvF5I/wCmaf1P6VPpHg3T9Ouft128mpak3LXd0dzZ/wBkdFFUlcyk1Hcqzax4r8X/AC6dE+gaU3/LxKM3Eg/2R/D9a0tD8KaXoWZIITLdvzJdTnfK57/MelbdFUlYxlUb06BRRRTMzK8J/wDJaL//ALAg/wDRqV6tXlPhP/ktF/8A9gQf+jUr1asJbnqUfgQUUUUjQKKKKACiiigDx3wV/wAhvxh/2GZauKc/EuQdhpKn/wAimqfgr/kN+MP+wzLUOtvdxeLNXmsH2XcWhLJEcZ+YSscY98YrRbHFP42dvRWJZ+J7CcaPFJJi51SDzokUZ6KCc+nf8q26oyaaK97Y2uo2r217bxXEDjDRyqGB/OvL9f8AhNPZ3Daj4Ru3t5hz9ld8A+yt/Q16xRR1uhp6W6HhFn4wudOuzp/iWzks7heDIUIH1I/qK62C4huYVlglSSNhkMhyDXb634e0vxDaG21O0Sdf4WIwy/Q9RXlWrfDrxB4Ume98MXb3lp95rZ/vgemOjfUYNejQzGcNKmq/E8nFZPSq+9R919un/AOiorltI8bWl3L9l1GM2N2p2sr8Ln8en0NdQCGAIIIPQivXpVoVVzQdz5yvhquHly1Y2YtFFFamByXxE/5FtP8Ar4X+TVa07/kG23/XJf5VV+In/Itp/wBfC/yarWnf8g22/wCuS/yrz3/vMvRHsx/3GH+J/oRz2Ul1fbpZWNoI8eUrFctnqcdRiqVu9rDrlxBIIoBAq/Z0wFBBGSw9TnituopbaCcgywxyEdNyg4pyp63W5MK1k4y2tbQgkv1fMdniebp8v3V9yen4daksrUWdv5e7c7MXdv7zE5JqZEVF2ooUegGKdVqOt2Q5q3LHYKbIpeNlVyhIwGHUVDdXttZR77mdIx/tHrWDL4s+0T/ZdIsZr2dvu4U4/IcmoqVqdP4maUMLWrP93G/5Gv8A2fL/ABald/gVH9Ky7++03T8ibV7t5B/yzjlyf0HFa+n/AA68Z+JCH1W6TS7U9UPLY/3Qf5mu80H4TeGdE2ySwNqFwOfMuTkZ9lHA/WvOqYxbQX3ns0cua1qz+SS/M8gsofEfiSYJoFhqLoDzNJKdo+pOFFdtpXwYvL2RbjxPq7yN1MEBzj23Hp+Ar2COKOGNY4kVEUYCqMAfhT645TlP4mejCMKfwK35mHofhDQfDqAabpsEUmMGYrukP/Ajz+HStyiioG3cKKKKACiiigDmvGPjXTvBljDPepJLLOxWGGPq2Opz2AyPzrzWf49XXmN9n0SHy+3mTHP6Cu7+JPgtvGOhxrbMFv7Ri8Bbo2Ryp+uB+VfNd/YXWmXstnewPBcRHDo4wRUts2pxi1qetQfHq4z/AKRocRH/AEzmP9RW5YfHPQpyBe2F5bE91xIP6Vi/CPw14T1vR5Zb23ju9Tjc+ZFMchV7EL6e9eiXHw58I3Iw+h2yn1QFT+lNXFLkTtYqQ+J/AXiwLFLcaZcv2jvIgrZ9t4/lXQWuh6JDYtbWumWC2sn3o44E2P8AUYwa4rUvgp4YvATaPd2T9vLk3r+TZ/mK52T4c+N/Cz+d4b11rmJeRFuKHHptJKn86NRWi9mdTrnwf8N6pukso302c8gwH5M/7p6fhiuXPhr4k+Cvm0XUG1SxTkQbt2B/uN/7KaLP4v69oN2LHxXop3DgyIvlv9cHhvwxXpHh/wAb6B4lVRp9+hmP/LCT5XH4Hr+FGjG+eO+qOF0z40G2mFr4m0eezmBwzxqePqrYNehaN4s0LX4w2m6nbzkjmPdtcfVTg1a1PRNM1mExajYwXK9P3iAkfQ9a881j4JaXPIbjRL+fTpwcqp+dAfY5BH5mjUn3H5HqVc9441HUNH8I32o6ZJFHcWyiTMq5BXPI+teYyaX8VPCYIs7x9QtxwNjCYf8AfLc1xXirxP4x1SL7Nrz3UUORmIw+UhPuABmhsqNO73Op0z456xAQNR0+2uV7tHmM/wBRXRMfBHxakB3y2WtCPAB4fA/RgPzrweuo+H+lanqHjLS5NPikxBcxySyqPlRAwLZP0zx3qbmsoJarQ63U/gZrUBLadf2t0vZZMxt/UVLoHwP1Ga4D67dRW8APMcDb3b8eg/Wvd6bJIkUbSSOqIoyzMcAD1JquVGPtZGXoXhrSPDdr9n0uyjgB+84GXf8A3m6mr93eW1hbPc3dxHBAgy0kjBVA+prjNS+Iiz3L6f4WsW1e8Bw0oO2CI+rN3+g/Os+LwhdavcpfeLdQbUZgdy2ifLbxewXvTXkZyaWsmWbvx7f65K1p4OsDcKDh9RuVKQp/ug8tUdh4Lie8GpeIbuTWNR6hrjmKP2VOgFdPDDFbxLFDGscajCqowBT6pRMpVW9FoIAFAAAAHQClooqjIKKKKACiiigDK8J/8lov/wDsCD/0alerV5T4T/5LRf8A/YEH/o1K9WrCW56lH4EFFFFI0CiiigAooooA8d8Ff8hvxh/2GZatxgN8S7wEAj+yIgQfeV6qeCv+Q34w/wCwzLUXiO8n8P6vrWvNGREukxxQuejS73wP/Hga0WxxT1m0YHgKylj1TV9SuGWSHRY5LCz5yAAxYn8sD8TTPDV54m0y70zXtU1F7nTdbm2PA7E+QXP7sjPTPA4qTw3ps/h7TdY0eZ28660pb75jzvIIf8iVFdfpek2useCNHtp9wjSGCVChwQy4INCQ5PVnS0UVj+JPE2neFtOW91FnCM4RVRcsx9qoxSvojYorO0XXNP8AEGnJfadOJYW4PYqfQjsa0aAasc34m8DaJ4piJvLYR3WPluogFcfX1H1ry/UPD3i3wExkg3appCnOVBOwe46r+HFe6UVUZSg+aLsxSUakeSorrszx3RfFem6yAiSeTcd4ZDg/h61uVc8UfC7R9eLXNn/xLr/qJYV+Rj/tL/UYrz+5uPE/gaYW+uWrXdjnC3KHIx7N/Q16lDMulZfM8PFZJf3sM/k/0ZP8RP8AkW0/6+F/k1WtO/5Btt/1yX+VYvjDWrDWPCqPZzqxFwhZDwy8N1FXY9XsdP0u2+03CKwiX5Qct09K0dSHt5SvpZGao1Fg4U+V35np9xZeDUWdit5EiZ4AiyQPzpjWt4qlpNUKgdSIlH86yo/EGp61Obbw/pM1zJnG8qSB+A4H4muj034SeIdbZZvEeqi0hJyYIvnbHp/dH6/Suepi6Ufhu/mzro5dXlrUtFeibOXvtbtrQlBrFzcSdNkKpj88VLpGi+NvEj79Nt7qC1cY8+6YKuPUEjn8Aa9m0H4d+GvDwVrbT0mnH/La4+dv14H4Cuq6DAriniKk+tj06eFo01td+aX5HlOjfBSzWQXHiDUZr+bqY0JVc+5PJ/SvRtL0PStEtxBpmn29qnfykAJ+p6k/WuN8ZfFfTvC95Lp1vayXmoR8MpOxEOO56n8K5Xw/8c5vtZj1+xj8h2+WW1BBjHoVPUfr9a57q518s2j2yiqGk63puu2gutNu4riI9Sh5X2I7VfpmYUUUUAFFFFAHI/EPxi/g3QY7uCATXM8vlRBvug4JJP5V4jd/FjxjdSl11QW6/wByGFAB+YJr3rxr4Wh8X+HZdOdxHMGEkEhH3HGcfhyR+NfL+s6NfaBqcun6jA0U8Z6How7EHuKmVzekoteZ0UHxR8aRycazJJn+F4kP/stbtl8afFFoR9ttba5T/ajKH8xW18Ev7Ant7u3nggbVw+4GVQS0eP4c+nOa9gl06xnXbNZ28i+jxKf6UJMJyinax5lpXxz0i4ZU1OwuLQnq8ZEi/lwa3NQt/A/xJtQq3lrNchcRyxtsnT8Dg49iK1NS+H3hbVUIuNHt1b+/ENjD8RXC6z8DYQxuPD+qSQSrysVxyM+zjkfkaepC5Omhy+r/AA48V+C78anokktzFEdyz2v+sUf7S9SPpkV1Hhr42QsUtPEtq1vKPla5iUkZ9WXqPwrnz4n+IHw7nSDVUa5tAcL9o+dGHs45FdBba/8AD74hYi1ixTTtSk43MdhJ9nGAfxpehb1XvK56jputaZrEIl06/t7pD3ikBx9R2q/Xiuo/BXULCf7X4Z1s56qkpKOPo68H8hWVLq3xT8KNi4F1PEv8TxidSPqM07kcifws9w1XRdN1u0a11KzhuYm7SKCR7g9QfcV4D8Qfh1P4NkXVNNmkfTmkwrZw8LdgT3+tXI/jh4mgYrNY6e5HBDRup/Rq57xV8SNd8W2gtLwwQ2oYMYYEIBI6ZJJNJtMuEJxZveEPjDqukyR2uts9/ZdPMP8ArUH1/i/GvddH1rT9e09L7TblLiB+6nkH0I6g+xr49ru/hPrl/pvjWzs7cu9tet5c0Q6Yx978P5UJjqU01dH0tTJIYplKyxo6nghlBFPoqjnMx/DmhyPufRtPZvU2qE/yq9Db29rFsghjhjHZFCgflXO+IPHWkaBL9l3Pe6i3CWdqN7k+/p+Nc3LZeJ/GB361dHSNMbkafaN+8cejv/h+lA3oryZta38QtPsro6dpEMmsap08i15VD/tv0H+elYjeHtb8TyLP4s1ArbZ3LpdoxWIf75H3jXRaVounaJai3061jgTvtHLfU9TV+qUe5lKr/KV7OxtNOtlt7O3ighUYCRqFFWKKKoxCiiigAooooAKKKKACimySJFG0kjqiKMszHAArll1zVvFV6+meDbUShTtm1SYYgh9cf3jSbSLhCU3ZGt4SP/F6NQ/7Ag/9GpXq1cl4N8BWXhNpr17ma/1e5TbcXsx5YZztUfwrnHHtXW1i3dnpwjyxSCiiikUFFFFABRRRQB5JrHh7X/BOs6lrekQHVtHvpzc3dqo/fwserL/eHtWnpWsaP4q00yWzxXMLcSwyKCUPoynpXpFcH4o+G0Go3raz4fuv7H1wc+bGP3U3tIvf6/zqlKxjUpKWq3MzVtEmvNfsNQhZAiQzW1yp6tG44x9GANcdZeM/7F0ay8OxkDXLa9SxNu6k7o9+A2fTbjmuj07xbPaaiui+KrP+y9U6I5P7m490bp+FbE3h7SbjWotYksomv4hhJsc1e+xz/DpJGpWJr3hyy12602e+bMdlMZRE4BSQ4xgg1X8Om+XW/EMV1MzxLdq0ClshFKA4HpXPfEPTrrxD4g0HQIr57OGcSyvIozyoGOMjPX1oexMV71rljR7CDw58TrnT7CMQ2Oo2H2nyUGEWRXAyB24Jrf8ACOuTeINCF9cRpHIJpYiE6HaxGf0rhvDfhu78MfEu2tLrV5NR3abK6O6kFBuAxyTXSfDfjwUW/wCnq5P/AJEaki5pWv6F3xxrc2keCb7UtPlXztqrFIuDgswUEfnUPgC78Q3WhyDxJEyXUUm1HZQDIhUEHjg9eorzK/bVk+EWjTW5D6cHxdRk8k+YCmPxGOPWvXfDHiC317w7baikbWyNmMpKQCrKdpH5ihO7CUeWPzNuo54IbmF4Z4klicYZHUMrD0INSVnX2tWmn6jYWM5fzr52SLaMjIGTn0qjJHn3ij4N2N8XudBlFnMeTbvkxn6d1/lWB4V8M+GNI1EWXja1ubfUN37s3LYtZPTDD+pxXuAIYAggg9CKq6jpllq1o1rf20dxC3VXXP5elS4mqqu1mXrK0s7O2SKxt4IIAPlWBAq49gOKsV51/wAI94g8IMZ/C94b2wBy2lXjZwP+mb9vp/OtzQPHema1cfYbhZNO1ReHsrr5Wz/snowoC19UdTRRRQI5Pxb8PdE8XfvrmMwXoGBcw8MR6MO9cFF8BT9q/e64Db56LD8/88V7TRRZFKcloj511fwJ4t8AXh1LRriea3T/AJb2udwH+2np+YrqPCvxsik2WviWHyn6faoV+X6svUfhXsXWuF8V/CzQ/Em+eFPsF8efOhX5WP8AtL3/AEpWtsXzqWkij8SvHsmkeGbOfw/dRSNfuyrcxkOEUDJx78j9a8Gu9d1e/laS71O8ndupkmY/1rZ8UeB/EHhUFL2F5LLdlZ4iWjJ9fY/WuWqWzaEUloaljq2upKBYX+oLIOnkTPn9DXTWfxE8d6M4Wa6uZVH8F5Du/UjP616J8EbzSpfDs1rDHGmpRSFpjgb3U9Dn07V6jJGkq7ZEV19GGRTSM5zSdmjxnR/jsQRHrOlfWS2b/wBlP+NdVcXngb4m2AtnuoGucfu9/wC7niPtnr+GRW1q3gHwxrQJu9JgDn/lpEPLb8xXm/iD4HTRM1z4dv8AfjkW9xww+jj+oH1p6kpwe2hzHiH4c+JPBl4NR08y3FtE26O6ts74/wDeA5H16V2PhL41ROI7PxLF5Tj5ftca5U+7L1H4Vy1j468Z+BLwafq0Uk8K8eReZOR/sv8A/rrp4Lf4ffEv7iHSdYk6opCMW9v4W/nS9C5ar3vvPWrDU7HVLcT2F5BcxHo0Thh+lWq+f774W+MPC9y11oN41yg5D2zmOTHupPP5mq0PxS8b+Hpxb6mglK9UvICCfxGDTv3M/Z3+Fn0HdWtve27291BHNC4w0cihgR9DXgPxN+Gy+GwdY0rJ053w8R5MJPTB7rWnB8e7xR/pGgQSf9c7gp/NTXOeMfipqfizT204WkNlZsQXRWLs2OmWOOPwpNplQhOLGeDfifrHhiSO2uJHvdNBwYZGyyD/AGD2+nSvoTQte03xJpiX2m3CzQtww/iQ+jDsa+Qa7X4X+ILvRfGljBEzNb30q280fY7jgH8D/WhMupTTV0fRd/oGj6ou2/0uzufeWFWI+hI4rn7n4WeDbnJOjJGT3ildf0ziuxoqjnUmtjg1+D3g9etnO31naui0TwloPh3LaVpsMEhGDLgs5H+8cmp9a8QaX4ftDc6neR26fwhj8zfQdTXFzeIvE/i3Meh2x0bTG4N9crmZx6onb/PSgbba1eh1fiDxdo3hqIG/uh57f6u2i+eVz7KP5niuRlu/F3jDgF/D2kv2B/0mRfr/AAfoa0NF8IaZo0pudr3d8/L3dyd8jH69vwrfqlHuZOql8JkaJ4Z0rQIitjbKJW+/O/zSP9WPNa9FFUYttu7CiiigQUUUUAFFFFABRRTJZY4InlldY40GWZjgAe5oAfWNrvifT9BRUmdpruTiG0hG6WQ9gAP51mx6xrPi+7fT/B1sDCp2z6rOCIYv93+8a73wl8PNK8Lubx2fUNXk5lv7nlye+0fwj2H51Dn2Oqlh29ZHJaX4D1zxjIl54vd7DTM7o9IhfDOO3msP5fyr1Ow0+z0uyis7C2itraIbUiiUKqj6CrNFZN3O2MVFWQUUUUDCiiigAooooAKKKKACiiigDM13w9pXiXTXsNWs47mBuRuHzIfVT1B9xXmN7pniX4dEson13w0v8Q+a5tV9/wC8o/zivYaKadiZRUlZnmPhmbTb2G71LTb/AO2JezeaxzyhwBtx1GMdDWf440/UdthrmkQeffaZIZPJHWWMjDKK2/EXw1IvX1vwhcrpWq9ZIcf6Pc+zL2PuP/r1k6R4v8zUP7G160bSdaXgwSn5JfeNu4NWmnoc06coPmWpyHhvWNR8QfE+LUL3TZbCJ9OkjgjlBBIBGTz710Xw8cJ4FlyceXcXO72+djXVTabaz6lbag8f+lW6ssbg9AwwR7ivLtUvtb8Fajq+iWelve2msSNJZSqSPLeQYYHg5x6cdM0bE359ERAf8WM08etzF/6OFafjnRpPEHiLQNAjuTZW00Ms7Mg+84x27n/Gs0jHwP0setzD/wCjq6j4g6TqEum2OuaRn+0dKbzVAGSyY+YY79OlBV7S+bDwNe6lYajfeFNZuDcXNiiy28x6yQngfkSPzqTVf9M+Kej2/VbOxluD7FjtH8jUnhS80rxZPB4qtt0WoLbm1uIg3A5BwR9QCDUekf6b8TfEd11W0t4LVT6ZG4/qTTIe7ZH8K5ZJfCsxkkZ9t5KF3HOBnoK7ivHvAXjvQ/D2krpt/M6zTXkrEquVQFuCxr1+ORJYlkjYOjDcrKcgihbCqJqQ6sjXfDGk+IoPL1G1V3X7ky/LIh9Qw5qt4W8Tf8JKNSdbbyEtLprdctktjufSugp7k6xZwqSeLfBfeTxFo69j/wAfMK/+ziur0DxVpHiWDfp10rSr/rIH+WWM+hU8/j0q/XNa74J03WZxewmSw1NeUvLU7XB9/wC9SsWpp7nYUV57H4o8Q+EWEHii0N/p44XVLNeVH/TRP6j9a7bTNVsNZs1u9OuoriBujRtnHsfQ0htFyiiigQySKOaNo5UV0YYZWGQR9K8z8WfBvS9V8y60Rl0+6PPlY/dMfp/D+HFen0UWGpNbHylcaf4m+H+tx3EkU1lcxn5Jl5SQegPQg+lexeDfi9pmtCOz1gpYXx4DscRSH6/wn616FfWFpqdq9re28dxA/VJFyK8j8WfBNH8y78Nz7G6mzmPB/wB1u30P50rNbGvNGfxHsisrqGRgynoQcg0tfL2n+KPF3gK9NmzzwhOtrdKWQj2B/pXfaT8eIHCprGkPG3eW1fcP++W6fmaOYl0mtj1LWNC0zX7JrTU7OK4iPTcOVPqD1B+lfOnj7wJdeC9SWaB2k06Zv3Ew4ZT12n3969bHxm8ImLcZ7oNj7n2c5/wrzX4jfEuLxfbRadYWjw2ccnmGSUje5HTgdBQ7FU1JPyNDwL8XrrTnj0/xFI9zaHCpcnmSP6/3h+te3Pb6ZrdkjyQ2t7ayqGUuiyKwPfmvjuvXPgt4tuIdTPhy4cvbTKz2+T/q2HJA9jzSTKqU+qO/1P4T+EdSJYacbRz/ABWrlP05H6Vzl18CNKfJtdWuovQOit/hXrNFVZGKnJdTxxfgLb/x65L+EI/xrrfCvwv0Lwvdpex+Zd3qfcmmx8nuAOh967K4uIbWB57iVIokGWd2wAPrXC33xCn1Od7Hwhp51CUHa17LlbeP3z/FSsh80mtztNQ1Ky0q0e6v7qK2gQZLysAP/r1wtz411nxG7W/hGwMdrnadUvF2p9UU9ajtPBZvLtdQ8T3z6vejlUfiGI/7KV1aIsaKiKFVRgKBgAVSRjKoltqc3pfgu0trv+0dVnk1bUzybi6O4Kf9legrpgMDAooq0rGMpOTuworlNLPiAeMG/ta5iFtLbTNBaw9ECvGASe5IauroQSVgooooEFFFFABRRRQAUVHNPFbQvNPIscSDLO5wAK5iHVNb8Z3T2HhC3EdoG2zavcKRGnrsH8R/z70m0i4U5TdkaGu+KLDQ9kL77i+l4hs4BvlkP0HT607Svh/rPiyWO/8AGcjWun5Dx6NA+Mjt5rDr9B+ldd4S+H2k+FN1ype+1ST/AF1/c8yMfb+6PYV1lZOTZ306EYa9SCzsrXTrSO0sreK3t4xtSOJQqqPYCp6KKk2CiiigAooooAKKKKACiiigAooooAKKKKACiiigArF8SeFNH8V2BtNWtFlA5jlXiSI+qt1BraooA8cul8SfDtguq+drXh4HC38a5mtx28wdx7109hqFjq9nHeWU8VxA4yroc/8A6jXdsquhR1DKwwQRkEV5trvw3udOvZNZ8EXCWV0x3TadJ/x73H0H8J/T6VSl3MKlFPWJkeJ/CxbwbFpGiW4CQ3McqRF+ih9xAJpusX9zpXxA0MyXDpp97A9s8Zc7PMHK5HTPOKvaF4vg1O7bTNQt5NM1iPiSzuOCfdT/ABCrHirw1b+KdGexlkMMqkPBOo5jcdDV+hz3adpHLWFhH4W+LX2Wy/d2WsWrytCOiyKScgfgfzrR8Af6SniDVD/y96nLtPqq4A/rXO6D4Y8TaXrd1r3ia7WddPspEt38zeW46j0GM9fWus+HlubfwFpxYYaZHnPvvYt/Iikip7b9jiPhz4I0jXPD+pXmp2qTyXE7xRuesYHdfQ5rZ8J6vqGkeE9d0wxm6vdBleOJOSZE6qOOfX8MVf8AhM4bwVgYyLqbP/fVRaI3kfF/xNAOFltoZMD12rk/zoXQcndyTMn4Qa7ZTrqlnJMkV/c3b3CW7HkqRk49cc16pXlfwy0CxudS1HW3Rhe2uozojBuCrAggj8axtN+LdzoluLS8ia/kW9lEjM+GSEY2gepzu6+lCdlqE4c0nynp/ifxdpfhK3gm1JpP37lUSJdzHHU/QcfnWhpOsWGuafHfadcJPA/8S9QfQjsfavKvGt3pXjbxT4Ws7a6EtrMxWXYcMuSMg+hxXo3hXwta+E9PnsbOWSSGWdpl8zquQBjPfp+tNPUiUUorubjKrqVYBlPBBHBrj9R8CrBeNqfhi8fR9QPLLF/qZfZk6V2NFOxKk1scfZePbjSrlLDxjYnTpmO1L2MFraX8f4fxruIZoriFZYZEkjcZV0YEEexFULuztr+2e3u4I5oXGGSRcg1xz+EtX8NTNd+D7/bFnc+l3RLQv/un+H/PNTYtNPyPQ6K5DRfiBY312NN1a3k0fVBwbe5OFc/7D9DXX0DaaCiiigRz/jLTLDUPDd497pK6iYYmeOID5yQP4SOQfpXyjLjzX2oUG44UnJX2r7OrhPFXwq0LxJI9zFu0+9bkywqCrH1Zeh/Sk1c1pzUdGfNNaWk6DqWuytFpluLiVf8AlmJUDn6KSCfwr0hfgNqv2sK+s2Qts8uEYvj/AHen616X4V+HmheFFSS3g+0XoHN1MMtn2HQfhUqJpKqktDwq3+FvjK4cKNFkjH96SRFA/WvU/h38LW8M3q6tqsyS36qRHHEcrHkYJz3NenVyWvfEDS9JuDYWaSapqh4W0tfmIP8AtN0UVVkjJ1JS0OsZlRSzMFUckk4AritW+IlsLptN8OWr61qI4Pk/6mM/7T9PyrJfRfEPixvN8TX32SxJyumWbYBH+2/f6fyrptO0yy0m1W2sbaOCFf4UGM/X1qkmzGU4x8zml8K6l4gnW78X6g10AdyafASkCfUD71dXbW0FnAkFtDHDEgwqRqFAH0FS0VSVjGU3LcKKKKZIUVzniXxjaeHXjg+zT3t043mC3XLIndj6CtjTNQg1bTbe/tiTDOgdc9fofelcbi0rlSTnxdB/s2En6yJ/hWtWT18XD/ZsP5yf/WrWpg+gUUUUCCiiori4htIHnuJUiiQZZ3OABQBLWHrnimx0V0tgHu9RlOILK3G+SQnpwOlULfUNd8cXDWfhOH7PYA7ZtYuFOweojX+I/wCeOteheEvAOkeE1aaFWu9Sk5mv7j5pXPf6D2FRKfY6qWGb1kcjpHw81bxRNHqHjaUxWgIaLR4Hwo/66kdT7V6la2lvY2sdtaQRwQRqFSONQqqB2AFTUVle52qKirIKKKKBhRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQBz3inwZo/i60EeoQbbiPmC7iO2WE+ob+nSvPZ73xB4BmW38So+o6NnbFq8KElB2Eqjp9a9jpksMc8LwzRrJG42sjjIYehFNOxMoKSszhc2Ot6WwWSO6s7mMqSjZV1PuKktbSGwsIrO3XbDDGI0XOcADArH1f4eaj4buZNV8DygITun0eY/upPUxn+E+3/6iaB4tstcd7R0kstTh4msbgbZEPt6j3q1JM5J0pR9DhPhVqp0Z7rRtW/0Q3DtPbed8mSDh1578Zx9a0fCF5FrPxT8UalbsHt1iSFHU5B2gLkH32k10njPwXZeMNNWCZ/s9zEd0Nwq5K56gjuDSeCvBtv4O0qS2jnNxcTNvmmK7d3oAMnAFFmDlFpvqzG+FP/IP1v8A7Cctc98NPDGl63beIpNRtEn8y5aBSw5Uck7T2PI5roPhc8cY8RWe4ebFqcpKd8Z4P6Uz4Rf8gXVz/wBRKT+QoXQcm1zW8jjfGfhFvD3jHRl8MvIl7cjMQZhw64AwT6+9eo6V4hax8JWd/wCKpo7C7bckolGz5gxHT3AzxXO+M/8AkqHhD/eP86pfE/TjrnjDwxpE8zQ2tyXDOvXPHT37fjRsN+8kmemWV/aajbLcWVzDcQt0kicMD+IqxXjjaVffCbXrW9t7uS60G8kEMyvwUJ6Z7Z7g+xr2JGV0V1OVYZB9qaZlKNtVsLRRRTIM7WNB0zXrQ22pWkc6fwkjDKfVT1BrllsvFXgznSpn1zSF/wCXOdv38S+iN3+ld1RSaKUmjK8PeMtH8RgxW0xhvU/1tncDZKh7/Kev1FdBXK6/4P0rxARNPG0F4nMd3bnZKh+o6/jWKms+KfBhEesQNrmkr0vbdcTxj/bXv/nntS2NFaWx6JRWbo2v6Z4gtBc6ZeR3EfcKfmX6jqKh17xRpHhu383UrtI2P3Ih80j/AEUcmgVnexsVzviHxro3hzENxOZ75v8AV2duN8rHtwOn41zE2q+LPGPy2UbeH9Jb/ltIN1zKPYfw/wCeTWnonhXS9By9tCZLpuZLmY75HPckmmk2KUox3MqZPFnjD/kITNoWlN/y6wN+/kHozdvpW9o+gaZoNv5On2iRZ+8/V3PqWPJrSoqkrGMqjloFFFFMgKKZNNHbwvNM6pGilmZjgACsjTdftfEukXc+iXCmVN8SNIpAV8fKSPToaBpN6kmv+ItP8N2Iur+RgGO1I0GXc+wq5p+o22p6bBqFq+63mTere3v71xvgm1udWnn1DWiLqayd7OB3GQSGO9wPc4H0FaWnkaf4R1pIV2x2st75ar2AZ2A/WkmXKCWnUueHIEeC51icL5185cu3aIcIPpgZ/Gk8Jtb/AGG+itJUktYb6ZYjG2VCkhsA+xY1zenaDr3iewtU1iY6ZpEcSLHY27fPKoAA3t2FdvYafY6Lp4trSKO2togSQOAPUk/1pIc7K6uVU58XTf7Ngn6yP/hWtXAT+Ir7VfEt0nhWBLotbxwPeyZEMJVnJP8AtH5hXexh1iQSMGcAbiBjJppkzi1a46iobm6gsrd7i5mSKFBlnc4ArmrW71/x1O1r4XiNlpedsusXCnBHfyl/iP8AnjrQ2kEKcpvQu654qs9IlSziSS+1ObiGythvkY+4HQVZ0f4can4jnj1LxxLiAHfFo8D4jT08wj7x9q6/wn4E0fwjEz2sbT30v+uvZ/mlkPfnsPYV09ZOTZ306MYa9SK3toLS3S3toY4YUG1I41Cqo9AB0qWiipNgooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAK5fxZ4E0nxYiyzK9rqUX+ov7c7ZYz25HUexrqKKAPHG1rW/Bd0lj4xi8yzY7INZhT92x7CQD7prr4ZoriFJoJEkicZV0OQR7Guuu7S3v7WS1u4I54JBteORcqw9xXl+p+Bta8HTSah4Nc3enE7ptGmbp6mJu30/n0q1Luc9SgnrEof8IQ1n8QofEunzhIZd/wBrgJxklSMj15xxVL4TRSQ6RrEcsbRuNSkyrDBHC9q6bw/4q07xFG627NDdxcTWkw2yxn3H9a2VRVZmVQCxyxA6n3qrdTByduVnnXjL/kqPhD/eP86v/E3w9datokOoaarnUdNk8+LZ94gcnHvwD+FVvF9rcN8SPCd0sLm3RyjSBflBz0JrR1vxDfaT4+0TTy6f2bqKNGwZekgzjB98gUu5Sv7rRi6Zqtp8VfBlxpFzMttqabTKAM4IOQ4Hoeh9M16BptvLaaZa208gkliiVHcDhiBjNeV+O/Dtx4R1uLxloOUjEg+1QrwBk8n/AHT0PvXqmmX8WqaXa38H+quIlkX6EZpoU9rrYtUUUUzIKKKKACgjIwelFFAHAeN/DVnpmmXviTR3l0zVLaMyGS0bYJPZl6GpPDHhbT4be31e68y/1O4jWV7q6bewJGeM9K1viD/yIWs/9e5qXQ/+QBp//XvH/wCgihLUqcnybmhRTJporeJpZpFjjUZZnOAKxdI8WaZruqXNlpzSTfZ1DPOF/d5z0B7mqMUm1c2nljjKh3VSxwoJxk+gp9eeaHoN3qHj/UNR1W/a8TT3xAq5CI7cgAf7K4z7muz1vVodE0me/mVnEYwka9ZGPCqPcmkmVKNmktTQqtqE1xb6dczWkHn3CRs0UWcb2xwPzrz5tU8c6XNBrmqrbjS3dRNaJ96FGPU8ds+tekqwdQynIIyDQncJR5fM86tLvV9fJ8P60yfaZbstdRxfdit0VSV49SQPzrvLTTrOwaV7S2jhMu0ybBjdgYH6Vh+HNPiTxF4h1DrNLciLPoqqDj8zXSnoaEhzetkY3hVQNEyABuuJmOP+ujVX023N3oOs246zXV4g/F3FT+GZEi8NxyyMFQNK7Mew3tVLwRqseqWV+YIpBCl7MyTMMLKHkZgV+gIoB31ZBY+M9MtvCltcTTo15HGIDaKwMrSj5du3rnNaum6U8/h57XVt0st6Gkul3Ecv1UY6ADA/Ckh8I6HBrb6vHYRi8c7i55APqB0BrUu7y3sLV7m7mSGFBlnc4AoXmKTX2Qs7K2sLZLa0gjghQYVI1wBWPrfiq10u4SwtYpNQ1aXiKythucntnHQVUtJ/EPj6U2/hyNtO0gHEurXCHLj0iXv9f5V6P4U8D6P4RtyLKIy3cn+uvJjullPfJ/oKhz7HRTw7eszj9F+G2oa9cx6n45mEiqd0OkQt+5j/AN8j7xr1CCCK2gSCCJIokG1ERQAo9ABUlFZnYkkrIKKKKBhRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQByHi34fab4lkW/t3fTdai5iv7b5X+jD+IfWuMi8R6p4Yvo9J8aW4gLHbBqkY/0ef6n+E+oP8AKvYqq6jptlq9jJZahbR3NtIMPHIuQaadiJwUtzllZJUV1Kup5UjkH3Fcn8QvDlxr2grLYErqVi4uLYr1LDsPf096kv8Awlr/AICZrvw4ZNW0MHMmmSNmaAesbdx7f/rrU0HxJpviK1M1jNl14khcbZIz6MvatE0zklCVN3PKtZ+Kdvqvgm90nULGaLV5I/JdduEz3b1B9q9E+HQlX4f6MJgQ3kcZ/u7jt/TFSav4E8O65fC8vtPRpwcs6Erv/wB7HWughhjt4UhiQJGihVVRgADtQk76hKUXG0UPooopmQUUUUAFFFFAHNfEH/kQtZ/69zUuh/8AIA0//r3j/wDQRUXxB/5ELWf+vc1Lof8AyANP/wCveP8A9BFC3CfwL1M/xhoMGv6M0VxPNHFBumKxnG8hTgH2qtoMtloHw8tb5YY4kSyWZ9igF225/Ek/zrf1P/kFXn/XB/8A0E1wo1C0l07wfodzcRxRzQxXEodsBgijav4tj8qHowjdxt0Os8MafLYaJF9pH+lzkz3B/wBtuSPw6fhVXUYhqfi6ws3+aCyjN269t5O1M/T5j+FdFXneqTeI7rxrq1joMUcRaOBJb2XpCu3OB7/NTego3k2ze8Z69pGnaLc2d9OpmuYmSO3T5nYkcceme9bOjl20SxMisrmBNwYYIO0daxNA8Eafospvrl2v9Sbl7u45OfYHpW9fajaabYSX13OkdtGu5pCeMf1oXdila3LEzvD/APx960f+n9v/AEFav6rcz2el3FxbWr3U6JmOFOrt2FefaefEXiie+XS2bTNGurlpTeSLiWRSAMKO3TrXpFtALa1igDs4jQIGc5JwMZNCdxzVnqc/4Q0vVbPRJINceJzKxK26gFYkPJUnv1NdFFDHBEsUMaxxqMKiDAA9hUV7fWunWr3N5OkMKDLO5wK52zPiPx/IYtBRtL0QnEmqTp88g7+Uv9aTaQ4wlUeha1nxXb6fdJp1hBJqWry8R2VsNzZ9Wx90fWtDQ/hpeazdRat44nW4dTvh0qI/uIvTd/fP6fUV2HhXwVo3hC2aPToC1xJ/rrqU7pZT7t/SuhrNybO2nRjD1GRRRwRLFDGscaDCogwAPQCn0UVJsFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABXEeKvhzZ6zd/2vpE7aRrqcrdwDCye0i9GHv1rt6KAPILPxVe6TqKaN4xtBp183EN0P+Pe591boD7V1oIIBBBB6EV0Ws6JpviDTpLDVLSO5tn6q46H1B7H3rzC90HxH8PGM2n+drnhscm3Jzc2q/7P99R/n1q1Luc1Sh1iddRWbouu6dr9kLrTrlZY/wCIdGQ+hHY1pVZzNWCiiigQUUUUAc18Qf8AkQtZ/wCvc1Lof/IA0/8A694//QRUXxB/5ELWf+vc1Lof/IA0/wD694//AEEULcJ/AvUm1P8A5BV5/wBcH/8AQTXnHh7wdb+K/CX27U42S6kiWKykBIMKRrtUge5BP416Pqf/ACCbz/rg/wD6Cao+FAB4S0gD/n0i/wDQRTauxRk4x0K/gvUZ9Q8NQfayTd2zNbz567kOKqw3iaf8Rb20mIRdQtY5YiTgMyZUj64xVfT9Ts9B8W6zp13MsIupop7dT/GzjBA/Ff1rV8TeFbHxRbRR3TSRSwtuiniOHSl0G7KWuzKXiXWPtdzH4b0yUtf3fEzx8/Z4f4mJ7HHA+tbz6XZy2EVjPbpNbxhQqSDI+XpVDw54V07wzbulmrvNL/rZ5Tl3+prSv9QtNMtHur24SCFBku5xT9SW1tEsKoVQqgADoB2rntY8Vw2d4ul6ZbyaprMnCWdt8xU+rkfdHfntUFjH4k+IL7NHWTR9Czh9RmX97MPSNf6//qr0vwv4O0fwjZGDTbfEr8zXMnzSyn1ZqiU+x0U8M3rM4/Qvhnc6ndR6t44nW9nU7odNjP8Ao8H1H8R/zzXpscaRRrHGioijCqowAKdRWZ2JJKyCiiigYUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAcB4m+G0dzetrfhi4Gka31YoP3Nx7SJ0/GsLS/FssOpDRPE9odK1ccKH/1Vx6GNuhz6fhXrlZPiDw3pPijTmsdWtEniP3SeGQ+qnqDTTsZzpqe5iUVx95ZeJPhycz+drvhscCdRm5tR/tD+Ie/8q6PS9WsdasUvNPuUngfoynp7EdjWidzknTcNy7RRRTMzmviD/wAiFrP/AF7mpdD/AOQBp/8A17x/+gioviD/AMiFrP8A17mpdD/5AGn/APXvH/6CKFuE/gXqSaqypo96zMFAgfkn/ZNc54E8SWeqabbabaJK7WVnEJZiuEDYAKg9zWt4j8PReJLSC0ubmaK2SUSSJEceaAD8pPpzV/TtNs9Js0tLG3SCFOioMfifU09bk3jy26lefQNNutah1ee2WS8hTZG7chRknIHrz1rSqpqOpWek2b3d9cJBCvVnP6D1NYVja+JfiE2NOEmi+HycNfSrie4Xv5a9gfX/APVSbSKhTlU2JdW8VpBfLpOj2smq6xJwtrb87Pdz0UVsaB8Mpb67j1jxtOuoXindFYL/AMe0H4fxH6/rXYeGfCOj+ErH7NpVqEZv9bM3zSSn1Zu9blZuTZ3U6MYeoiIsaBEUKoGAAMAUtFFSahRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAhAYEEAg9Qa868Q/DaSC+k1vwZcLpmpN80tqf+Pa5+q/wk+o/nzXo1FAmr7nk+i+L0ur46RrVq+k61H962n4EnujdGFdPWr4n8I6R4tsRbapbhmTmKdPlkiPqrdq84uX8RfDyQRa2JNX0AHEepRLmWAekq+3r/APqq1Luc1Sh1iXfiD/yIWs/9e5qXQ/8AkAaf/wBe8f8A6CKo+M7+01L4b6rdWU8c8D2xKuhyDTrXVbHR/Clld39wkEK2ycsevyjgDuatbnPJPlS8zcrm9U8VBNQGj6HaPq2sNwIIOVj93booplhp/iX4hEG1EuheHj1uZBi4uB/sL/CD6/z6V6d4b8K6R4U08WmlWqxA8ySHl5D6s3U1Ln2NaWG6zOQ8PfDFp7yPWPGdwup6gvzRWg/49rf6L/Efr+tekKqooVVCqBgADAFLRWZ2JJKyCiiigYUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAU10SVGSRVZGGCrDIIp1FAHkvjD4RTSWt4/g27Fh9sUrc6e7fuJAe69dh+n6Ve8JfCmO1NrqPiu5/tXUYVUQwH/AI97fHQKvRiPU/8A169MooFZbiABQAAABwAKWiigYUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFAH/9k=)

![img](https://images2018.cnblogs.com/blog/799055/201803/799055-20180309154723871-127136242.png)

平时我们安装虚拟机的centos都需要好几个G，为什么Docker才需要200M？

![image-20200810130954729](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200810130954729.png)

对于一个精简的OS，rootfs可以很小，只需要包含最基本的命令、工具和程序即可，因为底层直接用kernel，自己只需要提供rootfs就可以了。由此可见对于不同的linux发行版，bootfs基本是一致的，rootfs会有差别，因此不同的发行版可以共用bootfs。

## 分层理解

> 分层的镜像

我们下载镜像的时候，注意观察镜像输出的日志，可以看出是一层层地下载。

**思考：为什么Docker采用分层下载这种方式呢？**

最大的一个好处就是 - 共享资源

比如：有多个镜像都从相同的 base 镜像构建而来，那么宿主机只需在磁盘上保存一份base镜像，同时内存中也只需加载一份 base 镜像，就可以为所有容器服务了。而且镜像的每一层都可以被共享。

**Docker镜像的特点**

Docker镜像都是只读的，当容器启动时，一个新的可写层被加载到镜像的顶部，通常这层被称为“容器层”，“容器层”之下的都叫“镜像层”。

## commit镜像

```shell
docker commit 提交容器成为一个副本

#命令和git原理类似
docker commit -m="提交的描述信息" -a="作者" 容器id 目标镜像名:[tag]
```

实战测试

```shell
#启动一个默认的tomcat
docker run -it -p 8080:8080 tomcat

#发现默认的tomcat总是没有webapps应用，镜像的原因，官方镜像默认webapps下面是没有文件的
#从xshell5重新打开一个终端
docker exec -it e185baa01c20 /bin/bash

#自己从webappsdist拷贝进去文件
cp -r webapps.dist/* webapps

#提交
docker commit -a="作者" -m="提交信息" 容器id tomcat02:1.0 
```

![image-20200810141245238](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200810141245238.png)

如果想要保存当前容器的状态，就可以通过commit来提交获得一个镜像，就好比学习VM时候的快照！