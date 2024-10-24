# 第四章 Dockerfiles文件详解

# 1. 什么是Dockefile

Dockerfile文件是一个用来构建镜像的文本文件，文本文件内容包含了一条条构建镜像所需要的指令和说明。

# 2. 构建镜像

当我们创建好Dockefile文件后，我们就可以执行构建动作指令

```bash
sudo docker build -t NAME .
```

build：build指令用于构建docker镜像-t：-t指令用于指定镜像名称.：表示Dockerfile文件所在的路径

# 3. Dockefile文件指令详解

指令全部都是大写，后面跟具体的指令

| FROM | 构建镜像基于哪个镜像 |
| --- | --- |
| MAINTAINER | 镜像维护者名称 |
| RUN | 构建镜像时运行的指令 |
| CMD | 运行镜像时运行的指令 |
| VOLUME | 指定容器挂载点到宿主机自动生成的目录或者其他容器 |
| USER | 为RUN，CMD执行命令指定用户 |
| WORKDIR | 设置工作目录 |
| ARG | 构建时指定的一些参数 |
| EXPOSE | 声明容器的服务端口 |
| ENV | 设置容器环境变量 |
| ADD | 拷贝文件或者目录到容器中，如果是URL或者压缩包会自动下载或自动解压 |
| COPY | 拷贝文件或者目录到容器中，跟ADD类似，但不会自动解压或自动下载 |
| ENTRYPOINT | 运行容器时执行的shell命令 |