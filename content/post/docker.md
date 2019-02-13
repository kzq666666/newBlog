---
title: "Docker"
date: 2018-11-29T16:25:34+08:00
showDate: true
draft: false
tags: ["docker"]
---
记录学习docker的过程
### 特性
标准化
加速开发和构建流程，方便测试。容器可以在开发环境构建，轻松的提交到测试环境，并最终进入生产环境
### docker核心组件
* docker客户端和服务器（C/S）：docker引擎
* docker镜像
* 仓库Registry
* docker容器

### 安装
按照官网给的步骤一步一步来就好了
<br>https://docs.docker.com/install/

### 启动
```bash
$ systemctl start docker
```
### 运行一个容器
```bash
$ docker run -i -t centos /bin/bash
```
-i 开启标准输入(STDIN)
<br>-t 分配伪tty终端
设置了这两个参数就创建了一个我们可以交互的容器

### 附着到正在运行的容器
```bash
$ docker attach containerId/Name
```

### 删除容器
```bash
删除一个容器
$ docker rm containerId/Name

删除所有容器(-q是只显示容器id)
$ docker rm `docker ps -a -q`
```

### 镜像
拉取镜像
```bash
$ docker pull imageName:version
```

删除镜像
```bash
$ docker rmi imageName:version/id
```
查看镜像详细信息
```bash
$ docker inspect repositoryName/imageId
```
### 将镜像推送到Docker Hub
登录
```bash
$ docker login
Username:~
Password:~
```
推送
```bash
$ docker push Username/~:tag
push到远程仓库的镜像名必须是用户名开头的镜像，如果不是会被拒绝，改下镜像名字就好了
$ docker tag imageId Username/~:tag 
```
### 创建镜像
commit命令创建镜像
```bash
$ docker commit containerId/Name respositoryPath
```

Dockerfile创建镜像
```bash
$ mkdir buildEnv
$ cd buildEnv
$ touch Dockerfile
$ vim Dockerfile
# Dockerfile
# 指定基础镜像(base image)
FROM ubuntu:latest
# 申明作者以及邮箱
MAINTAINER Name "Email"
# 执行RUN指令
RUN apt-get update && apt-get install -y nginx 
RUN echo 'hello world' >/usr/share/nginx/html/index.html
# 暴露端口
EXPOSE 80

$ docker build -t="kzq/nginx" .

启动镜像
$ docker run -d -p 80 "kzq/nginx" nginx -g "daemon off;"
// -d以分离（detached）的方式在后台运行 -p公开端口给宿主机
```
### 自动化工具docker-compose
Compose is a tool for defining and running multi-container Docker applications
<br>Compose是一个用于定义和运行多容器Docker应用程序的工具

* 安装
  <br>话不多说，官网文档大法好
  <br>https://docs.docker.com/compose/install/
* 三步走
  <br>(1)创建Dockerfile搭建环境
  <br>(2)创建docker-compose.yml配置服务
  <br>(3)运行`docker-compose up`
* docker-compose.yml格式(注意空格)

  ```bash
  version: '3'
    services:
        web:
            ports:
            - "5000:5000"
            volumes:
            - .:/code
            - logvolume01:/var/log
            links:
            - redis
        redis:
            image: redis
    
  ```
### nginx配置
```bash
# 用户名
user nginx;
# 工作进程数
worker_processes auto;
# 错误日志
error_log /var/log/nginx/error.log;
# 进程管理
pid /run/nginx.pid;

# Load dynamic modules. 加载动态模块
include /usr/share/nginx/modules/*.conf;

# events模块，处理连接的设置
events {
    # 每个进程的最大连接数
    worker_connections 1024;
}

# http服务
http {
    # 日志格式
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    # 访问日志
    access_log  /var/log/nginx/access.log  main;
    # sendfile传输文件系统
    # 传统方法：硬盘->内核缓冲区->用户缓冲区->内核socket缓冲区->协议引擎
    # sendfile方法:硬盘->内核缓冲区->内核socket缓存区->协议引擎 
    # sendfile系统调用DMA引擎直接将文件数据从内核缓存区拷贝到内核socket缓冲区，提高了性能
    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    # 连接超时时间
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
}
```
