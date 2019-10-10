# 目录

- [什么是Docker]()
- [Docker的优点]()
- []()

## 1. 什么是Docker

Docker基于Google推出的Go语言进行开发实现，基于Linux内核的cgroup、namespace以及AUFS类的Union FS等技术对进程进行封装隔离，属于操作系统层面的虚拟化技术。

Docker是开发人员和系统管理员开发、部署和运行带有容器的应用程序的平台。容器化就是使用Linux的容器(container)来部署应用程序。

> Docker容器化(containerization)的优点：
> - 灵活flexible：即使最复杂的应用程序也可以被封装
> - 轻量级lightweight：容器共享主机内核(host kernel)，运行一个独立的进程
> - 可互换interchangeable：可以随时部署更新和升级
> - 可移植性portable：可以本地构建、部署到云
> - 可伸缩scalable：可以增加分布式容器备份
> - 可堆叠stackable：可以垂直、动态堆叠服务

Docker在容器的基础上，进行了进一步的封装，从文件系统、网络互联到进程隔离等等，极大的简化了容器的创建和维护。使得Docker技术比虚拟机更为轻便、快捷。

Docker和传统VM的区别![](/imgs/dockerVsVm.jpg)

## 2. Docker的优点

(相对于传统的虚拟机Virtual Machine)
### 2.1 更高效的利用系统资源

由于容器不需要进行硬件虚拟以及完整操作系统的额外开销，Docker对系统资源的利用率更高。应用执行速度、内存损耗、文件存储速度等等都要比传统虚拟机技术更高效。

### 2.2 更快速的启动时间

Docker容器应用直接运行于宿主内核，无需启动完整的操作系统，大大节省了开发、测试、部署的时间。

### 2.3 一致的运行环境

Docker的镜像确保了应用运行环境一致性，从而达到开发环境、测试环境、生产环境一致。由于Docker确保了执行环境的一致性，即无论物理机、虚拟机、公有云、私有云的运行结果是一致的 ，因此用户可以轻易的将在一个平台上运行的应用，迁移到另一个平台上。

### 2.4 持续交付和部署

开发人员可以通过Dockerfile来进行镜像构建，并结合持续集成CI(Continuous Integration)系统进行集成测试，而运维人员则可以直接在生产环境利用Dockerfile快速部署镜像，或 结合持续部署(Continuous Deployment)进行自动部署。

### 2.5 更轻松的维护和扩展

Docker使用的分层存储和镜像技术，使用镜像中的重复部分复用更加容易，也使得应用的维护更新更加简单。Docker团队及很多开源团队一起维护了大批高质量官方镜像。既可以直接在生产环境使用，又可以作为基础进一步定制，大大降低了应用服务的镜像制作成本。

## 3. 基本概念

### 3.1 镜像Image

操作系统包括内核空间和用户空间，对于Linux来说，内核启动后，会挂载root文件系统为其提供用户空间支持。

Image是一个可执行的包(executable package)，它包含运行应用程序所需的所有内容，包括代码、库、环境变量、配置文件。

> **分层存储**:
> 
> 因为镜像包含操作系统完整的root文件系统，其体积往往是庞大的，因此Docker设计时充分利用了Union FS的技术，将其设计为分层存储的架构。
> 镜像构建时，会一层层的构建，前一层是后一层的基础。每一层只需放需要添加的内容。

### 3.2 容器Container

image和container的关系类似class和instance的关系，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等，镜像相当于容器创建时的模版。

容器的实质是进程，但是和宿主机的进程不同，容器进程运行属于自己的独立命名空间，因此容器可以拥有自己的文件系统、网络配置、进程空间。容器内的进程运行在一个隔离的环境中，使用起来好像在一个独立的系统下操作一样。

容器本质也是利用了分层存储，即在自己使用的镜像上添加一个存储层。

### 3.3 Docker Registry&仓库Repository

Docker Registry是集中管理镜像的存储、分发的服务，用户可以上传、下载镜像到该服务。

> 公共Docker Registry<br/>
默认使用的Registry即Docker官方提供的https://hub.docker.com/，拥有大量的公开资源。因为国内网络原因，建议配合使用[阿里云的镜像加速器](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)<br/>
一些服务商也提供自己的公开服务，如[阿里云](https://cr.console.aliyun.com)、[DaoCloud](https://hub.daocloud.io/)<br/>
私有Docker Registry<br/>
用户也可根据官方文档私有化部署自己的服务。

## 4. Dockerfile的编写

Dockerfile就是一个名为Dockerfile的文本文件，它每一行就是一条指令，每条指令构建一层。

以下就是一个简单的Dockerfile
```
FROM nginx
RUN echo '<h1>hello, docker</h1>' > /usr/share/nginx/html/index.html
```

指令|说明|示例
-|-|-
FROM|指定所创建镜像的基础镜像|FROM java:8
MAINTAINER|指定维护者信息|MAINTAINER goddy
RUN|运行指令|RUN echo 'hello world' 或者 RUN ["echo", "hello, world"]
CMD|指定启动容器时默认执行的命令|CMD python3 app.py 或者 CMD ["nginx", "-g", "daemon off;"]
ENTRYPOINT|指定镜像的默认入口，相比于CMD，ENTRYPOINT可以在docker run xxx的后面急需添加参数|ENTRYPOINT python3 app.py 或 ENTRYPOINT ["nginx", "-g", "daemon off;"]
EXPOSE|声明镜像内服务所监听的端口|EXPOSE 80 8080
ARG|构建参数，加上等号相当于指定默认参数，arg指定的变量不会在容器运行中存在|ARG user=goddy
ENV|指定运行时的环境变量|ENV version=1.0 debug=on name='goddy wu'
ADD|添加文件到指定路径，推荐使用COPY|ADD app.py /code
COPY|添加文件到指定路径|COPY app.py /code
WORKDIR|指定之后指令运行的工作目录|WORKDIR /code
VOLUME|指定容器挂载点|VOLUME /data2 /data1
HEALTHCHECK|健康检查|HEALTHCHECK --interval=5s --timeout=3s CMD curl -fs http://localhost/ || exit 1
ONBUILD|只有在作为基础镜像时才会执行|ONBUILD COPY app.py /code

## 5. Docker的操作指令

### 5.1 操作镜像

```
# 下载镜像
$ docker pull nignx:latest

# 查看所有镜像
$ docker images
$ docker image ls nignx
$ docker images | grep nginx

# 打包镜像
$ docker save busybox:latest > busybox.tar
# 解压镜像
$ docker load < busybox.tar

# 删除镜像
$ docker rmi busybox:latest

# 生成镜像(当前目录包含dockerfile文件)
$ docker build -t busybox:2 .

# 添加别名
$ docker tag niginx nignx:4
```

### 5.2 操作容器

```
# 启动容器
$ docker run nginx -d

# 启动容器的bash终端
$ docker exec -it nginx (bash)
# 启动容器的shell终端
$ docker exec -it nginx /bin/sh

# 查看所有运行中的容器
$ docker ps
# 查看所有容器
$ docker ps -a

# 删除容器
docker rm xxxx
```

### 5.3 数据卷

## 6. docker-compose

docker compose是Docker官方维护的对Docker容器集群快速编排的系统，其代码库为https://github.com/docker/compose。

## 7. dockerignore

`.dockerignore`文件类似于`.gitignore`文件

## 8. 网络配置