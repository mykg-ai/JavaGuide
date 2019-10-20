<p align="center">
  <img src="/imgs/docker-compose-logo.png" />
</p>

# 目录

- []()
- [参考资料](参考资料)

## docker-compose简介

docker-compose是利用docker-compose.yml来编排多个容器的工具，可以使docker的运行命令文件化，便于长期存储使用。利用简单的命令操作docker-compose.yml即可操作多个服务的开始、停止、重启。

使用步骤非常简单：

1. 利用Dockerfile创建您的服务，想好各种配置项，也可以直接使用已构建镜像或官方提供的镜像
1. 创建`docker-compose.yml`，编排所有需要的服务(services)
1. 在`docker-compose.yml`的父级文件夹下执行`docker-compose up -d`即可启动所有服务！

## 文件编写

最简单的docker-compose.yml示例：
```yaml
version: '2'

services:
  # 👇下面这个是service name
  web:
    build: .
    ports:
     - "5000:5000"
    volumes:
     - .:/code
  redis:
    image: redis
```

key|含义
-|-
version|compose文件版本号
services(list)|服务，包含的都是服务名称
build|镜像的Dockerfile位置，一般不使用
ports(list)|暴露到服务器内的端口`:`容器内的端口，仅仅服务间通信就不用暴露出来
volumes(list)|挂载到服务器内的位置(相对于当前目录)`:`容器内的目录
image|镜像名称
comand|启动容器后执行的命令
container_name|生成的容器名称，一般不用
depends_on(list)|服务启动依赖的其他服务，一般会写一些数据库服务
environment(dict/list)|环境变量，字典方式是`SECRET: aa`列表方式是`- SECRET=aa`
expose(list)|暴露端口给其他服务，一般不需要声明
health_check|??
read_only|挂载的volume不可以修改
restart|一般使用always即

## 操作

```shell
$ docker-compose --help

# 查看当前文件夹下的docker-compose的格式是否正确
$ docker-compose config

# 启动某一服务
$ docker-compose start <service-name>
# 启动所有服务
$ docker-compose up
# 启动所有服务并挂载到后台运行
$ docker-compose up -d

# 暂停所有服务
$ docker-compose stop
# 暂停某一服务
$ docker-compose stop <service-name>

# 重启服务
$ docker-compose restart

# 停止服务并删除容器，这个重启只能利用up
$ docker-compose down

# 重新构建服务
$ docker-compose build
# 重新构建某一服务
$ docker-compose build <service-name>

# 查看日志
$ docker-compose logs <service-name>

# 进入容器，注意没有-it哦
$ docker-compose exec <service-name> bash

# 查看各个服务的进程
$ docker-compose top

# 改变服务使用的容器数量
$ docker-compose scale <service-1>=2 <service-2>=3
```

## 参考资料