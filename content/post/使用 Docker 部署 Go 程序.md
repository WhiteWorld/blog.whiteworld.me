{
    "date": "2015-03-17",
    "description": null,
    "draft": false,
    "id": 16,
    "image": null,
    "meta_title": null,
    "slug": "deploy-go-apps-with-docker",
    "tags": [
        "Deploy",
        "Docker",
        "Go"
    ],
    "title": "\u4f7f\u7528 Docker \u90e8\u7f72 Go \u7a0b\u5e8f",
    "type": "post"
}


Go 是二进制部署，本身比较简单，结合 Docker 进行部署也比较容易。

1.编写 Dockerfile 文件，以部署 [zlist](https://github.com/zlisthq/zlist) 为例，Dockerfile 如下：

```dockerfile
# zlist
# 
# VERSION 1.0
MAINTAINER Whiteworld <ljq258@gmail.com>

# 使用 golang 这个 base image
FROM golang

# 直接从 github 上安装 Go 程序。如果要部署的 Go 应用代码没有公开在网上，可以使用下面注释的 ADD 和 RUN go install 代替 RUN go get
# ADD . /go/src/github.com/zlisthq/zlist
# RUN go install github.com/zlisthq/zlist
RUN go get github.com/zlisthq/zlist

# 如果源码里使用了相对路径，使用 WORKDIR 切换工作目录
WORKDIR /go/src/github.com/zlisthq/zlist

# 指定容器启动时运行的命令
ENTRYPOINT /go/bin/zlist

# 指定监听端口
EXPOSE 8080
```

2.构建镜像
切换到 Dockerfile 所在目录，执行`docker build -t <image_name> .`

3.从镜像运行容器
执行`docker run -d -p 5004:8080 --name <container_name> <image_name>`

4.管理容器
`docker restart/stop/start <container_name>`

参考：[Deploying Go servers with Docker](https://blog.golang.org/docker)